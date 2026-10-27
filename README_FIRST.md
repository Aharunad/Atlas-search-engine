# ATLAS Futurica Android integration project (starter)

This is the Android Studio source project for the preferred emoji-checkbox ATLAS Futurica interface, bundled with the original ATLAS APF Python engine source/data and a Chaquopy bridge. It is **not yet a compiled APK**.

## What is included
- The preferred HTML interface in `app/src/main/assets/index.html`.
- Original APF core and bundled `engine/` and `data/` files under `app/src/main/python/atlas_engine/app/`.
- Android WebView host and JavaScript bridge.
- Python bridge calling `any_planet_finder_core.find_planets` locally, with a background scan loop, pause/resume, stop, extend-range and search-until-target controls.
- Gradle project configuration using Android Gradle Plugin and Chaquopy.

## Build prerequisites
1. Install Android Studio with Android SDK Platform 35 and Build Tools.
2. Install a compatible JDK (17 recommended) and Python 3.11 for Chaquopy's build configuration.
3. Open this folder in Android Studio and allow Gradle to sync/download its declared plugins. Internet access is needed for the first dependency sync.
4. Build via **Build > Build APK(s)** or run `./gradlew assembleDebug` if a Gradle wrapper is installed locally. This starter does not include a Gradle wrapper JAR.

## Important current integration boundaries
- No APK was built or installed in this environment: Android SDK/Gradle are not installed here.
- The bridge currently maps the portal, galaxy, system/batch limits, target count, and a small initial set of filters. It does **not** yet map every checkbox, colour swatch, terrain selection, and advanced filter to exact core arguments.
- When multiple terrain families are selected, the initial adapter currently passes only the first selected family. The planned correct implementation is a validated multi-pass/merge adapter.
- The engine's `find_planets` returns actual records, but result cards are presently generic field/value cards. Polished planet telemetry cards need a schema mapping pass.
- Engine modules use bundled reference data and dynamically load sibling Python modules; these paths are preserved. Android runtime validation is still required, especially for dynamic imports and any native/multiprocessing-dependent path. The adapter requests one worker to avoid multiprocessing pools.
- Do not treat the HTML opened directly in a browser as a working engine. The JavaScript bridge is available only inside the Android host app.

## Validation checklist before release
- Confirm Chaquopy packages the entire engine/data tree and all dynamic module paths resolve on device.
- Test known portal/gala​xy cases against the desktop core.
- Verify batch boundaries, progress counts, cancellation, pause/resume, extension after limit, and stop-until-found behavior.
- Wire and test every visible filter, especially multiple terrain-family selections and colour matching.
- Run on a real ARM64 Android device; record memory, battery, and long-search stability.
- Add app icon, attribution, versioning, signed release configuration, and a golden test corpus before distribution.
