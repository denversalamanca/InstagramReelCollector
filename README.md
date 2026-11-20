# Instagram Reel Link Collector (Android)

Android Studio Java project. The app opens Instagram's mobile website in Android WebView and saves **Reel URL navigation** detected by `doUpdateVisitedHistory`, `onPageFinished`, and periodic `WebView.getUrl()` checks. Link capture occurs **only when a reel URL appears as the browser URL**; a scroll that leaves the URL unchanged is not detectable by this implementation. No claim is made that all watched/scrolled Reels can be captured.

## Build to APK
1. Install Android Studio with SDK 35 and JDK 17.
2. Open this extracted `InstagramReelCollector` folder as a project; let Gradle sync/download Android Gradle Plugin 8.7.3.
3. Build > Build Bundle(s) / APK(s) > Build APK(s).
4. Find the APK at `app/build/outputs/apk/debug/app-debug.apk`.
5. Install the APK on Android. If Android warns about unknown sources, only install if you trust the project you built.

## Features
- Instagram mobile website in WebView; Instagram login may be blocked by Instagram.
- Best-effort automatic URL collection of /reel/shortcode/ pages, no background network scraping.
- Duplicate removal and on-device persistent storage.
- Copy All, export TXT using system file picker, delete confirmation.
- Handle Instagram Share -> Reel Link Collector as a reliable fallback (when Instagram allows sharing a link).
- No server, no credentials harvested, no cookies exported.

## Limitations
Instagram can block embedded logins and change its URL behavior. The app does NOT identify every visible reel from scrolling, and collecting links in bulk may be restricted by Instagram's terms. No APK is bundled because the build environment here has no Android SDK or Gradle distribution.

## Build APK for free with GitHub Actions (no Android Studio)
1. Make a new GitHub repository (for example, `InstagramReelCollector`).
2. Upload **the contents of this `InstagramReelCollector` folder** to the repository root (including the hidden `.github/workflows/build-apk.yml` file). You can upload the contents through GitHub's browser upload, or push using git.
3. Open **Actions** > **Build Android APK** > **Run workflow** (or the workflow runs automatically on a push to main/master).
4. Once it finishes successfully, click the workflow run and download **InstagramReelCollector-debug-APK** under **Artifacts**. Unzip the downloaded artifact to find `app-debug.apk`.
5. Install only APKs you built/trust. GitHub may require enabling Actions. This debug APK is for personal testing; it is not a Play Store signed release.

Note: The workflow and the app have not been built/tested in this environment. Instagram may refuse WebView login and not every scrolling Reel URL is detectable.
