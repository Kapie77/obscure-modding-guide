# `chapters.xmc` — Obscure 2 File Analysis

## Overview

`chapters.xmc` is an XML configuration file containing multiple chapter-related configurations. Each configuration describes character states and, in most cases, an associated set of items.

The file provides information about:

- Chapter and configuration identifiers.
- Associated level identifiers.
- Character states, including life, position, and controller fields.
- Item classes and item identifiers.
- Character ownership of certain items.
- Ammunition and item quantity values.
- Differences between configurations associated with the same chapter number.

The XML establishes the structure and values described below. The exact runtime meaning of some attributes, particularly `chest`, `controller`, and `pos_id`, requires confirmation from other game files or runtime behavior.

## 1. XML Structure

The document uses a root `<chapter>` element containing multiple child `<chapter>` elements.

Simplified structure:

```xml
<?xml version="1.0" encoding="UTF-8"?>
<chapter>
  <chapter id="1" current_chapter="1" level_id="B101">
    <character
      id="BOY1"
      level_id="0"
      pos_id="0"
      life="100.0"
      controller="0"
    />
  </chapter>
</chapter>
```

The example above illustrates the structure; it is not a complete representation of the original file.

Each child `<chapter>` contains character entries and may also contain item entries.

### 1.1 Chapter Attributes

| Attribute | Observed meaning or interpretation |
|---|---|
| `id` | Identifies a chapter configuration. Values include numeric identifiers such as `1`, `2`, and `12`, as well as the composite identifier `6_2`. |
| `current_chapter` | Associates the configuration with a chapter number. |
| `level_id` | Identifies the level associated with the chapter configuration. |
| `chest` | Numeric attribute found in several configurations. Its exact meaning is unknown. |

The `id` and `current_chapter` attributes are not interchangeable.

For example:

```xml
<chapter id="6_2" level_id="E001" current_chapter="6" chest="2">
```

This configuration has the identifier `6_2`, but its `current_chapter` value is `6`.

The `chest` attribute must not be assumed to represent a literal chest, checkpoint, inventory category, or save slot without additional evidence.

## 2. Character Entries

Each chapter configuration in the supplied file contains eight character entries.

The character identifiers are:

| Identifier | Classification |
|---|---|
| `BOY1` | Character identifier |
| `BOY2` | Character identifier |
| `BOY3` | Character identifier |
| `BOY4` | Character identifier |
| `GIR1` | Character identifier |
| `GIR2` | Character identifier |
| `GIR3` | Character identifier |
| `GIR4` | Character identifier |

The identifiers suggest a naming scheme that distinguishes two groups of four characters. The XML alone does not establish their official names or confirm their exact relationship to the game's character roster.## 2. Character Entries

Each chapter configuration in the supplied file contains eight character entries. Their identifiers correspond to the game's eight main characters, as established by the character model names and asset paths.

### 2.1 Character Identifier Mapping

| XML identifier | Character name | Primary model name | Model asset location |
|---|---|---|---|
| `BOY1` | Stan | `boy1_pc` | `datapack\characters\boy1\boy1_pc` |
| `BOY2` | Corey | `boy2_pc` | `datapack\characters\boy2\boy2_pc` |
| `BOY3` | Sven | `boy3_pc` | `datapack\characters\boy3\boy3_pc` |
| `BOY4` | Kenny | `boy4_pc` | `datapack\characters\boy4\boy4_pc` |
| `GIR1` | Shannon | `gir1_pc.zwo` | `datapack\characters\gir1\gir1_pc` |
| `GIR2` | Mei | `gir2_pc` | `datapack\characters\gir2\gir2_pc` |
| `GIR3` | Amy | `gir3_pc` | `datapack\characters\gir3\gir3_pc` |
| `GIR4` | Jun | `gir4_pc` | `datapack\characters\gir4\gir4_pc` |

The `BOY1`–`BOY4` and `GIR1`–`GIR4` identifiers are therefore character references, not merely anonymous character categories.

### 2.2 Character Model Variants

Some characters have additional model variants:

