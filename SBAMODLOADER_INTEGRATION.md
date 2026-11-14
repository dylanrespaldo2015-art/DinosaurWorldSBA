# SBAModLoader integration notes — Dinosaur World

## Confirmed loader support

The official `SBAModding/SBAModLoader` README describes:
- Fusion mods: BepInEx plugins compiled as .NET 10 DLLs hooking into the game's IL2CPP code.
- Native mods: Android `.so` libraries loaded before the game runtime.
- SBA packs (`.sbapack`): containers for texture packs, asset replacements, native code and Java code.
- Super Bear Adventure 13.0.8 is listed as supported by the loader documentation checked on 2026-11-14.

The official ModRepository contribution guide says browser-listed mods are submitted as one `mods/<id>.json` entry, with a published release asset or stable HTTPS download, exact SHA-256 and size, and an audit by maintainers. Its example metadata uses kinds such as `fusion`. This is a separate browser-distribution process; it does not define the internal `.sbapack` archive layout.

## Current project state

- `index.html` is a standalone browser prototype with an island, a bear, dinosaurs and simple touch gameplay.
- The test `.sbapack` previously used with the loader only checks the manual import/listing path. It is not the playable Dinosaur World mod.
- HTML is not listed as a loadable mod type. Renaming or zipping HTML as `.sbapack` does not make it a valid game mod.
- No playable in-game Dinosaur World package has been built yet.

## Work still required for an in-game world

1. Inspect the installed loader's actual pack parser and determine the exact `.sbapack` archive structure and metadata.
2. Inspect SBA 13.0.8 IL2CPP types and identify safe APIs for creating/loading a world, registering assets, and handling entry/exit.
3. Create original island, terrain, foliage and dinosaur assets in formats supported by the game's Unity runtime.
4. Implement and compile the required Fusion plugin and/or asset pack using the loader's supported toolchain.
5. Test on the Android device and inspect loader logs; do not call the mod complete until the world loads and is playable.

## Build constraints

The loader README's documented Android build environment requires JDK 17, Android SDK platform 37/build tools, CMake 3.22.1 and NDK 28. The user currently works from an Android phone and has no PC or Unity, so a phone-only workflow must be established before promising a compiled plugin.

## References

- Loader: https://github.com/SBAModding/SBAModLoader
- Mod repository contribution guide: https://github.com/SBAModding/ModRepository/blob/main/CONTRIBUTING.md
- Mod metadata example: https://github.com/SBAModding/ModRepository/blob/main/examples/example-mod.json
