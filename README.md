# RN Lite Template

A lightweight React Native 0.88 (TypeScript) template, based on the official
community CLI template.

## Create an app

```sh
npx @react-native-community/cli@latest init MyApp \
  --template file:///absolute/path/to/RN-Lite-Template
cd MyApp && cd ios && bundle install && bundle exec pod install && cd ..
npx react-native run-ios   # or run-android
```

`MyApp` replaces the `HelloWorld` placeholder in all native project files.

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
