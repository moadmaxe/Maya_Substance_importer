# Maya Substance Importer
### Substance Painter → Arnold (aiStandardSurface) texture importer for Maya

**By [EL MENDILI Mouad](https://github.com/moadmaxe)**  
[![ko-fi](https://img.shields.io/badge/Support%20me%20on-Ko--fi-FF5E5B?logo=ko-fi&logoColor=white)](https://ko-fi.com/elmendili)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

---

## What it does

A single Python script that scans your Substance Painter texture export folder and automatically creates, connects, and assigns Arnold `aiStandardSurface` shaders to your selected objects in Maya — in one click.

No manual shader naming. No renaming your textures. No configuration files. Just point it at your folder and run.

---

## Features

- **Zero setup** — paste the script into Maya's Script Editor and run. That's it.
- **Automatic material matching** — reads the existing material names from your scene and matches them to texture sets by name. Works even if your textures have a prefix like `BUZZ_3_graaaays_BaseColor...`
- **ACES & sRGB support** — queries Maya's actual color management config at runtime and sets the correct color space for every texture node automatically. Works with ACES, sRGB, and any custom config.
- **Smart UDIM detection** — automatically detects whether textures are a real UDIM sequence (multiple tiles) or a single-tile file. No false UDIM assignments.
- **Multi-material objects** — correctly handles objects with per-face material assignments. All face assignments are preserved.
- **All map types supported** — Base Color, Metallic, Roughness, Normal, Height, AO, Emissive, Opacity.
- **Arnold-native normal maps** — uses `aiNormalMap` node by default, with `bump2d` as a fallback.
- **Advanced options** for power users (all optional, hidden by default):
  - Choose which maps to connect
  - Switch normal map method (aiNormalMap / bump2d)
  - Adjust height bump depth and emission multiplier
  - Set a texture prefix to strip during matching
  - Re-connect existing shaders after re-exporting from Substance

---

## Requirements

- Maya 2020 or later
- Arnold (MtoA) plugin loaded
- Textures exported from Substance Painter with standard naming

---

## Installation

No installation needed. Two options:

**Option A — Run once:**
1. Open Maya's Script Editor (`Windows → General Editors → Script Editor`)
2. Create a new Python tab
3. Paste the entire contents of `substance_importer.py`
4. Press the Run button

**Option B — Shelf button (recommended):**
1. Save `substance_importer.py` somewhere on your computer (e.g. `Documents/maya/scripts/`)
2. Add this to a shelf button:
```python
import substance_importer
substance_importer.run()
```

---

## How to use

1. Export your textures from Substance Painter as usual
2. In Maya, select all the objects you want to apply textures to
3. Run the script — the UI window opens
4. Click **Browse** and navigate to your texture export folder
5. Click **Apply to Selected Objects**

The script will scan the folder, match each object's material name to the correct texture set, create `aiStandardSurface` shaders, connect all maps with correct color spaces, and assign them — all automatically.

---

## Texture naming

The script works with Substance Painter's default export naming:

```
ProjectName_MaterialName_BaseColor.1001.tif
ProjectName_MaterialName_Roughness_Utility - Raw.1001.tif
ProjectName_MaterialName_Normal_Utility - Raw.1001.tif
```

If your textures have a project prefix (e.g. `BUZZ_3_`) that isn't part of the material name in Maya, enter it in the **Prefix** field under Advanced Options and the matching will work correctly.

---

## Re-exporting textures

If you make changes in Substance and re-export, you don't need to redo everything. Just:
1. Open the script, select your objects, browse to the folder
2. Expand **Advanced Options**
3. Tick **Re-connect existing shaders**
4. Click Apply

This refreshes the texture paths without deleting or reassigning anything.

---

## License

MIT License — free to use, modify, and distribute. Credit appreciated but not required.

---

## Support

If this saved you time, consider buying me a coffee ☕  
👉 [ko-fi.com/elmendili](https://ko-fi.com/elmendili)
