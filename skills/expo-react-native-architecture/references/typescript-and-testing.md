# TypeScript and testing with Expo

Use the repository's installed Expo SDK, TypeScript configuration, and test setup as the source of truth. Preserve existing conventions and choose checks that cover the behavior changed.

## TypeScript

- Inspect `tsconfig.json` and `package.json` before changing compiler settings or adding types.
- Keep route parameters, feature contracts, and API boundaries typed. Use runtime validation for untrusted values when correctness or security requires it; static types do not validate runtime data.
- Check Expo's current TypeScript guidance before changing Expo-specific configuration.

## Testing

- Prefer the existing test runner and scripts in the project. Do not introduce a new testing stack for a narrow change without a concrete need.
- Test pure business rules and utilities at the unit boundary; test important component behavior and critical user journeys at the appropriate integration or end-to-end boundary.
- For changes to native dependencies or app configuration, use an available Expo prebuild or platform check in addition to JavaScript-level tests when appropriate.
- Report which checks ran and any that could not run. Do not claim an unrun check passed.

## Official documentation

- [TypeScript with Expo](https://docs.expo.dev/guides/typescript/)
- [Unit testing in Expo](https://docs.expo.dev/develop/unit-testing/)
