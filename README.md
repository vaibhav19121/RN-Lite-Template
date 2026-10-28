# RN Lite Template

A lightweight React Native 0.88 (TypeScript) template, based on the official
community CLI template.

## Requirements

- Node.js **22.11+**
- A working React Native environment
  ([setup guide](https://reactnative.dev/docs/set-up-your-environment))
- iOS: Xcode, Ruby + Bundler (for CocoaPods)
- Android: Android Studio + JDK 17

## Create an app

### Straight from GitHub (recommended)

```sh
npx @react-native-community/cli@latest init MyApp \
  --template https://github.com/vaibhav19121/RN-Lite-Template.git
```

To pin a specific branch or tag, append it after `#`:

```sh
npx @react-native-community/cli@latest init MyApp \
  --template https://github.com/vaibhav19121/RN-Lite-Template.git#main
```

### From a local clone

```sh
git clone https://github.com/vaibhav19121/RN-Lite-Template.git
npx @react-native-community/cli@latest init MyApp \
  --template file://$(pwd)/RN-Lite-Template
```

### Useful options

| Flag                          | Purpose                                       |
| ----------------------------- | --------------------------------------------- |
| `--package-name com.acme.app` | Android package / iOS bundle identifier       |
| `--title "My App"`            | Display name shown under the app icon         |
| `--directory ./my-app`        | Folder to create the project in               |
| `--skip-install`              | Skip `npm install` (install manually later)   |

`MyApp` replaces the `HelloWorld` placeholder in all native project files.

## Run it

```sh
cd MyApp

# iOS
cd ios && bundle install && bundle exec pod install && cd ..
npm run ios

# Android
npm run android
```

Metro starts automatically; run `npm start` yourself if it doesn't.

Set your backend URL in `src/config.ts` (`API_BASE_URL`).

## What's inside

| Concern       | Library                                         |
| ------------- | ----------------------------------------------- |
| Navigation    | React Navigation 7 (native stack + bottom tabs) |
| Icons         | react-native-vector-icons (Ionicons)            |
| Server state  | axios + @tanstack/react-query                   |
| Client state  | zustand, persisted with react-native-mmkv       |
| Safe areas    | react-native-safe-area-context                  |

## Folder structure

```
src/
├── api/          axios client (auth header, 401 handling) + QueryClient
├── assets/       images, fonts
├── components/   shared UI: Button, FloatingTabBar, SafeAreaLayout, ...
├── config.ts     app constants (API_BASE_URL)
├── hooks/        shared hooks (useXyz.ts)
├── navigation/   RootNavigator (stack), BottomTabs, typed param lists
├── screens/      one file per screen: XyzScreen.tsx
├── store/        zustand stores + MMKV storage adapter
├── theme/        colors (light/dark), fonts, spacing, makeStyles, nav themes
├── types/        ambient .d.ts declarations
└── utils/        pure helpers
```

## Conventions

- **Styles:** `const useStyles = makeStyles(colors => ({ ... }))`, then
  `const styles = useStyles()` in the component. Light/dark mode is automatic.
- **Tabs** have no header; `SafeAreaLayout` keeps content below the status bar.
  **Stack screens** (Details, Create) keep the header and back button.
- **Add a tab:** add it to `BottomTabParamList`, `TAB_ICONS` and the navigator.
  Tabs split evenly around the centre "+" button. Remove `onCenterPress` in
  `BottomTabs.tsx` to hide that button.
- **Add a pushed screen:** add it to `RootStackParamList` and `RootNavigator`.
  `useNavigation()` is typed globally, so no generics are needed.
- **Safe areas:** read insets per edge (`insets.left`, `insets.right`). Never
  assume left equals right.

## Troubleshooting

- **Template not found / git error:** make sure `git` is installed and the
  repo URL ends in `.git`. Fall back to the local clone method above.
- **Pod install fails:** run `bundle install` first, then
  `bundle exec pod install --repo-update` inside `ios/`.
- **Icons show as boxes:** rebuild the native app after installing
  (`npm run ios` / `npm run android`), not just reload Metro.

## Working on the template itself

Everything under `template/` is copied into new apps. Files that start with
`_` (e.g. `_gitignore`, `_eslintrc.js`) are renamed to `.` files on init.
Test changes with the local clone method before pushing.

## License

MIT, see [LICENSE](LICENSE).
