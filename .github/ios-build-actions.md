# GitHub Actions: iOS Build Caching & Architecture Comparison

## iOS Build Caching (CocoaPods & DerivedData)

- **Pods cache:** Use `actions/cache` to cache `ios/Pods` and `ios/Podfile.lock`.
- **DerivedData cache:** Cache `~/Library/Developer/Xcode/DerivedData` to speed up subsequent builds.
- **Restore caches before build, save after.**

## Architecture Comparison (Intel vs Apple Silicon)

- Use `runs-on: macos-13` (Intel) and `runs-on: macos-14` (Apple Silicon) in your workflow jobs.
- Run identical build steps on both runners.
- Use `time` or Actions timing to measure build duration.

## Example Workflow Snippet

```yaml
jobs:
  build-intel:
    runs-on: macos-13
    steps:
      - uses: actions/checkout@v4
      - uses: actions/cache@v4
        with:
          path: ios/Pods
          key: pods-${{ hashFiles('ios/Podfile.lock') }}
      - uses: actions/cache@v4
        with:
          path: ~/Library/Developer/Xcode/DerivedData
          key: deriveddata-${{ github.sha }}
      - name: Install CocoaPods
        run: cd ios && pod install
      - name: Build iOS
        run: time xcodebuild -workspace ios/YourApp.xcworkspace -scheme YourApp -configuration Release

  build-apple-silicon:
    runs-on: macos-14
    steps:
      # ...same as above...
```

## Project-Specific Notes

- The `Podfile` and `ios/` directory are now present after ejecting.
- Update `YourApp` in the workflow to match your actual Xcode scheme/workspace.
- For Expo/React Native, the first build after pod install is slow; caching helps most on subsequent builds.

## References

- [GitHub Actions: Caching dependencies](https://docs.github.com/en/actions/using-workflows/caching-dependencies-to-speed-up-workflows)
- [React Native iOS build caching example](https://github.com/actions/cache/blob/main/examples.md#react-native)
- [Expo eject docs](https://docs.expo.dev/bare/using-expo-client/)
