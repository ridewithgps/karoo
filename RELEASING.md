# Releasing

Each release here is a build of the Ride with GPS Android app that has already shipped through Google Play, so the Karoo and Play builds are signed with the same key and riders can update from one to the other.

1. In Play Console, open **App bundle explorer**, pick the release and download the **Signed, universal APK**.
2. In RWGPS-Android, run `tools/karoo/karoo_release.py --apk <universal.apk> --notes "<what's new>"`. It writes `manifest.json`, `ridewithgps.apk`, `icon.png` and `README.md` to `build/karoo-release/` and prints the `gh release create` command.
3. Check that the signer SHA-256 it prints matches the previous release. A different key means riders can't update.
4. Run the printed `gh release create` command against this repo.

The app reads `https://github.com/ridewithgps/karoo/releases/latest/download/manifest.json` (set in `full_client/src/main/res/values/karoo.xml`). The Karoo shows **Update** when that manifest's `latestVersionCode` is newer than the installed app, so mark only stable releases as latest, and never publish a pre-release as latest.

The download URLs only work while this repository is public.
