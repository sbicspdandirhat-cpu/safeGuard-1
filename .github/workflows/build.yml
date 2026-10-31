name: Build APK
on:
  workflow_dispatch:
  push:
    branches: [main]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-java@v4
        with:
          distribution: temurin
          java-version: '17'
      - uses: subosito/flutter-action@v2
        with:
          channel: stable
      - run: |
          cp lib/main.dart /tmp/main.dart
          flutter create --org com.saveguard --project-name save_guard .
          cp /tmp/main.dart lib/main.dart
          flutter pub add shared_preferences url_launcher
          sed -i 's/android:label="[^"]*"/android:label="সেভ গার্ড"/' android/app/src/main/AndroidManifest.xml
          flutter build apk --release
      - uses: actions/upload-artifact@v4
        with:
          name: save-guard-apk
          path: build/app/outputs/flutter-apk/app-release.apk
