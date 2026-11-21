# Urmux

**Urmux** is an Android terminal emulator and Linux environment based on the open-source [Termux application](https://github.com/termux/termux-app).

This fork keeps the upstream terminal engine and package environment while developing the Urmux app identity, interface, and build workflow.

## Project status

- Android application based on the Termux codebase.
- Current application ID remains `com.termux` to stay compatible with the upstream bootstrap binaries and shared data path.
- Android 7+ package variant: `apt-android-7`.
- GitHub Actions builds a **Universal APK only**. No Android App Bundle (AAB) is produced.
- The launcher icon uses a dark navy background and the Urmux terminal mark.
- Android 12+ devices display an animated Urmux splash icon.

## Build a Universal APK

Requirements: JDK 17, Android SDK, and Android NDK versions configured by this repository.

```bash
TERMUX_PACKAGE_VARIANT=apt-android-7 \
TERMUX_SPLIT_APKS_FOR_DEBUG_BUILDS=0 \
./gradlew --no-daemon assembleDebug
```

The GitHub Actions workflow named **Urmux Universal APK** builds the debug APK and uploads it as a workflow artifact. Open the repository's Actions tab, select a successful run, and download the `urmux-universal-apk` artifact.

## Bootstrap and package compatibility

The bundled Termux bootstrap binaries contain paths tied to the `com.termux` application data directory. Changing the Android application ID without rebuilding a matching bootstrap would prevent the terminal environment from installing or running correctly. A future migration to a separate Urmux package ID must therefore include a matching Urmux bootstrap build and coordinated path changes.

## Upstream project and packages

Urmux is an application fork. The Linux packages installed inside the terminal are maintained separately by the [termux/termux-packages](https://github.com/termux/termux-packages) project. Package management guidance is available in the [Termux package management wiki](https://github.com/termux/termux-packages/wiki/Package-Management).

## Contributing

Changes should preserve upstream terminal behavior unless a deliberate Urmux feature requires otherwise. Please include build/test results with pull requests.

## License

Urmux is a derivative work of the Termux application and retains the upstream GPLv3-only licensing for the covered code. See [LICENSE.md](LICENSE.md), the license files in each module, and the upstream [termux/termux-app](https://github.com/termux/termux-app) repository for details. Third-party components may have separate licenses.
