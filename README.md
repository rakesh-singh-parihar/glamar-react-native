# Glam React Native App

## Overview

This is a React Native application that integrates a WebView to load the GlamAR SDK. The WebView requests camera permissions and interacts with the SDK for skin analysis and other AR-based functionalities.

## Features

- Loads GlamAR SDK inside a WebView
- Requests camera permissions on Android
- Handles WebView messages to track events
- Sends initialization data to the SDK

## Project Structure

```
root
├── App.js  # Main entry point of the app
├── WebViewScreen.js  # WebView component handling SDK interactions
├── android/
│   ├── app/
│   │   ├── src/
│   │   │   ├── main/
│   │   │   │   ├── java/com/glam/MainActivity.java  # Handles WebView permissions
│   │   │   │   ├── AndroidManifest.xml  # Permissions configuration
│   ├── local.properties  # Android SDK path configuration
├── package.json
└── README.md
```

## Setup and Installation

### Prerequisites

- Node.js
- React Native CLI
- Android Studio (for Android development)

### Installation Steps

1. Install dependencies:
   ```sh
   npm install
   ```
2. Configure the Android SDK path:
   - Open `android/local.properties`
   - Replace the username in the following line with your own:
     ```
     sdk.dir = /users/YOUR_USERNAME/library/android/sdk
     ```
3. Ensure required permissions are added in `AndroidManifest.xml`:
   ```xml
   <uses-permission android:name="android.permission.CAMERA"/>
   <uses-feature android:name="android.hardware.camera" android:required="true"/>
   ```
4. Start the Metro bundler:
   ```sh
   npx react-native start
   ```
5. Build and run the app on Android:
   ```sh
   npx react-native run-android
   ```

## WebView Integration

The WebView loads the GlamAR SDK and communicates via `window.postMessage`. The SDK events are handled in `onMessage`.

### Camera Permission Handling

- On Android, camera permission is requested using `PermissionsAndroid`.
- In `MainActivity.java`, `onPermissionRequest` grants camera access for WebView.

### Initialization Payload

When the WebView loads, the following payload is sent to initialize the SDK:

```json
{
  "type": "initialize",
  "payload": {
    "apiKey": "YOUR_API_KEY",
    "platform": "react_native",
    "category": "skinanalysis",
    "openLiveOnInit": true,
    "skinAnalysis": {
      "version": "GlamGen",
      "defaultFilter": true,
      "startScreen": true
    }
  }
}
```

## Troubleshooting

### WebView Not Loading

- Ensure the device has an active internet connection.
- Check if the SDK URL (`https://www.glamar.io/sdk`) is accessible.

### Camera Permission Issues

- Verify that camera permission is granted in Android settings.
- Ensure `onPermissionRequest` in `MainActivity.java` correctly grants camera permissions.

### WebView Communication Not Working

- Use `console.log(event.nativeEvent.data)` inside `handleMessage` to debug messages received from the WebView.

## Contributors

- **Your Name** (Project Maintainer)

## License

This project is licensed under [Your License].