| Character | Additional model or asset location | Notes |
|---|---|---|
| Corey | `boy2b_pc` under `datapack\characters\boy2b\boy2b_pc` | Alternative character model assets. |
| Amy | `gir3b_pc` under `datapack\characters\gir3b\gir3b_pc` | Alternative character model assets. |
| Amy (dead in the flower bed) | `NPCG01_0` in `datapack\levels\k\k003\lvl_pc` | Level-specific representation using the `amybmp` and `amytga` textures. |
| Jun (sleeping) | `PosingJun` in `datapack\levels\b\b105\lvl_pc` | Level-specific representation using the `JunB` and `JunH` textures. |

These level-specific representations should not be treated as additional character identifiers in `chapters.xmc`. They are separate asset references associated with particular scenes or level content.

### 2.3 Character Attributes

Each character entry can contain the following attributes:

| Attribute | Description |
|---|---|
| `id` | Identifies the character using one of the eight identifiers listed above. |
| `level_id` | Associates the character with a level identifier or the value `0`. |
| `pos_id` | Stores a numeric position reference. Its exact mapping to in-game placement has not yet been established. |
| `life` | Stores the character's life-related value. All character entries in the supplied XML use `100.0`. |
| `controller` | Stores a controller-related value, including `0`, `CHC1`, `CHTM`, or, in one case, an empty string. The exact meanings of these values remain under investigation. |

A character's `level_id` can differ from the parent chapter's `level_id`. These values should be documented separately rather than assuming that every character belongs to the chapter's primary level.

### 2.4 Character Life

All character entries in the supplied XML use:

```xml
life="100.0"
```

No different life values were observed in the supplied data.

This establishes that the configurations store the same life value for all listed characters. It does not establish whether the game always initializes characters at this value or whether the file is only a default configuration.

### 2.5 Controller Values

The following values occur in the `controller` attribute:

| Value | Observation |
|---|---|
| `0` | Frequently used for character entries. |
| `CHC1` | Appears on selected characters in multiple configurations. |
| `CHTM` | Appears on selected characters in multiple configurations. |
| Empty string | Appears on `BOY3` in chapter 2. |

The distribution of `CHC1` and `CHTM` changes between configurations.

For example, in chapter 1:

- `BOY2` uses `controller="CHC1"`.
- `GIR2` uses `controller="CHTM"`.

In chapter 2:

- `BOY4` uses `controller="CHC1"`.
- `GIR3` uses `controller="CHTM"`.

These values may identify controller types, control assignments, or another internal game mechanism. Their exact definitions require further investigation.

The value `0` should not automatically be interpreted as a dead, unavailable, or unplayable character. The XML does not establish that relationship.

### 2.6 Character Level IDs Can Differ from the Chapter Level

A character's `level_id` does not always match the parent chapter's `level_id`.

Examples from the supplied file:

| Chapter configuration | Chapter `level_id` | Character | Character `level_id` |
|---|---|---|---|
| `3` | `A006` | `BOY4` | `C008` |
| `3` | `A006` | `GIR3` | `C008` |
| `8` | `F006` | `BOY1` | `G003` |
| `8` | `F006` | `BOY3` | `G004` |
| `10` | `I000` | `BOY2` | `I007` |
| `10` | `I000` | `GIR3` | `I007` |
| `12` | `D003` | `BOY2` | `I014` |
| `12` | `D003` | `GIR3` | `I008` |

This is a direct observation from the XML. It indicates that character-level configuration can contain level identifiers different from the parent chapter's level identifier.

Possible explanations include separate areas, transitions, or character-specific placement configurations. These explanations remain hypotheses until the level definitions are examined.

## 3. Item Entries

Some chapter configurations contain `<item>` elements after the character entries.

A simplified example:

```xml
<item class_type="GUN" owner="BOY2" id="1" ammos="7.0" />
<item class_type="FLAS" id="1" />
<item class_type="MEDI" id="0" quantity="2" />
```

The item attributes describe the item class, identifier, optional owner, ammunition value, or quantity.

### 3.1 Item Attributes

