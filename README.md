# Garden Guard: Android APK

## Option A: no installs, build in the cloud (easiest)
1. Create a new GitHub repository and upload everything in this folder (keep the .github folder).
2. Open the repo's Actions tab and run "Build Android APK" (it also runs on every push to main).
3. When it finishes (about 5 minutes), open the run and download the artifact "garden-guard-apk". Unzip it to get app-debug.apk.
4. Copy the APK to your phone, tap it, and allow "install unknown apps" when asked.

## Option B: build on your computer
Needs Node 20+, JDK 17 and Android Studio (or the Android SDK command-line tools).
    npm install
    npx cap add android
    npx cap sync android
    cd android && ./gradlew assembleDebug
The APK is at android/app/build/outputs/apk/debug/app-debug.apk
(or run "npx cap open android" and press Run in Android Studio).

## Updating the game
Replace www/index.html with the new version, then run "npx cap sync android" and rebuild (or push to GitHub for Option A).

## Before publishing on Google Play
- Change appId in capacitor.config.json (it is com.example.gardenguard now) before your first release.
- Debug APKs are for testing. Play Store needs a signed release build (AAB): run "./gradlew bundleRelease" and sign it with your own keystore.
- Add your own icon and splash screen with: npm i -D @capacitor/assets, then put icon.png (1024x1024) in an assets folder and run npx capacitor-assets generate --android
