# Flutter / Dart rules

- Confirm Flutter SDK/FVM version from repo, `pubspec.yaml`, `pubspec.lock` and CI. Prefer `fvm flutter` if configured and available; otherwise the repo's standard `flutter` command.
- Follow widget and feature folder conventions, project theme (`ThemeData`, `ColorScheme`, extensions), `AppSpacing`/existing tokens, `l10n`, routes, and dependency injection. Use `const` when valid; avoid unnecessary widget state and large build methods.
- If Riverpod is present: use the repository's provider APIs and ownership conventions; scope `ref.watch` to reactive reads and `ref.read` to events; avoid triggering side effects inside `build`; manage auto-disposal/async invalidation and stale results.
- If `reactive_forms` is present: preserve control names, typed validators, touched/dirty state, submission guards and error display; do not introduce a second form-state source of truth.
- Prefer `LayoutBuilder`, `MediaQuery`, constraints, `Flexible`/`Expanded`, scrollable content, and safe areas to fixed sizes. Check long localizations, text scaling, keyboard insets and overlay placement.
- Respect null safety. Avoid `!` unless guarded. Handle `AsyncValue` loading/error/data and enum fallback branches explicitly.
- When using generated Freezed/JSON/OpenAPI clients, modify upstream schema or generator inputs when possible, and run the project's generation workflow rather than manually editing generated files.
- Validate with repository-supported commands, commonly `dart format`, `flutter analyze`, `flutter test`, and where appropriate target platform builds. Only run `flutter pub get` when dependency state requires it. Do not change platform signing/Firebase configs merely to make an unrelated check pass.
