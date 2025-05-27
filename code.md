# 📱 Flutter App Setup Guide

This guide provides useful Flutter commands and configurations for:

- Creating secure APKs and App Bundles
- Locking screen orientation
- Enabling edge-to-edge UI in your Flutter app

---

## 🔐 1. Creating Secure Builds

### ✅ Secure APK

To create a release APK with code obfuscation and separated debug info:

```bash
flutter build apk --release --obfuscate --split-debug-info=build/debug_info
```

### ✅ Secure App Bundle (AAB)

To generate an AAB for Play Store deployment with similar security:

```bash
flutter build appbundle --release --obfuscate --split-debug-info=build/debug_info
```

> 📂 The `build/debug_info` directory will contain symbol files for stack trace de-obfuscation.

---

## 🔒 2. Lock Screen Rotation

To restrict your app to **portrait mode only**, use the following code in your `main.dart` file (inside the `main()` function):

```dart
SystemChrome.setPreferredOrientations([
  DeviceOrientation.portraitUp,
]);
```

> 📌 Import required package:
> ```dart
> import 'package:flutter/services.dart';
> ```

---

## 🖼️ 3. Enable Edge-to-Edge UI

### ✨ a) Flutter Configuration in `main.dart`

Add this to your `main()` or before running the app:

```dart
EdgeToEdge.configure(
  statusBarColor: Colors.transparent,
  navigationBarColor: Colors.black,
  statusBarIconBrightness: Brightness.light,
  navigationBarIconBrightness: Brightness.dark,
  enableTop: true,
  enableBottom: true,
);
```

> 📌 Required imports:
> ```dart
> import 'package:flutter/services.dart';
> import 'package:edge_to_edge/edge_to_edge.dart';
> ```

🔗 [Edge-to-Edge pub.dev page](https://pub.dev/packages/edge_to_edge)

---

### ✨ b) Native Android Configuration in `styles.xml`

To fully enable edge-to-edge behavior on Android, add the following in your `styles.xml` file (`android/app/src/main/res/values/styles.xml`):

```xml
<item name="android:windowOptOutEdgeToEdgeEnforcement">true</item>
```

Insert this inside your app theme:

```xml
<style name="AppTheme" parent="Theme.AppCompat.Light.NoActionBar">
    <!-- Existing style items -->
    <item name="android:windowOptOutEdgeToEdgeEnforcement">true</item>
</style>
```

---

## ✅ Summary

| Feature              | Code/Command                                         |
|----------------------|------------------------------------------------------|
| Secure APK           | `flutter build apk --release --obfuscate ...`       |
| Secure AAB           | `flutter build appbundle --release --obfuscate ...` |
| Lock Rotation        | `SystemChrome.setPreferredOrientations([...])`       |
| Edge-to-Edge Flutter | `EdgeToEdge.configure(...)`                          |
| Edge-to-Edge Android | `<item name="android:windowOptOutEdgeToEdgeEnforcement">true</item>` |

---

**Happy coding!** ✨
