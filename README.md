# Android Developer Verifier Placeholder

This Flutter app is a test placeholder that uses the package name `com.google.android.verifier`. It is meant for compatibility and safety checks on Android devices where you want to test how a placeholder app behaves when the Play Store tries to identify the app.

## What this app is for

This is a test app. After installing it, opening the Play Store and checking the installed app will show it under the name Android Developer Verifier because the package name matches the official app identity.

This project was created to demonstrate that a placeholder app can block the official app from updating or reinstalling when the package name is already occupied.

## Important note about the behavior

Your device did not have the Android Developer Verifier app previously. After installing this placeholder app, the Play Store recognizes the package name `com.google.android.verifier` and treats it as if the official app is present.

### 1. How your placeholder blocks the official app
Because your custom app is currently installed, it acts as a shield using two rules built into Android:

- Signature Block: Your placeholder is signed with your own debug/test key. The official Google app is signed with Google's private key. Android will never allow an update from a different developer key to overwrite an existing app.
- Version Block: Your version code (`2100000000`) is much higher than anything Google will release for years. Android automatically rejects updates that have a lower version number than the one already installed.

If the Play Store or your phone tries to silently install or update the official app in the background, the installation will fail automatically.

### 2. Why the app disappeared when you tapped Uninstall
When you looked up the app on the Play Store, Google recognized the package name (`com.google.android.verifier`) on your device and assumed it was the real app.

When you tapped Uninstall, the Play Store successfully removed the app you built.

- The Risk: Now that your placeholder app is gone, the package name is completely vacant. The official Google app can now install itself freely because your shield has been removed.

## Build the APK

Run these commands in the project folder:

```bash
flutter pub add -d change_app_package_name
dart run change_app_package_name:main com.google.android.verifier
flutter clean
flutter pub get
flutter build apk --release --build-name="999.999.999" --build-number=2100000000
```

The APK will be generated at:

```text
build/app/outputs/flutter-apk/app-release.apk
```

The latest APK is also stored in the repository folder:

```text
apk/app-release.apk
```

You can download it directly from GitHub at:

```text
https://github.com/Sundeeppazhoor/Android-Developer-Verifier-Placeholder/raw/main/apk/app-release.apk
```

