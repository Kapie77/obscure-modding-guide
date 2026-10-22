# Obscure 2 — XMC File Inventory

## Map
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
