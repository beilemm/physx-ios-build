# PhysX JNI for iOS (arm64)

Build scripts that compile [physx-jni](https://github.com/fabmax/physx-jni)
**v2.5.1** into `libPhysXJniBindings_64.dylib` for iOS (arm64).
The build runs on [Codemagic](https://codemagic.io), so no Mac is required.

## What this is

- Only the native PhysX JNI library for iOS.
- It does **not** contain Physics Mod or any of its files.
- CUDA and GPU particle bindings are removed automatically during the build
  (iOS has no CUDA). Rigid bodies, joints, raycasts, vehicles and character
  controllers remain.

## Build guide (no Mac required)

1. **Fork this repo** to your own GitHub account (Fork button, top right).
2. Go to https://codemagic.io and sign in with GitHub (free).
3. Click **Add application**, pick your fork, and choose **Other** as the
   project type (it uses `codemagic.yaml`).
4. Click **Start new build** (not "Rebuild"), select the `main` branch and the
   **PhysX JNI iOS** workflow.
5. Wait about 30-60 minutes for the build to finish.
6. Open the **Artifacts** tab and download `libPhysXJniBindings_64.dylib`.
7. Open `symbol_check.txt`. It must say `SYMBOL_OK`.

### Pick the right version

In `codemagic.yaml`, the line `PHYSX_JNI_REF: "2.5.1"` must match the
physx-jni version your mod uses. A wrong version produces a dylib that does
not work. Only 2.5.1 has been tested; other versions are untested.

### If the build fails

Open an Issue and attach `strip.log` and the `errors_N.txt` file with the
highest N from the Artifacts.

## Usage

Put the dylib where your Java launcher loads native libraries.
Get Physics Mod yourself from the author's official page:
https://www.patreon.com/Haubna. It is not included in this repo.

## Notes

- Codemagic's free plan has a monthly build-minute limit.
- Do not commit mod `.jar` files or anything extracted from them to this repo.

## Disclaimer

Not affiliated with or endorsed by Haubna, Physics Mod, NVIDIA, Mojang or
Microsoft. Use at your own risk.

## Credits and licenses

- [physx-jni](https://github.com/fabmax/physx-jni) by fabmax
- [NVIDIA PhysX](https://github.com/NVIDIA-Omniverse/PhysX)
- Check each project's `LICENSE` before redistributing any build output.