| Attribute | Observed behavior | Interpretation |
|---|---|---|
| `class_type` | Contains codes such as `GUN`, `MEDI`, `DOC`, and `CPSS`. | Identifies the item class. |
| `id` | Contains values such as `0`, `1`, `2`, `17`, and `20`. | Identifies an item instance or variant within a class. The exact semantics are unknown. |
| `owner` | May contain character identifiers such as `BOY2`, `BOY3`, `BOY4`, or `GIR2`. | Associates the item with a character when specified. |
| `ammos` | Contains numeric values such as `0.0`, `1.0`, `2.0`, `5.0`, and `7.0`. | Stores an ammunition-related value for applicable items. |
| `quantity` | Appears on items such as `MEDI` and `AMSH`. | Stores a quantity-related value. |

Not every item has an `owner`, `ammos`, or `quantity` attribute.

For example, the following entries do not explicitly specify an owner:

```xml
<item class_type="FLAS" id="1" />
<item class_type="MEDI" id="0" quantity="2" />
```

The absence of `owner` is an observable property of the XML. It does not, by itself, prove that these items belong to a global inventory or are placed in the world.

### 3.2 Item IDs Are Not Necessarily Inventory Slot Numbers

The `id` attribute varies within some item classes.

For example, `DOC` entries include IDs such as `1`, `2`, `5`, `6`, `7`, `8`, `9`, `17`, `18`, `19`, and `20`.

The `BATT` and `SYRI` classes also appear with multiple IDs.

These values may identify predefined items, variants, or entries within an internal database. The XML does not establish that they correspond to inventory slots, chapter order, or the number of items owned by the player.

The `quantity` attribute should be considered separately from `id`.

## 4. Item Class Codes

The following identifications combine the observed `class_type` values with the supplied modding reference and previously identified texture names. Entries marked as probable or unconfirmed require further verification.

### 4.1 Weapons and Weapon-Like Items

| `class_type` | Possible identification | Evidence and notes |
|---|---|---|
| `BEAT` | Bat or melee weapon | Appears in multiple chapter configurations. |
| `CLUB` | Club or golf-club-like melee weapon | Appears in multiple configurations. |
| `CROS` | Unresolved melee weapon or related item | The exact mapping remains uncertain. |
| `CSAW` | Chainsaw | Appears from chapter 6 onward in the supplied configurations. |
| `GUN` | Pistol or generic firearm | May include an `owner` and an `ammos` value. |
| `TASE` | Taser | Appears with ammunition values, including `0.0`. |
| `CBOW` | Crossbow | Appears with different ammunition values. |
| `SHOT` | Shotgun | Appears with different ammunition values. |
| `FLBA` | Flare-related weapon | Exact name and function remain unconfirmed. |
| `FLGU` | Flare gun | Appears with ammunition values. |
| `UBFL` | Uber flashlight | Listed as a weapon-class entry in the XML. |
| `FLBG` | Possibly a flashbang or related explosive item | Exact mapping remains unconfirmed. |
| `DYNA` | Dynamite | Appears in chapter 10. |

The fact that a code appears in an item entry does not independently establish its official in-game name or whether the item is classified as a weapon by the user interface.

### 4.2 Ammunition-Related Codes

| `class_type` | Possible identification | Evidence and notes |
|---|---|---|
| `AMGU` | Possibly ammunition associated with a firearm | Appears in chapter 4 with `quantity="14"`. Its exact weapon association is unconfirmed. |
| `AMSH` | Possibly shotgun ammunition | Appears in chapter 11 with `quantity="7.0"`. |
| `AMFB` | Possibly ammunition associated with `FLBA` | Appears in chapter 11 with `ammos="4.0"`. This association is inferred from the codes, not confirmed. |
| `AMFG` | Possibly ammunition associated with `FLGU` | Appears in chapters 10 and 11 with different `ammos` values. The exact association remains unconfirmed. |

The names of these classes should be verified against item definitions, model references, or other files before being treated as definitive.

### 4.3 Consumables, Documents, and Other Items

| `class_type` | Identification | Evidence and notes |
|---|---|---|
| `FLAS` | Unconfirmed; possibly a flare or related item | Appears with IDs `1` and `2` in many configurations. The exact mapping requires confirmation. |
| `MEDI` | Medikit or healing item | Appears with `quantity` values such as `1` and `2`. |
| `BATT` | Battery | Appears with IDs `1` and `2`, among the supplied configurations. |
| `SYRI` | Syringe | Appears with IDs including `1`, `2`, and `3`. |
| `CPSS` | Compass | Associated with the previously identified `fs_cpss` texture. Appears from chapter 9 onward in the supplied excerpt. |
| `TALK` | Walkie-talkie or communication device | Appears from chapter 6 onward in the supplied configurations. |
| `DOC` | Document or document-related item | Appears with numerous IDs, including `1`, `2`, `5`, `6`, `7`, `8`, `9`, `17`, `18`, `19`, and `20`. |

