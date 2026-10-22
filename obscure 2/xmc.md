# Obscure 2 — XMC File Inventory

This document tracks the `.xmc` files identified during the Obscure 2 modding investigation. It is intended to grow as more files are extracted, inspected, and understood.

> **Scope note:** This is the inventory of filenames identified in our discussion so far, not a claim that these are every `.xmc` file shipped with the game.

## Inventory

| File | Known location / context | Status | Summary |
|---|---|---|---|
| [`game.xmc`](#gamexmc) | Extracted to `game.xml` for inspection | **Analyzed** | Appears to contain game configuration and resource references, including character/state settings, item and weapon metadata, save-point identifiers, chest contents, cinematic entries, animation files, and resource directories. |
| `combos.xmc` | Mentioned under `datapack\characters\combos.xmc` | **Not analyzed yet** | Purpose and internal structure still need to be confirmed by inspecting its XML output. The filename suggests combo-related data, but that is only a filename-based hypothesis. |
| `chapters.xmc` | Mentioned as `chapters.xmc` in the converter working folder | **Not analyzed yet** | Purpose and internal structure still need to be confirmed by inspecting its XML output. The filename suggests chapter-related data, but that is only a filename-based hypothesis. |
| `e100.xmc` | Extracted with `obscure-xmc-converter extract e100.xmc`, producing `e100.xml` | **Extracted; not analyzed yet** | The XML was generated successfully. Its role and contents have not yet been documented. |

## `game.xmc`

### Current summary

`game.xmc` appears to be a broad game-configuration file rather than a file dedicated to one single asset. Its extracted XML contains several groups of settings and references:

- **Common game state:** character-slot identifiers (including `BOY1`–`BOY4` and `GIR1`–`GIR4`), life/state values, level and position identifiers, and controller-related fields.
- **Gameplay settings:** health-item limits such as the maximum number of medikits and energy drinks.
- **Items and weapons:** item/weapon class tables and metadata fields, including identifiers, string IDs, inventory names, descriptions, usage-related fields, quantities, ammunition, and teammate-healing information.
- **Lighting parameters:** a light type and attenuation-related numeric parameters.
- **Save points:** a collection of save-point IDs and associated string IDs.
- **Chests:** entries that reference item/weapon codes and, in some cases, quantities.
- **Cinematics or sequences:** entries with IDs and display/playback-related fields. The precise meaning of individual fields still needs verification.
- **Animation references:** paths to `.zwo` files.
- **Resource references:** paths such as `Assets\Door\`, `Assets\hcase\`, `Assets\Weapons\`, and `Assets\Heart\`.

### What it may control

Based on the extracted structure, `game.xmc` likely supplies configuration used by multiple game systems: shared state, gameplay item limits and definitions, save-point/chest data, cinematic configuration, and references to other resources.

This is a working interpretation of the extracted XML, not a definitive statement about the game's runtime implementation. Some field names and codes are not self-explanatory; their meanings should be confirmed by comparing the XML with related files and testing changes in-game.

### Confidence

- **High confidence:** the file contains the groups and values listed above, because they are present in the extracted XML.
- **Moderate confidence:** the broad functional interpretation as shared game configuration.
- **Unconfirmed:** the exact runtime meaning of every field, identifier, and resource reference.

## Files to investigate next

### `combos.xmc`

- **Known path:** `datapack\characters\combos.xmc`
- **Current status:** Not analyzed.
- **Next step:** Extract to XML, record its top-level structure, and inspect the fields and IDs before assigning meanings.

### `chapters.xmc`

- **Known context:** `chapters.xmc` was mentioned in the converter working folder.
- **Current status:** Not analyzed.
- **Next step:** Extract to XML and check whether it describes chapter progression, chapter metadata, or something else. Do not assume the filename alone proves its purpose.

### `e100.xmc`

- **Known context:** `e100.xmc` was extracted successfully and produced `e100.xml`.
- **Current status:** Extracted, but not analyzed.
- **Next step:** Inspect `e100.xml`, document its root and main sections, and compare its identifiers with other files where useful.

## Investigation template for future files

Copy this section for each newly discovered `.xmc` file:

### `filename.xmc`

- **Known path:**
- **Extracted XML:**
- **Status:** Not analyzed / Extracted / Partially analyzed / Analyzed
- **Root element and main sections:**
- **Likely purpose:**
- **Evidence from XML:**
- **Related files or identifiers:**
- **Confidence / unresolved questions:**

---

## Notes

- The converter warning `hashes.json not found` means unknown CRC-based names may remain unresolved; it does not by itself mean extraction failed.
- Keep observed facts separate from hypotheses. A filename or an unfamiliar ID is not enough to establish what a file or field does.
- Update this inventory as more `.xmc` files are provided and analyzed.
