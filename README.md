# WriteToOpen

A minimal, no-frills Android app launcher where you type an app's name, tap OK, and open it immediately.

Features
--------
- Basic, lightweight UI with a text input and an OK button (no clutter, no icons, no app list).
- Supports pressing Go / Done / Enter on the keyboard as a shortcut for OK.
- Smart case-insensitive matching against installed launchable apps:
  1. Exact app name match (e.g., "Settings", "Chrome")
  2. Exact package name match (e.g., "com.android.settings")
  3. Starts-with match (e.g., "You" -> "YouTube")
  4. Contains match (e.g., "Maps" -> "Google Maps")
- Built with pure Android framework APIs (Java, zero external libraries) — resulting APK is ~13 KB.
- Includes QUERY_ALL_PACKAGES and launcher <queries> support so installed apps are visible on Android 11+.

How it works
------------
- Basic UI (activity_main.xml): Uses standard Theme.DeviceDefault.Light with a plain prompt label, single-line EditText, OK Button, and status TextView for error feedback.
- App Matching & Launching (MainActivity.java):
  1. Clicking OK (or pressing Go/Done/Enter on the keyboard) queries launchable apps via PackageManager.queryIntentActivities (ACTION_MAIN + CATEGORY_LAUNCHER).
  2. Matches the typed text case-insensitively in priority order: exact app label → exact package name → label starts with query → label contains query (shortest matching label).
  3.Launches the matched app's component (FLAG_ACTIVITY_NEW_TASK | FLAG_ACTIVITY_RESET_TASK_IF_NEEDED), falling back to getLaunchIntentForPackage if needed, and displays a message if no app matches or it cannot be opened.
- Android 11+ App Visibility (AndroidManifest.xml): Declares android.permission.QUERY_ALL_PACKAGES and a <queries> launcher intent filter so installed apps remain discoverable on Android 11 and newer.

Requirements
------------
- Android 7.0 (API 24) or higher

Installation
------------
1. Download `WriteToOpen.apk` from the Releases section (or build it yourself).
2. Open the `.apk` file on your Android device and allow installation from unknown sources if prompted.
3. Open WriteToOpen, type any installed app name, and tap OK.

Building from Source
--------------------
1. Clone the repository.
2. Open the project in Android Studio or run Gradle 8.12+ from the project root:
   gradle assembleDebug
3. The APK will be generated at:
   app/build/outputs/apk/debug/app-debug.apk

Verification
------------
- Built cleanly with Gradle 8.12 (assembleDebug: BUILD SUCCESSFUL, 32 actionable tasks).
- Verified APK signature (apksigner verify --verbose: Verifies, v2 scheme) and manifest metadata (aapt2 dump badging: package: name='com.example.writetoopen', minSdkVersion:'24', targetSdkVersion:'34', QUERY_ALL_PACKAGES).

Permissions
-----------
- QUERY_ALL_PACKAGES: Required on Android 11+ so the app can look up the names of installed launchable apps when you search for them. No internet permission is requested or used.

Autors
------
- cotyrobayeszz (@brvnocreations)
- Gemini 4 Hydrogen in Antigravity