The `DOC` class is especially notable because the same class can have many different IDs within one chapter. The XML does not include document titles or their contents.

### 4.4 Previously Identified Item Classes Not Present in This Excerpt

The following classes were identified or partially identified during separate analysis of item classes and textures:

| Code | Identification or current hypothesis | Related evidence |
|---|---|---|
| `ICRN` | Crank handle | Textures `fs_icrn001` and `fs_icrn002`. |
| `MEDA` | Medallion | Textures `fs_meda001` and `fs_meda002`; models `medallion001_pc` and `medallion002_pc`. |
| `IDSC` | Puzzle plate used in a light-based puzzle | Textures `fs_idsc001` and `fs_idsc002`. |
| `SERU` | Serum or healing item | Textures `fs_seru001`, `fs_seru002`, and `fs_seru003`. |
| `CHKE` | Small key | Associated texture `fs_chke`. |

These codes do not occur in the chapter configurations included in the supplied `chapters.xmc` excerpt. Their absence here does not establish that they are unused elsewhere in the game.

## 5. Chapter Configuration Inventory

The following inventory summarizes the chapter configurations in the supplied XML. The item lists refer to the `class_type` values present in each configuration. They do not imply that every item is assigned to a character.

### Chapter 1

- Configuration ID: `1`
- `current_chapter`: `1`
- Chapter level: `B101`
- Character controller assignments:
  - `BOY2`: `CHC1`
  - `GIR2`: `CHTM`
- Items: No `<item>` entries.

### Chapter 2

- Configuration ID: `2`
- `current_chapter`: `2`
- Chapter level: `A000`
- Character controller assignments:
  - `BOY4`: `CHC1`
  - `GIR3`: `CHTM`
- `BOY3` has an empty `controller` value.
- Items: No `<item>` entries.

### Chapter 3

- Configuration ID: `3`
- `current_chapter`: `3`
- Chapter level: `A006`
- Character controller assignments:
  - `BOY2`: `CHC1`
  - `GIR2`: `CHTM`
- `BOY4` and `GIR3` use `level_id="C008"`, different from the chapter's `A006`.
- Items: No `<item>` entries.

### Chapter 4

- Configuration ID: `4`
- `current_chapter`: `4`
- Chapter level: `D000`
- `chest`: `1`
- Character controller assignments:
  - `BOY2`: `CHC1`
  - `GIR3`: `CHTM`
- Item classes:
  - Weapons and weapon-like items: `BEAT`, `CLUB`, `CROS`, `GUN`, `TASE`
  - Other items: `FLAS`, `AMGU`, `DOC`, `MEDI`, `BATT`, `SYRI`
- Notable attributes:
  - `GUN` is assigned to `BOY2` with `ammos="7.0"`.
  - `BEAT` and `CROS` are assigned to `BOY4`.
  - `CLUB` is assigned to `GIR3`.
  - `MEDI` uses `id="0"` and `quantity="2"`.

### Chapter 5

- Configuration ID: `5`
- `current_chapter`: `5`
- Chapter level: `B000`
- `chest`: `1`
- Character controller assignments:
  - `BOY3`: `CHC1`
  - `GIR2`: `CHTM`
- `GIR4` uses `level_id="B105"` while the chapter level is `B000`.
- Item classes:
  - `BEAT`, `CLUB`, `CROS`, `GUN`, `TASE`, `FLAS`, `DOC`, `MEDI`, `BATT`, `SYRI`
- Notable attributes:
  - `GUN` and `TASE` are associated with `BOY3` and `GIR2`, respectively.
  - Both weapons have `ammos="0.0"`.
  - `MEDI` uses `id="0"` and `quantity="2"`.

### Chapter 6

