# SBAModLoader integration notes — Dinosaur World

## What the official loader documents

The official `SBAModding/SBAModLoader` README describes three mod delivery types:

- Fusion mods: BepInEx plugins compiled as .NET 10 DLLs, using hooks into the game's IL2CPP code.
- Native mods: Android `.so` libraries loaded before the game runtime.
- SBA packs: `.sbapack` files that can bundle texture packs, asset replacements, native code and Java code.

The official loader README lists Super Bear Adventure 13.0.8 as a supported game version (at the time of the documentation checked).

## What this means for this project

The current `index.html` is a standalone browser prototype. It is useful for testing the island layout and basic gameplay idea, but SBAModLoader does not list HTML as a loadable mod type. Renaming or zipping the HTML as `.sbapack` would not make it a valid game mod.

A genuinely new playable world likely needs game-side integration through a Fusion/BepInEx plugin and/or assets packaged in the loader's supported SBA pack format. The exact pack manifest/layout and the game's scene-loading APIs must be confirmed from the loader implementation and the target game build before generating a package.

## Required technical work before a real in-game build

1. Inspect the exact SBAModLoader version installed on the Android device and its supported pack structure.
2. Identify the Unity/IL2CPP scene and asset-loading APIs available in SBA 13.0.8.
3. Build or adapt original island, terrain, foliage and dinosaur assets for the game's runtime.
4. Implement a plugin that registers/loads the new world and its entry/exit logic.
5. Package the plugin/assets in the correct format, test on the device, and inspect loader logs for failures.

## Current status

- [x] Browser prototype committed to this repository.
- [x] GitHub Pages deployment workflow committed.
- [ ] Verify Pages deployment succeeds.
- [ ] Confirm exact `.sbapack` structure from the installed loader source.
- [ ] Confirm game-side scene-loading approach for SBA 13.0.8.
- [ ] Build and test an actual in-game mod.

## Official references

- Loader: https://github.com/SBAModding/SBAModLoader
- Mod repository contribution guide: https://github.com/SBAModding/ModRepository/blob/main/CONTRIBUTING.md

This document deliberately does not claim that a playable in-game mod has been built.
