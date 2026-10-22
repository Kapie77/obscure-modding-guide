# Obscure 2 — `edit_menu.xmc` Analysis

## 1. Overview

The file contains a menu definition with seven top-level sections. Each section groups menu entries, and each entry has an `action` code identifying the associated operation. Some entries also include a `value` attribute.

| Menu | Purpose indicated by its entries |
|---|---|
| `DISPLAY` | Rendering statistics, memory statistics, characters, lights, subtitles, and visual effects. |
| `CHEATS` | Gameplay cheats and options affecting character behavior, ammunition, voices, and item availability. |
| `CHAPTERS` | Chapter-selection entries for Chapters 2 through 12. |
| `DEBUG` | Debugger connection, main menu access, camera settings, settings load/save, and level restart. |
| `STRINGS` | String-related operations labeled `RESET` and `DUMP`. |
| `LANGUAGE` | Language selection. |
| `MEMORY CARD` | Memory-card operations, including formatting and filling. |

The labels suggest that this is a debug- or development-oriented menu. The XML defines menu labels and action identifiers, but does not reveal the implementation of each action.

## 2. Menu Structure

### 2.1 `DISPLAY`

Contains 11 entries related to display diagnostics and visual options.

| Menu label | Action code |
|---|---|
| `SHOW 3D STATS` | `3DST` |
| `SHOW GAME STATS` | `GAST` |
| `SHOW GAME STATS 2` | `GAS2` |
| `SHOW MAIN MEMORY STATS` | `MMST` |
| `SHOW LEVEL MEMORY STATS` | `MLST` |
| `SHOW LOADING STATS` | `LOST` |
| `ZONE SAFE XBOX` | `ZSXB` |
| `SHOW CHARACTERS` | `SHCH` |
| `SHOW LIGHTS LIST` | `LILI` |
| `SHOW SUBTITLES` | `SUBT` |
| `BLOOM` | `BLOM` |

The labels indicate options for displaying statistics and lists, toggling subtitles, and controlling visual effects. The exact behavior of each action code remains unverified.

### 2.2 `CHEATS`

Contains six entries associated with cheats or gameplay modifications.

| Menu label | Action code |
|---|---|
| `ENABLE NPC` | `ENPC` |
| `INVINCIBLE` | `INVI` |
| `AUTO RUN` | `ARUN` |
| `INFINITE AMMOS` | `IAMM` |
| `ENABLE VOICE` | `VOIC` |
| `SHOW ALL ITEMS` | `SHAL` |

The labels suggest options for NPC activation, invincibility, automatic running, unlimited ammunition, voice activation, and displaying all items.

### 2.3 `CHAPTERS`

Contains 11 entries for Chapters 2 through 12. All entries use the action code `CHAP`, with the chapter number stored in the `value` attribute.

| Menu label | Action | Value |
|---|---|---:|
| `Chapter 2` | `CHAP` | 2 |
| `Chapter 3` | `CHAP` | 3 |
| `Chapter 4` | `CHAP` | 4 |
| `Chapter 5` | `CHAP` | 5 |
| `Chapter 6` | `CHAP` | 6 |
| `Chapter 7` | `CHAP` | 7 |
| `Chapter 8` | `CHAP` | 8 |
| `Chapter 9` | `CHAP` | 9 |
| `Chapter 10` | `CHAP` | 10 |
| `Chapter 11` | `CHAP` | 11 |
| `Chapter 12` | `CHAP` | 12 |

Chapter 1 is not listed in this menu. This does not establish whether it is inaccessible through other mechanisms or simply omitted from this particular menu.

### 2.4 `DEBUG`

Contains six entries for debugging and game control.

| Menu label | Action code |
|---|---|
| `CONNECT TO SCRIPT DEBUGGER` | `HWEC` |
| `MAIN MENU` | `MENU` |
| `CAMERA SUPER WIDE` | `CASW` |
| `LOAD SETTINGS` | `LOAD` |
| `SAVE SETTINGS` | `SAVE` |
| `RESTART LEVEL` | `RESL` |

