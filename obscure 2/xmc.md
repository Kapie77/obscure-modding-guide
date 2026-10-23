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
