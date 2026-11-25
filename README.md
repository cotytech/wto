# WriteToOpen
===========

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

Permissions
-----------
- QUERY_ALL_PACKAGES: Required on Android 11+ so the app can look up the names of installed launchable apps when you search for them. No internet permission is requested or used.

An app launcher, where you type instead of clicking. 
