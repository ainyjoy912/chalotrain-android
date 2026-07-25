# ChaloTrain Android App

A native Android WebView wrapper for ChaloTrain.com that provides seamless access to railway booking and management tools.

## Features

- **Secure WebView**: Opens https://chalotrain.com in a secure WebView container
- **Full Website Integration**: All website features and railway tools work inside the Android app
- **JavaScript Support**: JavaScript enabled for dynamic content
- **DOM Storage**: Local storage and database support for data persistence
- **Responsive Design**: Mobile-optimized display with proper viewport settings
- **External Link Handling**: External links open in device browser; internal links stay within the app
- **File Download Support**: Download functionality enabled
- **Back Button Navigation**: Back button navigates through WebView history
- **Automatic CI/CD**: GitHub Actions builds debug APK on every push

## Project Structure

```
chalotrain-android/
├── app/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/chalotrain/app/
│   │   │   │   └── MainActivity.java
│   │   │   ├── res/
│   │   │   │   ├── layout/
│   │   │   │   │   └── activity_main.xml
│   │   │   │   ├── values/
│   │   │   │   │   ├── colors.xml
│   │   │   │   │   ├── strings.xml
│   │   │   │   │   └── themes.xml
│   │   │   │   └── xml/
│   │   │   │       ├── backup_descriptor.xml
│   │   │   │       └── data_extraction_rules.xml
│   │   │   └── AndroidManifest.xml
│   │   ├── test/
│   │   └── androidTest/
│   ├── build.gradle
│   └── proguard-rules.pro
├── gradle/wrapper/
├── .github/workflows/
│   └── build.yml
├── build.gradle
├── settings.gradle
├── gradlew
├── gradlew.bat
└── README.md
```

## Requirements

- Android SDK 21 (Android 5.0) or higher
- JDK 11
- Gradle 8.1.1

## Building Locally

### Prerequisites

1. Install Android Studio or Android SDK command-line tools
2. Set up ANDROID_HOME environment variable
3. Ensure JDK 11 is installed

### Build Debug APK

```bash
./gradlew assembleDebug
```

The APK will be generated at: `app/build/outputs/apk/debug/app-debug.apk`

### Build Release APK

```bash
./gradlew assembleRelease
```

### Run Tests

```bash
./gradlew test
```

## Installation

### From GitHub Actions

1. Navigate to the repository's **Actions** tab
2. Select the latest successful build workflow run
3. Under **Artifacts**, download **ChaloTrain-APK**
4. Extract the APK file
5. Transfer to your Android device or use Android Debug Bridge (adb):
   ```bash
   adb install app-debug.apk
   ```

### Manual Installation

1. Enable "Unknown Sources" in Android device settings (Security)
2. Transfer the APK to your device
3. Open file manager and tap the APK file
4. Follow the installation prompts

## App Permissions

The app requests the following permissions:

- **INTERNET**: Required for WebView to access chalotrain.com
- **READ_EXTERNAL_STORAGE**: For accessing files during downloads
- **WRITE_EXTERNAL_STORAGE**: For saving downloaded files
- **ACCESS_NETWORK_STATE**: For checking network connectivity

## Architecture

### MainActivity

The main entry point of the application that:

- Sets up WebView with security and feature configuration
- Loads chalotrain.com with proper user agent
- Handles internal and external URL navigation
- Manages back button behavior for WebView history
- Enables JavaScript, DOM storage, and file access

### WebView Configuration

- **JavaScript**: Enabled for dynamic content
- **DOM Storage**: Enabled for data persistence
- **Database**: Enabled for local storage
- **User Agent**: Set to mobile Chrome for compatibility
- **Layout Algorithm**: Single column for mobile display
- **Mixed Content**: Allowed for compatibility
- **File Access**: Enabled for download functionality

## Network Configuration

The app allows mixed HTTP/HTTPS content (Android 5.0+) for better compatibility with third-party resources on chalotrain.com.

## CI/CD Pipeline

GitHub Actions automatically:

1. **Triggers on**:
   - Every push to main branch
   - Manual workflow dispatch

2. **Steps**:
   - Checks out code
   - Sets up JDK 11
   - Makes gradlew executable
   - Builds debug APK
   - Uploads APK as artifact (30-day retention)

3. **Artifacts**:
   - APK available as "ChaloTrain-APK" for 30 days
   - Can be downloaded from GitHub Actions

## Troubleshooting

### App Won't Load ChaloTrain

- Ensure device has internet connection
- Check if INTERNET permission is granted
- Verify chalotrain.com is accessible

### WebView Shows Blank Page

- Clear app cache: Settings > Apps > ChaloTrain > Storage > Clear Cache
- Restart the app
- Check device internet connection

### Build Fails

- Ensure Android SDK 34 is installed
- Verify JDK 11 is set as default
- Run `./gradlew clean` and try again
- Check gradle.properties for correct SDK path

### APK Installation Fails

- Ensure "Unknown Sources" is enabled
- Uninstall previous version first
- Try using adb: `adb install app-debug.apk`

## Configuration

### Package Name

`com.chalotrain.app`

### App Name

ChaloTrain

### Target Website

https://chalotrain.com

### Min SDK

21 (Android 5.0)

### Target SDK

34 (Android 14)

## Security

- HTTPS enforcement for chalotrain.com
- WebView security features enabled
- File access restricted appropriately
- No hardcoded credentials or sensitive data

## License

MIT

## Support

For issues or feature requests, please create an issue in the repository.
