# Copilot Instructions for DemoApp

## Project Overview
- **DemoApp** is a cross-platform mobile/web app built with [Expo](https://expo.dev) and React Native, using file-based routing (see `app/`).
- The project was scaffolded with `create-expo-app` and uses the [expo-router](https://docs.expo.dev/router/introduction) for navigation.
- Major UI and logic are organized under `app/` (routes/pages), `components/` (reusable UI), `constants/`, and `hooks/`.
- Assets (images/icons) are in `assets/images/` and referenced in `app.json` for platform-specific configuration.

## Key Workflows
- **Install dependencies:** `npm install`
- **Start development server:** `npx expo start` (opens Metro bundler, supports Android/iOS/web)
- **Reset to blank project:** `npm run reset-project` (runs `scripts/reset-project.js`)
- **Build for web:** See `expo build:web` or refer to Expo docs for platform-specific builds.

## Routing & Structure
- **File-based routing:**
  - Files in `app/` map to routes. E.g., `app/(tabs)/explore.tsx` → `/explore` tab.
  - Layouts: `_layout.tsx` files define shared layouts for route groups.
  - Modal routes: `modal.tsx` in `app/` is a modal screen.
- **Typed routes:** Enabled via `app.json` (`experiments.typedRoutes: true`). Use route types for navigation safety.

## Patterns & Conventions
- **Theming:** Use hooks in `hooks/` (e.g., `use-theme-color.ts`) and constants in `constants/theme.ts` for color/theme logic.
- **UI Components:** Prefer using or extending components in `components/` and `components/ui/`.
- **Platform-specific code:** Use `.ios.tsx`, `.web.tsx`, etc. for platform overrides (see `icon-symbol.ios.tsx`).
- **Splash/icon assets:** Managed in `app.json` and `assets/images/`.

## Integration Points
- **Expo plugins:** See `app.json` for plugins like `expo-router` and `expo-splash-screen`.
- **New architecture:** `newArchEnabled: true` in `app.json` enables React Native's new architecture (Fabric/TurboModules).

## Tips for AI Agents
- Always update or reference `app.json` for platform config changes.
- When adding routes, follow the file-based routing pattern in `app/`.
- For new UI, check for reusable components in `components/` before creating new ones.
- Use hooks from `hooks/` for theme and color logic.
- For project resets, use the provided script (`npm run reset-project`).

## References
- [Expo Router Docs](https://docs.expo.dev/router/introduction)
- [Expo App Config](https://docs.expo.dev/workflow/app-config/)
- [Expo Theming](https://docs.expo.dev/guides/using-custom-themes/)