The labels suggest access to a script debugger, the main menu, a wide camera mode, settings load/save, and level restart functionality.

### 2.5 `STRINGS`

Contains two entries.

| Menu label | Action code |
|---|---|
| `RESET` | `RSTR` |
| `DUMP` | `DSTR` |

The names suggest operations on strings or string-related data. Their exact effects cannot be determined from the XML alone.

### 2.6 `LANGUAGE`

Contains five language options.

| Menu label | Action code |
|---|---|
| `ENGLISH` | `L_EN` |
| `FRENCH` | `L_FR` |
| `DEUTSCH` | `L_DE` |
| `ITALIAN` | `L_IT` |
| `SPANISH` | `L_SP` |

The action codes follow a language-selection pattern. The file lists these five options but does not establish whether additional languages are supported elsewhere in the game.

### 2.7 `MEMORY CARD`

Contains four entries associated with memory-card operations.

| Menu label | Action code |
|---|---|
| `COPY DEBUG TO CURRENT VERSION` | `MCDC` |
| `FORMAT` | `MCFO` |
| `UNFORMAT` | `MCUF` |
| `FILL` | `MCFI` |

The labels identify operations involving formatting, unformatting, filling, and copying debug data to the current version. The precise data affected by each operation requires further investigation.

## 3. XML Attributes

The entries use three attributes:

| Attribute | Observed use | Interpretation |
|---|---|---|
| `name` | Human-readable menu labels, such as `INVINCIBLE` and `Chapter 2`. | Defines the text displayed for a menu entry. |
| `action` | Four-character codes such as `INVI`, `CHAP`, and `MCFO`. | Identifies the operation associated with the entry. |
| `value` | Numeric chapter identifiers from `2` through `12`. | Supplies an additional parameter to the action, demonstrated by the `CHAP` entries. |

Attribute order varies between entries. For example, some entries place `action` before `name`, while others reverse the order. This is valid XML and does not imply a difference in behavior.

The `value` attribute is only present on the chapter entries in the supplied file.

## 4. Action Code Summary

The file contains **45 menu entries** distributed across seven sections.

| Section | Entry count |
|---|---:|
| `DISPLAY` | 11 |
| `CHEATS` | 6 |
| `CHAPTERS` | 11 |
| `DEBUG` | 6 |
| `STRINGS` | 2 |
| `LANGUAGE` | 5 |
| `MEMORY CARD` | 4 |
| **Total** | **45** |

Each entry has an `action` code. The `CHAP` action is reused for all 11 chapter entries, with `value` distinguishing the chapter number. The remaining action codes each appear once in the supplied XML.

## 5. Findings and Limitations

- The file defines menu labels, grouping, action codes, and chapter parameters for a menu that appears to serve debugging and development purposes.
- The `CHAPTERS` section explicitly lists Chapters 2–12, using `CHAP` with a numeric `value`.
- The `DISPLAY` and `CHEATS` sections contain options whose names indicate diagnostic and gameplay-modification functionality.
- The `LANGUAGE` section lists five language choices.
- The XML does not contain the code that executes the actions. Their precise implementation, persistence, and runtime effects cannot be confirmed from this file alone.
- The root tag, `tag_CCC38570`, is preserved as an observed identifier; its meaning has not been established.

## 6. Conclusion

`edit_menu.xmc` is a menu-definition file containing seven categories and 45 entries. Its labels and action codes indicate a debug-oriented interface with display diagnostics, gameplay cheats, chapter selection, debugging controls, string operations, language selection, and memory-card utilities.

The strongest confirmed findings are the menu organization, the action identifiers, and the chapter numbers supplied through `value`. Understanding the exact behavior of individual actions will require examining the code or other game resources that reference these identifiers.
