# `edit_menu2.xmc` Analysis

## Overview

`edit_menu2.xmc` is an XML representation of a debug-oriented menu configuration for *Obscure 2*. The document uses the root element `tag_CCC38570` and defines three menus containing 14 items in total.

The XML directly establishes menu names, item labels, action codes, and—where present—numeric values. The descriptions of what the actions do are interpretations based on the labels and codes; their implementation is not confirmed by this file alone.

## Structure

| Menu | Number of items | Contents |
|---|---:|---|
| `DEBUG` | 2 | Infinite ammunition and debug information |
| `CHAPTERS` | 11 | Chapter selection for Chapters 2–12 |
| `MEMORY CARD` | 1 | Copy debug data to the current version |
| **Total** | **14** | **3 menus** |

## 1. `DEBUG`

| Item name | Action code | Value | Interpretation |
|---|---|---|---|
| `Infinite ammos` | `IAMM` | Not specified | Appears to enable or control infinite ammunition. |
| `Show debug infos` | `GAST` | Not specified | Appears to display debug information. |

The XML does not indicate whether either item is a toggle, a one-time command, or a persistent setting.

## 2. `CHAPTERS`

The menu defines 11 chapter entries. Every entry uses the action code `CHAP`, and the `value` attribute identifies a chapter number from 2 through 12.

| Item name | Action code | Value |
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

**Interpretation:** `CHAP` likely triggers chapter selection or loading using the numeric `value`. This behavior is inferred from the labels and attribute pattern; the XML does not define the implementation. No entry for Chapter 1 appears in this file.

## 3. `MEMORY CARD`

| Item name | Action code | Value | Interpretation |
|---|---|---|---|
| `COPY DEBUG TO CURRENT VERSION` | `MCDC` | Not specified | Appears to copy debug data to the current version. |

The XML does not specify which data is copied, the source of that data, or any execution conditions.

## Comparison with `edit_menu.xmc`

Based on the previously analyzed `edit_menu.xmc`, that file contains seven menus and 45 items, including display diagnostics, gameplay cheats, chapter selection, debugging controls, string operations, language selection, and several memory-card utilities.

`edit_menu2.xmc` is considerably smaller: it contains only `DEBUG`, `CHAPTERS`, and `MEMORY CARD`, with 14 items total. It retains two debug options, the Chapter 2–12 entries, and one memory-card operation (`MCDC`). This is a structural comparison only; the XML files do not establish why the menus differ or whether one replaces the other in a particular game state or build.

## Notes and limitations

- The root element is `tag_CCC38570`; its meaning is not established by this file.
- The action codes `IAMM`, `GAST`, `CHAP`, and `MCDC` are present in the XML. Their descriptions above are inferred from labels and context, not confirmed implementation details.
- No item includes a `value` attribute except the chapter entries.
- Attribute order varies between entries, but the XML structure and the action/value associations remain clear.