- Configuration ID: `6`
- `current_chapter`: `6`
- Chapter level: `E100`
- `chest`: `1`
- Character controller assignments:
  - `BOY2`: `CHC1`
  - `GIR3`: `CHTM`
- Item classes:
  - `BEAT`, `CLUB`, `CROS`, `CSAW`, `GUN`, `TASE`, `SHOT`, `FLAS`, `DOC`, `MEDI`, `BATT`, `SYRI`, `TALK`
- Notable attributes:
  - `GUN` has `ammos="5.0"`.
  - `SHOT` has `ammos="0.0"`.
  - `MEDI` uses `id="0"` and `quantity="2"`.

### Chapter 6 — Additional Configuration

- Configuration ID: `6_2`
- `current_chapter`: `6`
- Chapter level: `E001`
- `chest`: `2`
- Character controller assignments:
  - `BOY3`: `CHC1`
  - `GIR2`: `CHTM`
- Character level IDs include `E002` for `BOY2` and `GIR3`, while the chapter level is `E001`.
- Item classes:
  - `BEAT`, `CLUB`, `CROS`, `CSAW`, `GUN`, `TASE`, `CBOW`, `SHOT`, `FLAS`, `DOC`, `MEDI`, `BATT`, `SYRI`, `TALK`
- Notable attributes:
  - `GUN`: `ammos="5.0"`.
  - `TASE`: `ammos="0.0"`.
  - `CBOW`: `ammos="2.0"`.
  - `SHOT`: `ammos="1.0"`.
  - `DOC` appears with IDs `1`, `17`, and `2`.
  - `MEDI` uses `id="0"` and `quantity="2"`.

### Chapter 7

- Configuration ID: `7`
- `current_chapter`: `7`
- Chapter level: `F000`
- `chest`: `3`
- Character controller assignments:
  - `BOY1`: `CHC1`
  - `GIR1`: `CHTM`
- Item classes:
  - `BEAT`, `CLUB`, `CROS`, `CSAW`, `GUN`, `TASE`, `CBOW`, `SHOT`, `FLBA`, `FLAS`, `DOC`, `MEDI`, `BATT`, `SYRI`, `TALK`
- Notable attributes:
  - `GUN`: `ammos="5.0"`.
  - `TASE`: `ammos="0.0"`.
  - `CBOW`: `ammos="0.0"`.
  - `SHOT`: `ammos="2.0"`.
  - `FLBA`: `ammos="0.0"`.
  - `BATT` appears with IDs `1` and `2`.
  - `MEDI` uses `id="0"` and `quantity="1"`.

### Chapter 8

- Configuration ID: `8`
- `current_chapter`: `8`
- Chapter level: `F006`
- `chest`: `4`
- Character controller assignments:
  - `BOY2`: `CHC1`
  - `GIR1`: `CHTM`
- Character level IDs include `G003` for `BOY1` and `G004` for `BOY3` and `GIR3`.
- Item classes:
  - `BEAT`, `CLUB`, `CROS`, `CSAW`, `GUN`, `TASE`, `CBOW`, `SHOT`, `FLBA`, `FLGU`, `FLAS`, `DOC`, `MEDI`, `BATT`, `SYRI`, `TALK`
- Notable attributes:
  - `GUN`: `ammos="5.0"`.
  - `TASE`, `CBOW`, `FLBA`, and `FLGU` have `ammos="0.0"`.
  - `SHOT`: `ammos="2.0"`.
  - `DOC` appears with IDs `1`, `17`, `2`, `18`, and `5`.
  - `BATT` appears with IDs `1` and `2`.
  - `SYRI` uses `id="2"`.

### Chapter 9

- Configuration ID: `9`
- `current_chapter`: `9`
- Chapter level: `H000`
- `chest`: `4`
- Character controller assignments:
  - `BOY3`: `CHC1`
  - `GIR3`: `CHTM`
- Item classes:
  - `BEAT`, `CLUB`, `CROS`, `CSAW`, `GUN`, `TASE`, `CBOW`, `SHOT`, `FLBA`, `FLGU`, `FLAS`, `DOC`, `MEDI`, `BATT`, `SYRI`, `CPSS`, `TALK`
