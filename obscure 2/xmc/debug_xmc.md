# debug.xmc

## Overview

`debug.xmc` defines a multi-panel debug menu system. Its main panel provides shortcuts for starting gameplay, selecting characters, choosing chapters, configuring weapons and items, and loading individual levels. The file contains 25 `<menu>` panels and 256 `<item>` entries.

The menu definitions are declarative: each item has a displayed string and one or more actions. The XML explicitly identifies action types and parameters, but does not define the implementation of those actions.

## Main menu

The root panel is `DMAI` (`type="panel"`). It contains 18 entries:

- **Quick Launch** — changes the game state to `playing`.
- **Characters** — opens `DCHA`.
- **Chapters** — opens `DCHP`.
- **Weapons** — opens `DWEA`.
- **Items** — opens `DITE`.
- **Level shortcuts** — opens one of the location panels listed below.

The location panels are grouped under these labels:

| Menu ID | Main-menu label |
|---|---|
| `DBTA` | Batiment A - Exterieur |
| `DBTB` | Batiment B - Residence |
| `DBTC` | Batiment C - Confrerie |
| `DBTD` | Batiment D - Foret |
| `DBTE` | Batiment E - Hopital |
| `DBTF` | Batiment F - Barrage |
| `DBTG` | Batiment G - Lac |
| `DBTH` | Batiment H - Maison Jeddidiah |
| `DBTI` | Batiment I - Sous Sol Leafmore |
| `DBTJ` | Batiment J - Partie Elite Confrerie |
| `DBTK` | Batiment K - Partie Bad Trip |
| `DBTW` | Test W |
| `DBTX` | Test X |

The main panel's cancel action displays the menu identified as `main`.

## Level-selection panels

The 13 location/test panels contain 133 entries in total. Each entry uses `changeState` with `state="playing"` and a `level` parameter containing the selected level identifier. Their cancel actions return to `DMAI`.

| Menu ID | Entries | Level identifiers / displayed content |
|---|---:|---|
| `DBTA` | 3 | `a000`, `a003`, `a006` — exterior areas of the Confrerie |
| `DBTB` | 20 | `B000`, `B001`, `B003`, `B101`, `B103`–`B109`, `B118`, `B200`, `B210`, `B201`, `B202`, `B212`, `B204`, `B900`, `B901` — residence, rooms, corridors, stairs, exterior and basement |
| `DBTC` | 13 | `c000`–`c008`, `c101`–`c104` — Confrerie garden, halls, dining room, kitchen, library, laboratory and other rooms |
| `DBTD` | 4 | `d000`–`d003` — forest areas |
| `DBTE` | 17 | `e000`–`e007`, `e100`–`e107`, `e900` — hospital exterior, reception, laboratory, pharmacy, morgue, corridors, rooms and basement |
| `DBTF` | 9 | `F000`–`F008` — dam exterior, rooms, corridors, heating room, tunnels and control room |
| `DBTG` | 6 | `G000`–`G005` — dock, lake, TurtleStone island, beach/bar and trails |
| `DBTH` | 7 | `H000`–`H006` — Jeddidiah house exterior, workshop, hall, corridor, bedroom, bathroom and cellar |
| `DBTI` | 17 | `I000`–`I015`, `I100` — cave, basements, staff room, toilets, entrance, computer room, courtyard, parking, library, classrooms and Friedman office |
| `DBTJ` | 7 | `J000`–`J006` — annex garden, museum, initiation room, transition area, stadium-related areas and secret library |
| `DBTW` | 13 | `w000`–`w009`, `W010`–`W012` — test scenes, character/creature setups, respawn rooms and a door-animation test |
| `DBTK` | 4 | `k000`–`k003` — mausoleum exterior, corridors, dining room and crypt |
| `DBTX` | 13 | `x000`–`x011`, `x100` — test levels without descriptive names |

The labels and level identifiers above are taken from the XML. The file does not explain the internal content or purpose of every level beyond those labels.

## Character selection

Character selection is organized through three panels:

- `DCHA` is the character-selection hub. It links to the mode selector (`DMOD`), Character 1 (`DCH1`) and Character 2 (`DCH2`).
- `DMOD` offers **One Player** and **Two Players**. The corresponding `selectMode` actions pass `id="1"` and `id="0"`, respectively, then display `DCHA`.
- `DCH1` and `DCH2` each list the same eight named characters. Their `selectCharacter` actions distinguish the player slot through `which="1"` or `which="2"`.

