# PhysX JNI for iOS (arm64)

Build scripts that compile [physx-jni](https://github.com/fabmax/physx-jni)
**v2.2.2** into `libPhysXJniBindings_64.dylib` for iOS (arm64).
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
5. Wait about 5-10 minutes for the build to finish.
6. Open the **Artifacts** tab and download `libPhysXJniBindings_64.dylib`.
7. Open `symbol_check.txt`. It must say `SYMBOL_OK`.

### Required version

This build targets Minecraft has Physics Mod uses physx-jni **2.2.2**. In `codemagic.yaml`, keep `PHYSX_JNI_REF: "2.2.2"`.

If you use another Minecraft or mod version, `PHYSX_JNI_REF` must match the
physx-jni version bundled in your mod's `.jar`. A wrong version produces a
dylib that does not work.

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

This repo only contains build scripts. The build downloads and compiles:

| Project | Author | License |
|---|---|---|
| [physx-jni](https://github.com/fabmax/physx-jni) | fabmax | MIT |
| [NVIDIA PhysX](https://github.com/NVIDIA-Omniverse/PhysX) (via fabmax's fork) | NVIDIA | BSD-3-Clause (NVIDIA has announced a move to Apache-2.0 in future releases) |

If you redistribute a built `.dylib`, include the copyright notices and
license texts of both projects. They are in the `LICENSE` files of the
cloned repos. Neither license allows using NVIDIA's name to promote your
product.

The scripts in this repo are provided as-is. Add your own license
(for example MIT) if you want others to reuse them.
