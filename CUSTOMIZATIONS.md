# Android 1.3 ambient-home variant

This branch is based on upstream Free My TV 1.3, commit `aeffdb4c4faa781069ab5713890fa0b9efebb4ee`.
It preserves upstream's features and safety checks while adapting the Android home screen.
This is an independent customization, not an official release. The original license and credits apply.
LG webOS and Samsung Tizen keep their upstream 1.3 behavior; the custom interface applies to Android.

## Customizations retained

- Nine app shortcuts visible together. Other TVs can still scroll to additional apps as upstream allows;
  low-memory TVs keep a nine-app cap. Existing shelf order and editing controls are retained.
- Recommendations stay visible while the app shelf is focused. Up and Down move focus between
  recommendations and apps without clearing the scene or resetting the selected background palette.
  The app shelf stays close to the recommendation metadata; the drawer and app-sheet transitions remain.
- Fixed dark recommendation background with soft edge colors from the selected title. Palette changes
  crossfade, and late image loads retain the selected title instead of resetting to the first one.
  This is an on-screen effect, not control of physical Ambilight LEDs.
- A screensaver submenu selects the original TV saver (Google/Chromecast Backdrop on the tested Philips)
  or Free My TV. The Preview row previews Free My TV. Selection is preserved by startup verification.
  An explicit TV selection wins; without one, upstream's `screensaver=false` setting is respected.

## Upstream 1.3 retained

Expandable recommendation cards and posters, up to six picks per tab, service filtering, Continue Watching,
Now Playing, the native personal-photo importer, TMDB key entry, Sleep Timer, manual update checks,
remote support, and upstream performance and recovery changes remain present. Clock and Continue Watching
retain their original modes; the custom reveal and fixed dark glow apply to the recommendations mode.
These features keep their original permissions, opt-in settings and device limitations.
No new cloud-gallery provider or account integration has been added.

## Safe updates

Keep `config.properties` and `freemytv.keystore` backed up privately. An in-place Android update using the
same application ID (`io.freemytv`) and signing key normally preserves app preferences, shelf order and mode state.
Do not uninstall or clear app data to work around a signature mismatch; doing so removes settings.
An official APK has a different signing identity and cannot merge these customizations into this build.

To incorporate a future upstream release, merge its code into this branch, resolve conflicts, run the
project checks and build with the same key. Increase `android:versionCode` for each distributed update.

```sh
git remote add upstream https://github.com/simbasjungles/free-my-tv.git # once
git fetch upstream
git merge upstream/main
./tools/check.sh
adb install -r FreeMyTV.apk
```

Upstream's release updater is retained unchanged. It installs official updates only in a generic build
signed with the official release key. This self-built variant can manually check for newer official
versions, but must be rebuilt to retain its modifications. It does not automatically replace itself
with the official APK or fetch updates from this fork.

## Privacy and distribution

Only source, translations and documentation are published. There are no personal photos, cloud-gallery
experiments, credentials, private configuration, signing keys or personalized APKs in this branch.
The native photo feature remains available but carries no bundled personal images.
A personalized APK may contain the locally configured TMDB key: keep it private.
Other people must use their own settings and signing key when building this source.

## Validation

The Android build and APK signature verification passed, as did all 26 translation catalogues
(362 keys), LG/Samsung package builds and the project ES5/CSS compatibility checks.
On one Philips Android TV 11, the update preserved the nine-app order and the selected Google saver.
The selected recommendation changed the background palette and expanded its card; compact spacing
and the saver selector were checked visually. Both saver choices were verified through Android's
saved setting, ending with Google/Chromecast selected. No blanket compatibility or playback-performance
improvement is claimed.
The earlier installed APK and private configuration/key backup remain outside the repository.

### Persistent recommendations (1.3-custom.2)

Recommendations now remain visible when Down moves focus to the app shelf; the selected recommendation's
palette remains unchanged. The drawer and All Apps transitions keep their existing behavior.
The Android build, signature and complete project checks passed again. The navigation change was installed
and visually tested on a second Philips Google TV running Android 14. Background sample pixels were
unchanged before and after moving from a recommendation to the apps. The original Android 11 TV was not
updated with this follow-up; its next device test remains subject to the owner's instruction.
