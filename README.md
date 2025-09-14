<div align="center">

# 📱 Flutter App Version Checker Fixed

[![pub package](https://img.shields.io/pub/v/flutter_app_version_checker_fixed.svg)](https://pub.dev/packages/flutter_app_version_checker_fixed)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Platform](https://img.shields.io/badge/platform-Android%20%7C%20iOS-blue.svg)](https://flutter.dev/)
[![Flutter](https://img.shields.io/badge/Flutter-02569B?logo=flutter&logoColor=white)](https://flutter.dev/)

A modern, lightweight Flutter package for checking app version updates on Google Play Store and Apple App Store with enhanced error handling and improved reliability.

[Features](#-features) • [Installation](#-installation) • [Usage](#-usage) • [API Reference](#-api-reference) • [Contributing](#-contributing)

</div>

---

## ✨ Features

<div align="center">

| Feature | Description |
|---------|-------------|
| 🔄 **Version Comparison** | Smart version comparison with semantic versioning support |
| 🏪 **Multi-Store Support** | Google Play Store, Apple App Store, and APKPure |
| 🎯 **Auto-Detection** | Automatic app ID and version detection |
| 🛡️ **Error Handling** | Comprehensive error reporting and debugging |
| 📱 **Cross-Platform** | Full Android and iOS support |
| ⚡ **Lightweight** | Minimal dependencies and fast performance |
| 🔧 **Customizable** | Flexible configuration options |

</div>

## 🚀 Installation

Add this to your package's `pubspec.yaml` file:

```yaml
dependencies:
  flutter_app_version_checker_fixed: ^0.3.3
```

Then run:
```bash
flutter pub get
```

### 📦 Alternative Installation Methods

<details>
<summary><strong>From GitHub (Latest)</strong></summary>

```yaml
dependencies:
  flutter_app_version_checker_fixed:
    git:
      url: https://github.com/boughdiri-dorsaf/flutter_app_version_checker_fixed.git
      ref: main
```

</details>

<details>
<summary><strong>From Local Path</strong></summary>

```yaml
dependencies:
  flutter_app_version_checker_fixed:
    path: ./path/to/flutter_app_version_checker_fixed
```

</details>

## 📱 Platform Support

<div align="center">

| Platform | Play Store | App Store | APKPure | Auto-Detection |
|----------|:----------:|:---------:|:-------:|:--------------:|
| **Android** | ✅ | ❌ | ✅ | ✅ |
| **iOS** | ❌ | ✅ | ❌ | ✅ |

</div>

## 🔧 Quick Start

### Basic Usage

```dart
import 'package:flutter_app_version_checker_fixed/flutter_app_version_checker.dart';

class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> {
  final _checker = AppVersionChecker();

  @override
  void initState() {
    super.initState();
    _checkForUpdates();
  }

  Future<void> _checkForUpdates() async {
    try {
      final result = await _checker.checkUpdate();
      
      if (result.canUpdate) {
        _showUpdateDialog(result);
      } else {
        print('App is up to date!');
      }
    } catch (e) {
      print('Error checking for updates: $e');
    }
  }

  void _showUpdateDialog(AppCheckerResult result) {
    showDialog(
      context: context,
      builder: (context) => AlertDialog(
        title: Text('Update Available'),
        content: Text('New version ${result.newVersion} is available!'),
        actions: [
          TextButton(
            onPressed: () => Navigator.pop(context),
            child: Text('Later'),
          ),
          ElevatedButton(
            onPressed: () {
              // Open app store
              launchUrl(Uri.parse(result.appURL ?? ''));
              Navigator.pop(context);
            },
            child: Text('Update'),
          ),
        ],
      ),
    );
  }
}
```

### Advanced Configuration

```dart
// Custom app ID and version
final checker = AppVersionChecker(
  appId: "com.example.myapp",
  currentVersion: "1.0.0",
  androidStore: AndroidStore.googlePlayStore,
);

// Check specific app
final result = await checker.checkUpdate();
```

### Using Different Android Stores

```dart
// Google Play Store (default)
final playStoreChecker = AppVersionChecker(
  androidStore: AndroidStore.googlePlayStore,
);

// APKPure Store
final apkPureChecker = AppVersionChecker(
  appId: "com.vanced.android.youtube",
  androidStore: AndroidStore.apkPure,
);
```

## 📚 API Reference

### AppVersionChecker Class

#### Constructor
```dart
AppVersionChecker({
  String? appId,           // App identifier (auto-detected if null)
  String? currentVersion,  // Current version (auto-detected if null)
  AndroidStore? androidStore, // Android store to use
})
```

#### Methods
| Method | Return Type | Description |
|--------|-------------|-------------|
| `checkUpdate()` | `Future<AppCheckerResult>` | Check for app updates |

### AppCheckerResult Class

#### Properties
| Property | Type | Description |
|----------|------|-------------|
| `canUpdate` | `bool` | Whether an update is available |
| `currentVersion` | `String` | Current app version |
| `newVersion` | `String?` | Latest available version |
| `appURL` | `String?` | App store URL |
| `errorMessage` | `String?` | Error message if any |

### AndroidStore Enum
- `AndroidStore.googlePlayStore` - Google Play Store (default)
- `AndroidStore.apkPure` - APKPure store

## 🛠️ Setup

### Android Setup
No additional configuration required! The package automatically detects your app ID and version.

### iOS Setup
No additional configuration required! The package automatically detects your app ID and version.

## 🚨 Troubleshooting

### Common Issues

<details>
<summary><strong>❌ No Update Detected</strong></summary>

- Verify the app ID is correct
- Check if the app exists on the specified store
- Ensure the app is published and available

</details>

<details>
<summary><strong>🌐 Network Errors</strong></summary>

- Check internet connectivity
- Verify store URLs are accessible
- Handle network timeouts gracefully

</details>

<details>
<summary><strong>📱 Store Not Found</strong></summary>

- Confirm the app exists on the specified store
- Check app ID format (e.g., com.example.app)
- Verify store selection is correct

</details>

### Debug Information

```dart
final checker = AppVersionChecker();
final result = await checker.checkUpdate();

print('''
Debug Information:
- Can update: ${result.canUpdate}
- Current version: ${result.currentVersion}
- New version: ${result.newVersion}
- App URL: ${result.appURL}
- Error: ${result.errorMessage ?? 'None'}
''');
```

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guidelines](CONTRIBUTING.md) for details.

### Development Setup

1. Fork the repository
2. Create a feature branch: `git checkout -b feature/amazing-feature`
3. Make your changes
4. Run tests: `flutter test`
5. Commit your changes: `git commit -m 'Add amazing feature'`
6. Push to the branch: `git push origin feature/amazing-feature`
7. Open a Pull Request

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 📞 Support

<div align="center">

| Support Channel | Description |
|----------------|-------------|
| 🐛 [Issues](https://github.com/boughdiri-dorsaf/flutter_app_version_checker_fixed/issues) | Report bugs and request features |
| 💬 [Discussions](https://github.com/boughdiri-dorsaf/flutter_app_version_checker_fixed/discussions) | Ask questions and share ideas |
| 📧 Email | Contact the maintainer directly |

</div>

## 🔄 Changelog

See [CHANGELOG.md](CHANGELOG.md) for a detailed list of changes and updates.

## ⭐ Show Your Support

If this package helped you, please give it a ⭐ on [pub.dev](https://pub.dev/packages/flutter_app_version_checker_fixed) and [GitHub](https://github.com/boughdiri-dorsaf/flutter_app_version_checker_fixed)!

---

<div align="center">

**Made with ❤️ by [boughdiri-dorsaf](https://github.com/boughdiri-dorsaf)**

[![GitHub](https://img.shields.io/badge/GitHub-100000?style=for-the-badge&logo=github&logoColor=white)](https://github.com/boughdiri-dorsaf)
[![Pub.dev](https://img.shields.io/badge/Pub.dev-0175C2?style=for-the-badge&logo=dart&logoColor=white)](https://pub.dev/packages/flutter_app_version_checker_fixed)

</div>