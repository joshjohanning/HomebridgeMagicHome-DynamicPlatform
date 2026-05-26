# Changelog

All notable changes to this project will be documented in this file.

## [2.0.2] - 2026-05-26

### Bug Fixes

- Reverted plugin identifier in `registerPlatform()` and `PLUGIN_NAME` back to the unscoped `homebridge-magichome-dynamic-platform` to preserve compatibility with accessories cached under the original upstream plugin identifier.
- Added explicit `npm run build` step to the publish workflow. Previous releases (`2.0.0`, `2.0.1`) shipped without a `dist/` folder because `npm pack` does not trigger the `prepublishOnly` script, so the plugin could not be loaded by Homebridge.

## [2.0.1] - 2026-05-26

### Bug Fixes

- Attempted (incorrectly) to change plugin registration name to match scoped package name. Superseded by 2.0.2. Also did not ship `dist/`.

## [2.0.0] - 2026-05-26

### Initial Release

Fork of [Zacknetic/HomebridgeMagicHome-DynamicPlatform](https://github.com/Zacknetic/HomebridgeMagicHome-DynamicPlatform) with the following changes:

- Renamed package to `@joshjohanning/homebridge-magichome-dynamic-platform`
- Updated Node.js engine requirement to `^22.12.0 || ^24.0.0`
- Updated Homebridge engine requirement to `^1.6.0 || ^2.0.0` (Homebridge v2 compatible)
- Upgraded TypeScript from `3.9` to `5.x`
- Added `skipLibCheck: true` to tsconfig to support Homebridge v2 matter type declarations
- Fixed firmware version comparison type error (`string | number` narrowed via `Number()`)
- Updated repository, bugs, and homepage URLs to fork
- Added funding metadata
- Added CI and publish workflows for automated testing and package publishing
- Added migration guide and installation instructions to README
