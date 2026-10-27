# Build ATLAS Futurica APK from GitHub (phone-friendly guide)

## Important status
This project is a starter Android integration, not yet a validated release. The workflow below compiles a **debug APK**; a successful compilation does not prove that every search filter or long-running search is correct. The Python bridge still needs engine validation and complete filter mapping before treating this as a finished app.

## Create the repository
1. Open https://github.com/new in your browser and sign in.
2. Repository name: `ATLAS-Futurica-Android`.
3. Select **Private** (recommended) and leave **Add a README** unchecked.
4. Tap **Create repository**.
5. On the new repo page choose **Add file → Upload files**. Extract this ZIP on your device first, then upload the *contents* of the folder `ATLAS_Futurica_Android_Project` (including the hidden `.github` folder). GitHub's browser uploader can be awkward on a phone; if selecting nested folders does not preserve their paths, use GitHub's web editor only for the workflow file and upload the project files with GitHub's supported upload method. Do not upload the ZIP as a single repository file.
6. Commit the uploaded files to the `main` branch.

## Start the cloud build
1. In the repository, open **Actions**.
2. Select **Build ATLAS Futurica Android APK**.
3. Tap **Run workflow**, select `main`, then run it.
4. Open the newest workflow run. Wait for its status to finish.
5. If it succeeds, find **Artifacts** at the bottom of the run page and download `ATLAS-Futurica-debug-APK`. Extract the artifact ZIP; it contains `app-debug.apk`.
6. Keep the workflow run and its logs if it fails; they show the exact dependency/build error to fix.

## Scope and safety
- This workflow builds an unsigned debug APK for testing, not a Play Store release APK.
- Do not put passwords, keystores, API keys, or other secrets in the repository.
- The repository can remain private.
- Build dependencies are downloaded by Gradle/Android SDK during the run.

## Technical caveats to fix/test after first build
- The starter requires verification of Chaquopy and all dynamic engine-module/data paths on Android.
- Not every visible UI filter is currently mapped to the original core; multiple terrain choices need an explicit OR/merge strategy.
- Verify the `find_planets` argument names against the bundled core before relying on the bridge.
- Run golden portal/galaxy test cases against the desktop core and test pause/resume, cancel, extension, and search-until-found.
- Test the APK on the target Android device before considering release.