| Display name | Character ID |
|---|---|
| Stan | `BOY1` |
| Corey | `BOY2` |
| Sven | `BOY3` |
| Kenny | `BOY4` |
| Shannon | `GIR1` |
| Mei | `GIR2` |
| Amy | `GIR3` |
| Jun | `GIR4` |

After selecting a character, the action sequence displays `DCHA` again. `DCH2` also contains one additional entry with an empty display string and an empty character ID; it still invokes `selectCharacter` with `which="2"`.

## Chapter selection

`DCHP` contains 13 chapter entries. Each uses `changeState` with `state="chapter"` and a `chapter` parameter:

- Chapters `1` through `6`
- Chapter `6 part 2`, represented by `6_2`
- Chapters `7` through `12`

The cancel action returns to `DMAI`.

## Item selection

`DITE` provides two entries:

- **All Items** — invokes `selectItems` with `AllItems="1"`.
- **No Items** — invokes `selectItems` with `AllItems="0"`.

Both entries then display `DMAI`. The XML does not enumerate individual items or specify quantities.

## Weapon selection

`DWEA` is the weapon-selection hub. It provides four global controls and links to four weapon-slot panels:

- **All Weapons** — `selectWeapons` with `AllWeapons="1"`.
- **No Weapon** — `selectWeapons` with `AllWeapons="0"`.
- **Use Flashlight** — `selectWeapons` with `useflashlight="1"`.
- **No Flashlight** — `selectWeapons` with `useflashlight="0"`.
- **Weapon 1** through **Weapon 4** — open `DWE1` through `DWE4`.

Each slot panel contains the same 15 weapon choices. The `selectWeapons` action passes the weapon code and a slot index: `0` for `DWE1`, `1` for `DWE2`, `2` for `DWE3`, and `3` for `DWE4`. After the selection, the panel returns to `DWEA`.

| Display name in XML | Weapon code |
|---|---|
| Cross | `CROS` |
| Batte cloutée | `UBET` |
| Beat | `BEAT` |
| Chain Saw | `CSAW` |
| Shotgun | `SHOT` |
| Crossbow | `CBOW` |
| Taser | `TASE` |
| Gun | `GUN` |
| Dynamite | `DYNA` |
| Flare Gun | `FLGU` |
| Flashbang | `FLBG` |
| Uzi | `UZI` |
| Uber Flashlight | `UBFL` |
| Flashball | `FLBA` |
| Club | `CLUB` |

The weapon names and codes are reproduced from the XML. The file does not specify ammunition, damage, availability conditions, or other weapon properties.

## Structure and behavior

The file uses the following action types:

| Action type | Observed use |
|---|---|
| `show` | Opens another menu panel. |
| `changeState` | Starts gameplay at a selected level, starts normal gameplay through Quick Launch, or changes to a chapter-selection state. |
| `selectMode` | Sets the mode using an `id` parameter. |
| `selectCharacter` | Selects a character ID for the player slot specified by `which`. |
| `selectItems` | Enables or disables the `AllItems` option. |
| `selectWeapons` | Sets global weapon options or assigns a weapon code to a slot index. |

Most submenu cancel actions return to `DMAI`; the character submenus return to `DCHA`, while the main panel's cancel action returns to `main`.

## Observations and unresolved points

- The file is primarily a debug navigation and setup interface, rather than a database of character, item, weapon or level properties.
- The 13 location/test panels expose 133 direct level-selection entries.
- The four weapon-slot panels repeat the same 15 weapon codes, changing only the slot index.
- The `DCH2` panel contains an extra blank character entry with an empty ID.
- The XML uses inconsistent capitalization for some level identifiers, such as lowercase `w000`–`w009` and uppercase `W010`–`W012`. The values are preserved exactly as written.
- Several French strings contain replacement characters (`�`) in the extracted XML, suggesting text-encoding or source-data issues. The original intended characters cannot always be recovered from this file alone.
- The file does not define the code behind the action handlers, nor does it establish whether every listed test level is accessible or functional in the shipped game.

## Summary

`debug.xmc` defines a 25-panel debug menu with 256 menu entries. It provides direct level loading across 13 location/test groups, chapter selection, one- or two-player mode selection, character assignment for two player slots, global item toggles, and four independent weapon slots with 15 selectable weapon codes each.