- Notable attributes:
  - `GUN`: `ammos="5.0"`.
  - `TASE`: `ammos="0.0"`.
  - `CBOW`: `ammos="2.0"`.
  - `SHOT`: `ammos="3.0"`.
  - `FLBA`: `ammos="5.0"`.
  - `FLGU`: `ammos="3.0"`.
  - `CPSS` appears with `id="1"`.
  - `DOC` includes IDs `1`, `17`, `2`, `18`, `5`, `6`, `9`, and `19`.
  - `SYRI` uses `id="2"`.

### Chapter 10

- Configuration ID: `10`
- `current_chapter`: `10`
- Chapter level: `I000`
- `chest`: `5`
- Character controller assignments:
  - `BOY1`: `CHTM`
  - `GIR1`: `CHC1`
- `BOY2` and `GIR3` use `level_id="I007"`.
- Item classes:
  - `BEAT`, `CLUB`, `CROS`, `CSAW`, `GUN`, `TASE`, `CBOW`, `SHOT`, `UBFL`, `FLBA`, `FLGU`, `FLAS`, `FLBG`, `DYNA`, `AMFG`, `DOC`, `MEDI`, `BATT`, `SYRI`, `CPSS`, `TALK`
- Notable attributes:
  - `GUN`: `ammos="0.0"`.
  - `CBOW`: `ammos="2.0"`.
  - `SHOT`: `ammos="2.0"`.
  - `FLBA`: `ammos="0.0"`.
  - `FLGU`: `ammos="1.0"`.
  - `AMFG`: `ammos="2.0"`.
  - `MEDI` uses `id="0"` and `quantity="2"`.
  - `BATT` appears with IDs `1` and `2`.
  - `SYRI` uses `id="3"`.
  - `CPSS` uses `id="1"`.
  - `DOC` includes IDs `1`, `17`, `2`, `18`, `5`, `6`, `9`, `19`, `7`, `20`, and `8`.

### Chapter 11

- Configuration ID: `11`
- `current_chapter`: `11`
- Chapter level: `I007`
- `chest`: `5`
- Character controller assignments:
  - `BOY1`: `CHTM`
  - `BOY2`: `CHC1`
- All eight character entries use `level_id="I007"` or `level_id="0"`.
- Item classes:
  - `BEAT`, `CLUB`, `CROS`, `CSAW`, `GUN`, `TASE`, `CBOW`, `SHOT`, `UBFL`, `FLBA`, `FLGU`, `FLAS`, `FLBG`, `AMSH`, `AMFB`, `AMFG`, `DOC`, `MEDI`, `BATT`, `SYRI`, `CPSS`, `TALK`
- Notable attributes:
  - `GUN`: `ammos="7.0"`.
  - `TASE`: `ammos="0.0"`.
  - `CBOW`: `ammos="2.0"`.
  - `SHOT`: `ammos="5.0"`.
  - `FLBA`: `ammos="4.0"`.
  - `FLGU`: `ammos="1.0"`.
  - `AMSH`: `quantity="7.0"`.
  - `AMFB`: `ammos="4.0"`.
  - `AMFG`: `ammos="3.0"`.
  - `MEDI` uses `id="0"` and `quantity="2"`.
  - `BATT` appears with IDs `1` and `2`.
  - `SYRI` uses `id="3"`.
  - `CPSS` uses `id="1"`.
  - `DOC` includes IDs `1`, `17`, `2`, `18`, `5`, `6`, `9`, `19`, `7`, `20`, and `8`.

### Chapter 12

- Configuration ID: `12`
- `current_chapter`: `12`
- Chapter level: `D003`
- No `chest` attribute is present.
- Character controller assignments:
  - `BOY1`: `CHC1`
  - `GIR1`: `CHTM`
- `BOY2` uses `level_id="I014"`.
- `GIR3` uses `level_id="I008"`.
- No `<item>` entries are present in this configuration.

The absence of item entries does not prove that the characters have no equipment in the running game. Equipment could be supplied by another configuration or system.

## 6. Observed Patterns Across Configurations

### 6.1 Repeated Character Entries

All supplied chapter configurations contain the same eight character identifiers.

The values of `level_id`, `pos_id`, and `controller` change between configurations. This suggests that the file stores per-configuration character state rather than merely defining a static list of characters.

The exact rules used to interpret these fields remain unknown.

