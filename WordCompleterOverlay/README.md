# Word Completer - Overlay (Android)

A native Android port of the Suggestion Mode script: a floating settings
panel plus a floating "suggested word" box (`SYSTEM_ALERT_WINDOW` /
"draw over other apps" permission), so it works as its own app instead of
needing a Roblox executor. No key tracking, no automatic typing — you
still type the suggested word manually in the game.

## Important: this project is NOT a built APK

I don't have an Android SDK, Gradle, or network access in this chat
environment, so I could not compile, run, or sign this project — only
write the source.

### Option A — Build it online with GitHub Actions (no installs at all)

A workflow file is already included at
`.github/workflows/build.yml`. It builds the APK entirely on GitHub's
servers and gives you a download link, using only a web browser:

1. Create a free account at github.com if you don't have one.
2. Create a new repository (any name, Public or Private).
3. Open it, click **Add file → Upload files**, then drag in the whole
   `WordCompleterOverlay` folder (or all its files/subfolders) and
   commit. GitHub's uploader accepts folders dropped into the browser.
4. Go to the **Actions** tab of the repository. A run called
   "Build APK" should start automatically (if not, click it and then
   **Run workflow**).
5. Wait for it to finish (a few minutes, shown with a green check).
6. Open that run, scroll to **Artifacts**, and download
   `word-completer-overlay-debug-apk` — it's a zip containing
   `app-debug.apk`.
7. Transfer `app-debug.apk` to your phone and install it (enable
   "install unknown apps" for whichever app you use to open the file).

This produces a debug build, which Android signs automatically with a
built-in debug key — fine for installing on your own phone, not meant
for the Play Store. Because the workflow hasn't actually been run, a
step might need a small tweak if GitHub changes one of those actions;
the Actions log will show exactly which step failed.

### Option B — Android Studio (local)

1. Android Studio → **Open** → select the `WordCompleterOverlay` folder.
2. Let Gradle sync (downloads the Android Gradle Plugin and Kotlin
   plugin the first time — needs internet).
3. **Build → Build Bundle(s) / APK(s) → Build APK(s)**, or just press
   the Run button with a phone/emulator connected.
4. The built APK is under `app/build/outputs/apk/debug/app-debug.apk`.

Because none of this was compiled here, there may be small Kotlin/XML
issues that need a fix (a missing import, a renamed API, etc.) — the
logic itself mirrors the Lua script closely.

## Using the app

1. Open the app, tap **Grant overlay permission**, allow it in the
   system settings screen that opens, then go back to the app.
2. Tap **Start Word Completer**. The settings panel and a small
   "Restore settings" button appear floating on top of everything,
   including Roblox.
3. Switch to Roblox. Type a Prefix, optionally a Suffix / exclude
   ending / minimum length, and press **ENTER** (or the Enter/Go key
   on the on-screen keyboard) to get a suggestion. **Next Variant**
   works the same way as in the Lua version.
4. Type the suggested word into the game yourself.

The word list and the remote on/off switch are fetched from the same
GitHub URLs as the other two versions.

## Known limitations

- Android may kill background services after a while on some phones
  (MIUI, battery optimizers, etc.). If the overlay disappears, reopen
  the app and tap Start again, and consider excluding the app from
  battery optimization in your phone's settings.
- This hasn't been tested on a real device or emulator from this
  environment — please report anything that doesn't work.
