# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

- `npm install` - Install dependencies
- `npx expo prebuild` - Required before running on devices (whisper.rn dependency needs native compilation)
- `npm start` or `npx expo start` - Start development server
- `npm run android` - Run on Android emulator/device
- `npm run ios` - Run on iOS simulator/device
- `npm run lint` - Run ESLint

## Testing

- `npm test` - Run all unit tests
- `npm run test:watch` - Run tests in watch mode (re-runs on file changes)
- `npm run test:coverage` - Run tests with coverage report
- `npm run test:ci` - Run tests in CI mode with coverage

### Test Structure

- Unit tests are located in `src/__tests__` directory
- Test files follow the naming convention `*.test.ts` or `*.test.tsx`
- Common mocks and test setup are configured in `jest.setup.js`
- Use `@testing-library/react-native` for component testing
- Follow DRY principles: extract common test fixtures, helpers, and assertions

## Dependencies

- Add/remove dependencies by using `npm install libraryname` / `npm uninstall libraryname`. specify version and semantic version (semver) when installing if needed e.g., `npm install libraryname@1.2.3`. This ensures that `package-lock.json` is updated which is needed for `npm ci`. Do not edit `package.json` directly.

### Writing Tests

- Keep tests focused and small (one assertion per test when possible)
- Use descriptive test names that explain the expected behavior
- Mock external dependencies (AsyncStorage, file system, etc.)
- Prefer pure function testing over complex integration tests
- Ensure tests are deterministic and don't depend on execution order

## Project Architecture

This is an **Expo/React Native project with Whisper.rn integration** for on-device speech recognition.

### Platform Considerations

- **iOS**: Uses Core ML with `.mlmodelc` model files for model inference
- **Android**: Uses Google LiteRT with TensorFlow Lite models for model inference

### Critical Setup Steps

1. Install dependencies with `npm run setup`
2. **Must run `npx expo prebuild`** before device testing (native module requirement)

## Development Notes

- New architecture enabled (`"newArchEnabled": true`)
- Typed routes and React Compiler experiments enabled
- File-based routing with Expo Router
- Requires development builds for device testing (not compatible with Expo Go due to native modules)

## On Software Quality

Apply the DRY, SOLID, KISS, YAGNI principles for software quality.

Functions should be small (ideally 1-4 lines), do one thing, and have low indentation levels to enhance readability.

Apply SRP: Every unit of code you write (function, class, module, component, hook) must have one primary responsibility and therefore one main reason to change. When writing or modifying code: Ask: “What is the single responsibility of this piece of code?”, Ask: “What reasons might force me to change it?”. If the answer includes more than one distinct reason, refactor or design separate pieces of code until each has just one clear reason to change.

Limit the number of function arguments to no more than three for simplicity and clarity.

Avoid passing boolean flags into functions as they often indicate different behaviors better handled by separate functions.

Eliminate duplicated code by adhering to the DRY (Don't Repeat Yourself) principle—extract duplicated logic into reusable functions.

Write code that reads like well-written prose and avoid code that demands double takes or surprises the reader.

Choose meaningful, pronounceable variable names that indicate their purpose clearly.

Follow the Command Query Separation principle: functions either perform an action (command) or return data (query), but not both.

Write pure functions where possible that don’t have side effects or alter input arguments.

Prefer throwing exceptions over returning error codes to handle errors cleanly.

Keep code well-formatted with consistent rules, vertical spacing, small files, and variables declared close to their use.

## On Commenting

Comments should not repeat what the code is saying. Instead, reserve comments
for explaining **why** something is being done, or to provide context that is not
obvious from the code itself.

Bad:

```py
# Increment the retry count by 1
retries += 1
```

Good:

```py
# Some APIs occasionally return 500s on valid requests. We retry up to 3 times
# before surfacing an error.
retries += 1
```

When to Comment

- To explain why a particular approach or workaround was chosen.
- To clarify intent when the code could be misread or misunderstood.
- To provide context from external systems, specs, or requirements.
- To document assumptions, edge cases, or limitations.

When Not to Comment

- Don't narrate what the code is doing — the code already says that.
- Don't duplicate function or variable names in plain English.
- Don't leave stale comments that contradict the code.

Avoid comments that reference removed or obsolete code paths (e.g. "No longer
uses X format"). If compatibility code or legacy behavior is deleted, comments
about it should also be deleted. The comment should describe the code that
exists now, not what used to be there. Historic details belong in commit
messages or documentation, not in-line comments.