### 6.2 Item Availability Changes Between Configurations

The item sets vary between chapters.

Examples:

- `CSAW` appears in chapter 6 and later configurations.
- `CBOW` appears from the additional chapter 6 configuration onward.
- `FLGU` appears in chapters 8–11.
- `UBFL`, `FLBG`, and `DYNA` appear in chapter 10.
- `AMSH` and `AMFB` appear in chapter 11.
- `CPSS` appears in chapters 9–11.

These observations show that the declared item sets differ across configurations. They do not establish the exact moment when each item becomes obtainable during normal gameplay.

### 6.3 Item Ownership Is Selectively Specified

Some items include an `owner` attribute, particularly in chapters 4 and 5.

Examples:

```xml
<item class_type="BEAT" id="1" owner="BOY4" />
<item class_type="CLUB" id="1" owner="GIR3" />
<item class_type="GUN" owner="BOY2" id="1" ammos="7.0" />
```

Later configurations often omit `owner` from item entries.

This is a structural difference in the data. The meaning of an omitted owner must be confirmed before deciding whether an item is assigned to a character, stored elsewhere, or handled by another system.

### 6.4 Ammunition Values Change Between Configurations

Some weapon entries have different `ammos` values in different chapters.

Examples include:

- `GUN`: values such as `0.0`, `5.0`, and `7.0`.
- `CBOW`: values such as `0.0` and `2.0`.
- `SHOT`: values such as `0.0`, `1.0`, `2.0`, `3.0`, and `5.0`.
- `FLBA`: values such as `0.0`, `4.0`, and `5.0`.
- `FLGU`: values such as `0.0`, `1.0`, and `3.0`.

These values are stored directly in the XML. Whether they represent loaded ammunition, total ammunition, charges, or another internal quantity depends on the game's implementation.

### 6.5 The `chest` Attribute

Observed values:

| Configuration | `chest` |
|---|---:|
| Chapter 4 | `1` |
| Chapter 5 | `1` |
| Chapter 6 | `1` |
| Additional chapter 6 configuration (`6_2`) | `2` |
| Chapter 7 | `3` |
| Chapter 8 | `4` |
| Chapter 9 | `4` |
| Chapter 10 | `5` |
| Chapter 11 | `5` |

No `chest` attribute is present in chapters 1–3 or chapter 12 in the supplied XML.

The repeated and increasing values may indicate a grouping or progression mechanism, but the exact purpose of the attribute remains unknown. It should not be interpreted as a confirmed inventory chest count or checkpoint identifier.

## 7. Data Anomalies and Special Cases

### 7.1 Composite Configuration ID

The configuration `id="6_2"` is associated with `current_chapter="6"`.

This establishes that configuration IDs can include a suffix and that the configuration identifier is not always the chapter number.

### 7.2 Empty Controller Value

In chapter 2, `BOY3` contains:

```xml
<character pos_id="0" controller="" id="BOY3" level_id="0" life="100.0" />
```

This differs from the more common `controller="0"` value.

The XML does not establish whether the empty string has a distinct meaning or is simply another representation of an unset value.

### 7.3 Characters Associated with Other Levels

Several configurations contain characters whose `level_id` differs from the parent chapter's `level_id`.

These differences should be preserved when parsing or editing the file. Automatically replacing all character-level IDs with the parent chapter's level could destroy information encoded in the original configuration.

### 7.4 Chapter Without Item Entries

Chapter 12 contains character entries but no item entries.

This should be documented as an absence of item declarations in this configuration, rather than proof of an empty in-game inventory.

### 7.5 Zero Ammunition Values

Multiple weapons have `ammos="0.0"`.

A zero value should be preserved as data. It should not automatically be treated as equivalent to a missing `ammos` attribute.

### 7.6 Integer and Floating-Point Values

The file uses numeric strings in more than one format:

```xml
quantity="2"
quantity="7.0"
ammos="5.0"
life="100.0"
```

A parser should preserve the distinction between missing attributes and explicit numeric values. If the XML is rewritten, maintaining the original representation may also help avoid unnecessary differences.

## 8. Relationship to Other Game Files

The following investigations could clarify the remaining uncertainties.

### 8.1 Item Definitions

