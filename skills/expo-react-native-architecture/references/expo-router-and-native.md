# Expo Router and native boundaries

Use this reference when adding or moving routes, changing navigation behavior, or integrating native capabilities.

## Expo Router

- Use route groups such as `(auth)` and `(app)` to organize navigation without adding those group names to the URL. Dynamic segments such as `[id].tsx` represent parameterized routes.
- Use layouts for shared navigation and route-group behavior. Put session loading or route gating in a layout only when it belongs to that group; keep session state in its designated source of truth.
- Keep authentication and authorization decisions explicit. Hiding a screen in navigation does not replace backend authorization.
- Avoid duplicating Expo Router's route structure in a second navigation system unless there is a compelling requirement.
- Check route parameter types and navigation APIs against the installed Expo Router version.
- When moving or renaming routes, preserve externally used paths and deep links. Route groups do not appear in URLs, while route segments do.

## Native dependencies and app configuration

- Before adding a native library, check its Expo SDK compatibility, whether it needs a config plugin, and whether it works in Expo Go or requires a development build.
- Use Expo's SDK-aware package installation guidance for native dependencies; do not guess compatible versions from React Native versions alone.
- Keep app-wide native setup in app configuration and config plugins. Avoid hand-editing generated `ios/` or `android/` projects unless the repository intentionally maintains native projects.
- Check permissions, config changes, and required rebuilds when adding or changing native capabilities. A JavaScript reload does not apply every native configuration change.

## Platform-specific behavior

- Use React Native and Expo APIs appropriate to the target platform; do not assume browser-only APIs are available on native platforms.
- Use platform-specific files such as `.ios.tsx` and `.android.tsx` only when behavior or native APIs truly differ. Keep shared behavior in the feature and make platform differences explicit at the boundary.
- Preserve platform-specific behavior when refactoring, and verify affected platforms when the repository makes those checks available.

## Official documentation

- [Expo documentation](https://docs.expo.dev/)
- [Expo Router authentication](https://docs.expo.dev/router/advanced/authentication/)
- [React Native documentation: Getting started](https://reactnative.dev/docs/getting-started)
