# Running it as a real Android app

The whole app is one HTML file, so a WebView wrapper is all you need. No server, no internet.

1. Android Studio, New Project, **Empty Views Activity**, language Kotlin, package `com.calvin.taper`.
2. Right click `app/src/main` → New → Directory → name it `assets`.
3. Copy `index.html`, `manifest.webmanifest`, `sw.js`, `icon-192.png`, `icon-512.png` into that `assets` folder.
4. Replace `MainActivity.kt` with the file next to this readme.
5. In `AndroidManifest.xml`, inside the `<application>` tag, add `android:hardwareAccelerated="true"`. You do **not** need the INTERNET permission, everything is local.
6. Run on your phone, or Build → Generate Signed Bundle / APK → APK, then install the APK on your device.

Progress is stored in the WebView's localStorage, so it survives closing the app. It is wiped if you clear the app's data or uninstall, so use Settings → "Copy my data as backup" occasionally.

If you want an app icon, right click `res` → New → Image Asset and point it at `icon-512.png`.