Search for definitions of the `class_type` codes and the corresponding item IDs.

This could establish:

- Official item names.
- Which IDs represent distinct items or variants.
- Which classes are weapons, ammunition, consumables, or documents.
- The intended meaning of `owner`, `ammos`, and `quantity`.

### 8.2 Level Definitions

Investigate the level IDs referenced in the chapter and character entries, including:

`A000`, `A006`, `B000`, `B101`, `B105`, `C008`, `D000`, `D003`, `E001`, `E002`, `E100`, `F000`, `F006`, `G003`, `G004`, `H000`, `I000`, `I007`, `I008`, and `I014`.

The relevant level files may explain why some characters have level IDs different from the parent chapter configuration.

### 8.3 Controller Definitions

Search for `CHC1` and `CHTM` in other game files.

Their definitions may clarify whether they represent player-control schemes, character control states, or another internal mechanism.

### 8.4 Position Definitions

Search for the `pos_id` values in level or character placement data.

Examples worth investigating include:

`30`, `34`, `117`, `1001`, `1002`, `1003`, `1004`, `2001`, `2002`, `2003`, and `2004`.

Without those definitions, the IDs should be treated as references to unknown positions rather than world coordinates.

### 8.5 Chapter and Checkpoint Logic

Search for references to the `chest` attribute and the composite ID `6_2`.

This may clarify whether the configurations correspond to checkpoints, chapter variants, equipment presets, or another type of progression state.

## 9. Parsing and Editing Considerations

When implementing a parser or editor for `chapters.xmc`, the following precautions are appropriate.

1. Preserve the distinction between the parent chapter's `level_id` and each character's `level_id`.
2. Preserve configuration IDs such as `6_2` as strings rather than assuming all IDs are integers.
3. Treat `current_chapter` and `chest` as separate attributes.
4. Allow item entries to omit `owner`, `ammos`, or `quantity`.
5. Do not assume every item has a character owner.
6. Do not assume item IDs correspond to inventory slots.
7. Preserve explicit zero values, including `ammos="0.0"`.
8. Preserve the distinction between a missing `controller` attribute, `controller="0"`, and `controller=""`.
9. Allow chapters to contain character entries without item entries.
10. Retain unknown item classes rather than discarding them.
11. Preserve multiple entries of the same `class_type` when their IDs differ.
12. Avoid modifying unknown attributes until their meaning is established.

These are conservative data-handling recommendations based on the structure of the supplied XML, not claims about the game's internal implementation.

## 10. Confirmed Observations vs. Unresolved Questions

### Directly supported by the XML

- The file contains multiple chapter configurations.
- Configurations have identifiers and may specify a `current_chapter`.
- Each supplied configuration contains eight character entries.
- Character entries include `id`, `level_id`, `pos_id`, `life`, and `controller`.
- All supplied character entries use `life="100.0"`.
- Some configurations contain item entries, while others do not.
- Items use class codes and may include IDs, owners, ammunition values, and quantities.
- Character level IDs can differ from the parent chapter's level ID.
- The configuration ID `6_2` is associated with chapter 6.
- The `chest` attribute is present in several configurations and has values from `1` to `5` in the supplied data.

### Still unconfirmed

- The exact meanings of `CHC1` and `CHTM`.
- The mapping from `pos_id` values to actual positions.
- The exact meaning of `chest`.
- Whether the configurations are initial states, checkpoint states, presets, or a combination.
- Whether items without `owner` belong to a shared inventory or another system.
- The official names of unresolved item classes.
- Whether ammunition values represent loaded ammunition, total ammunition, or another quantity.
- Why chapter 12 contains no item declarations.
- Why certain characters use level IDs different from the parent chapter's level ID.

## Conclusion

`chapters.xmc` is a structured XML configuration file that associates chapter-related configurations with level identifiers, character states, and optional item lists.

Its most useful information for reverse engineering is the relationship between chapter configurations, character-level assignments, controller values, item classes, item IDs, and ammunition or quantity fields.

The XML provides a reliable basis for documenting these fields and comparing configurations. However, the meanings of `chest`, `controller`, `pos_id`, and some item classes should remain explicitly marked as unknown until corroborating definitions or runtime evidence are available.
