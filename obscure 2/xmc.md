# Obscure 2 — XMC File Inventory

## Tree
```text
cachpack.hvp
└── assets
    ├── digicode
    │   ├── 01.xmc
    │   ├── c103.xmc
    │   ├── e004.xmc
    │   └── e100.xmc
    ├── hacking
    │   └── words.xmc
    ├── lockpick
    │   ├── 01.xmc
    │   ├── 02.xmc
    │   ├── 03.xmc
    │   ├── 04.xmc
    │   ├── 05.xmc
    │   ├── 06.xmc
    │   ├── 07.xmc
    │   └── 08.xmc
    └── puzzle
        ├── e100.xmc
        ├── g005.xmc
        ├── hospital.xmc
        └── library.xmc

datapack.hvp
├── characters
│   ├── cbox.xmc
│   └── combos.xmc
├── menus
│   ├── debug
│   ├── font_arial14b.xmc
│   ├── font_mkabel12.xmc
│   ├── font_nonserif12.xmc
│   ├── font_smallfonts7
│   ├── inv_live.xmc
│   ├── inventory_pc.xmc
│   ├── mc.xmc
│   ├── menu_pc.xmc
│   ├── pause_pc
│   └── save.xmc
├── projects
│   ├── chapters.xmc
│   ├── edit_menu.xmc
│   ├── edit_menu2.xmc
│   ├── fx.xmc
│   ├── game.xmc
│   └── vibrations.xmc
└── sounds
    ├── soundfx.xmc
    └── streams.xmc
```

## Inventary

| File | Known location / context | Status | Summary |
|---|---|---|---|
| [`game.xmc`](xmc/game_xmc.md) | Extracted to `game.xml` for inspection | **Analyzed** | Appears to contain game configuration and resource references, including character/state settings, item and weapon metadata, save-point identifiers, chest contents, cinematic entries, animation files, and resource directories. |
| [`chapters.xmc`](xmc/chapters_xmc.md) | Extracted to `chapters.xml` for inspection | **Analyzed** | Contains chapter configuration entries, including chapter and level identifiers, character assignments, character-specific level and position references, controller settings, life values, chest configuration, and item availability with associated attributes across multiple chapter configurations. |
| [`edit_menu.xmc`](xmc/edit_menu_xmc.md) | Extracted to `edit_menu.xml` for inspection | **Analyzed** | Defines a debug-oriented menu with seven sections covering display diagnostics, gameplay cheats, chapter selection, debugging controls, string operations, language selection, and memory-card utilities. Contains 45 menu entries identified by action codes, with numeric values specifying Chapters 2–12. |
| [`edit_menu2.xmc`](xmc/edit_menu2_xmc.md) | Extracted to `edit_menu2.xml` for inspection | **Analyzed** | Defines a compact debug menu with three sections covering debug options, chapter selection, and memory-card utilities. Contains 14 menu entries, including infinite ammunition, debug information display, Chapters 2–12, and copying debug data to the current version. |
| [`fx.xmc`](xmc/fx_xmc.md) | Extracted to `fx.xml` for inspection | **Analyzed** | Defines visual effects and particle-system configurations, including bloom, electricity, water, shadows, environmental effects, character impacts, weapon effects, and explosions. Contains rendering parameters, texture references, color definitions, grouped effect types, and numerous references to external `.txt` particle definitions. |
| [`vibrations.xmc`](xmc/vibrations_xmc.md) | Extracted to `vibrations.xml` for inspection | **Analyzed** | Defines vibration parameters associated with animation identifiers, including left/right intensity values, start offsets, durations, and priorities. Separates common vibration entries from character-specific configurations for `BOY1` and `BOY4`. |
| [`streams.xmc`](xmc/streams_xmc.md) | Extracted to `streams.xml` for inspection | **Analyzed** | Catalogs 299 audio stream entries with numeric IDs, descriptive names, optional volume values, and references to beginning and looping audio files. Covers menu music, ambient sounds, chapter-specific audio, character events, and cinematic sequences. |
| [`font_arial14b.xmc`](xmc/font_arial14b_xmc.md) | Extracted to `font_arial14b.xml` and compared with `font_arial14b.tga` | **Analyzed** | Defines a proportional bitmap font named Arial, with letters, digits, punctuation, accented characters, and symbols mapped to texture coordinates. The XML declares a 256×128 texture, but its final glyph row extends beyond the supplied TGA's bounds, indicating an unresolved resource mismatch. |
| [`font_mkabel12.xmc`](xmc/font_mkabel12_xmc.md) | Extracted to `font_mkabel12.xml` for inspection | **Analyzed** | Defines a compact bitmap font containing digits 0–9, a slash, and a hyphen. Specifies a 128×32 texture with 17-pixel-high glyphs of varying widths. The glyph coordinates fit within the declared texture bounds; visual verification against the associated texture is pending. |
| [`font_nonserif12.xmc`](xmc/font_nonserif12_xmc.md) | Extracted to `font_nonserif12.xml` for inspection | **Analyzed** | Defines a variable-width bitmap font with uppercase and lowercase Latin letters, digits, punctuation, accented characters, and additional symbols. Specifies a 512×256 texture with 141 character entries. Several character attributes are empty or contain replacement characters, and visual verification against the associated texture is pending. |
| [`debug.xmc`](xmc/debug_xmc.md) | Extracted to `debug.xml` for inspection | **Analyzed** | Defines a debug menu system with 25 panels and 256 entries, covering direct level loading across 13 location/test groups, chapter selection, one- or two-player character assignment, item toggles, and weapon configuration. Includes 133 direct level-loading entries, eight playable character options, and four weapon slots with 15 selectable weapon codes each. |
| [`inv_live.xmc`](xmc/inv_live_xmc.md) | Extracted to `inv_live.xml` for inspection | **Analyzed** | Defines live inventory and HUD elements, including two weapon inventory panels with different color schemes, a six-position item indicator group, and an energy display assembled from four sprites referencing the `hud_nrj` texture. Also contains 22 input mappings for navigation, selection, confirmation, and cancellation, divided between two input contexts (`param="0"` and `param="1"`). |
| [`inventory_pc.xmc`](xmc/inventory_pc_xmc.md) | Extracted to `inventory_pc.xml` for inspection | **Analyzed** | Defines the main inventory interface, including weapon selection, item and clue browsing, team selection, document display, and message-box presentation. Contains 15 explicit weapon codes in a 16-position grid, 20 clue IDs with texture-atlas coordinates, nine team entries (eight mapped character IDs plus one `prof` entry without a `chara_id`), and 35 input mappings across three offset contexts. |
| [`mc.xmc`](xmc/mc_xmc.md) | Extracted to `mc.xml` for inspection | **Analyzed** | Defines a small memory-card-related interface with a main `check_mc` panel and a message box using the `mb` class. Includes one border sprite, two input contexts, and seven input mappings for navigation, confirmation, and cancellation. The exact memory-card operation and displayed message are not specified in the XML. |
| [`menu_pc.xmc`](xmc/menu_pc_xmc.md) | Extracted to `menu_pc.xml` for inspection | **Analyzed** | Defines the PC main-menu system, including Steam and non-Steam root menu variants, new-game transitions, load/save and exit panels, brightness and video settings, and controller/input configuration. Contains 25 menu definitions (24 distinct IDs), 109 visual/menu items, 69 actions, two input offsets, and 11 input mappings, with a separate debug-menu resource reference. |
