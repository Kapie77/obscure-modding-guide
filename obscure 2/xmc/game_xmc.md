# `game.xmc` — Obscure 2 File Reference

## Overview

`game.xmc` is a compiled XML configuration file used by **Obscure 2**. The supplied XML dump shows a collection of game-wide definitions and resource references, including character state, item and weapon metadata, save-point identifiers, chest contents, cinematic or visual entries, animation files, and resource directories.

The `.xmc` format is described by the *Obscure Modding Guide* as a compiled XML format used by the UI in Obscure 2 and Final Exam. However, this particular file contains more than UI layout: its structure suggests that `.xmc` is also used for configuration and resource metadata. The exact runtime role of every element should be confirmed against other files or the game's loader.

This document distinguishes **direct observations** from **tentative interpretations**. Names such as `MEDI` and `GUN` are present in the file; expansions of less obvious codes are hypotheses unless independently confirmed.

## Top-level structure

```text
tag_232B318C
├── common_state
│   └── character [repeated]
├── settings
│   ├── health
│   ├── toe [repeated: items, documents, weapons]
│   ├── light_param
│   ├── savepoints
│   │   └── savepoint [repeated]
│   └── chests
│       └── chest [repeated]
│           └── item [repeated]
├── kines
│   └── kine [repeated]
├── anim_files
│   └── file [repeated]
└── zoe_files
    └── file [repeated]
```

The root tag `tag_232B318C` appears to be an internal or generated identifier. Its meaning is not established by the XML alone.

## 1. `common_state`: shared game and character state

Example:

```xml
<common_state attr_B3DFCA20="12"
              level_id="B101"
              current_chapter="1">
    <character life="100.0"
               level_id="0"
               pos_id="0"
               controller="0"
               id="BOY1" />
</common_state>
```

### Attributes

| Attribute | Observed meaning / interpretation |
|---|---|
| `attr_B3DFCA20` | Unknown internal attribute. The supplied file sets it to `12`. |
| `level_id` | Likely a level or scene identifier. |
| `current_chapter` | Likely the current chapter index or identifier. |
| `character` | A character-state record. |
| `id` | Character code, such as `BOY1` or `GIR2`. |
| `life` | Character life value; all eight records in this file show `100.0`. |
| `pos_id` | Likely a position, spawn-point, or placement identifier. |
| `controller` | Unknown controller or character-state code. Some entries use `0`; others use codes such as `CHC1` and `CHTM`. |

### Character identifiers

The file lists eight records:

- `BOY1`, `BOY2`, `BOY3`, `BOY4`
- `GIR1`, `GIR2`, `GIR3`, `GIR4`

The names appear to correspond to the four male and four female main-character slots. The modding reference identifies the PC models as Stan, Corey, Sven, Kenny, Shannon, Mei, Amy, and Jun, respectively. The exact mapping between these IDs and names should still be verified against character configuration files.

`BOY2` and `GIR2` have `level_id="B101"` and non-zero controller codes (`CHC1` and `CHTM`), while most other records use `level_id="0"` and `controller="0"`. This may indicate a special initial state or selected characters, but the XML alone does not establish the meaning.

## 2. `settings`

This section contains several kinds of configuration: health limits, object definitions, lighting parameters, save-point identifiers, and chest contents.

### 2.1. `health`

```xml
<health nbMedikitMax="3" nbEnergyDrinkMax="5" />
```

| Attribute | Value | Likely meaning |
|---|---:|---|
| `nbMedikitMax` | `3` | Maximum number of medikits allowed in the relevant inventory or state. |
| `nbEnergyDrinkMax` | `5` | Maximum number of energy drinks allowed in the relevant inventory or state. |

The file does not reveal whether these limits apply per character, to a shared inventory, or globally.

### 2.2. `toe`: object definitions

The repeated `toe` elements appear to define entries in an object catalogue. They include ordinary items, documents, and weapons.

Item example:

```xml
<toe type="item"
     classtype="MEDI"
     string_id="8500008"
     inv_name_id="8500008"
     look="1"
     use="1"
     heal_teammate="1" />
```

Weapon example:

```xml
<toe type="weapon"
     classtype="GUN"
     string_id="04500058"
     inv_name_id="04500058"
     ammo="bullet" />
```

Document example:

```xml
<toe type="doc"
     id="1"
     string_id="0C500008"
     inv_name_id="0C500008"
     classtype="DOC" />
```

#### Observed attributes

| Attribute | Interpretation |
|---|---|
| `type` | Broad category. Values in this file include `item`, `weapon`, and `doc`. |
| `classtype` | Short internal class code, such as `MEDI`, `GUN`, or `DOC`. |
| `id` | Additional identifier or variant within a class. |
| `string_id` | Text/string-table identifier, likely used for a displayed name or related text. |
| `inv_name_id` | Identifier apparently associated with the inventory name. |
| `desc_id` | Identifier apparently associated with a description. |
| `look` | Likely controls whether an object can be examined or viewed. |
| `use` | Likely controls whether an object can be used. |
| `quantity` | Quantity value associated with the object. |
| `ammo` | Ammunition or consumption category. Values include `bullet`, `elec`, and `quantity`. |
| `heal_teammate` | Likely indicates whether an item can be used to heal a teammate. |

These interpretations are based on attribute names and context; exact behavior should be verified in the game or its loader. The values `0` and `1` appear to be flags, but their behavior is not proven by this file alone.

#### Item class codes

The following codes occur in `toe` entries with `type="item"`. The expansions below are tentative unless noted as a recognizable name.

| `classtype` | Possible meaning / notes |
|---|---|
| `MEDI` | Medikit / healing item |
| `SODA` | Soda or chemical item; the model reference identifies a soda item as caustic soda |
| `ENDR` | Energy drink |
| `ACID` | Acid |
| `BLEA` | Bleach |
| `GLYC` | Glycerin |
| `ICE` | Ice |
| `JERR` | Jerrycan / gasoline container |
| `PASS` | Pass or access card |
| `WELD` | Welder |
| `LVER` | Lever-related item; the model reference marks a lever model as discarded |
| `ICRN` | Unknown; needs confirmation |
| `MEDA` | Unknown; needs confirmation |
| `IDSC` | Unknown; needs confirmation |
| `JEMM` | Likely jemmy / bolt cutter, based on the model reference |
| `SYRI` | Syringe |
| `SERU` | Unknown; needs confirmation |
| `CPSS` | Unknown; needs confirmation |
| `CHKE` | Unknown; needs confirmation |
| `STAT` | Possibly statuette; the model reference lists a crucifix/statuette model |
| `BKPK` | Backpack; the model reference marks one backpack model as discarded/unused |
| `TBAT` | Possibly a battery-related item; unconfirmed |
| `TALK` | Walkie-talkie or communication item; the model reference marks a talkie model as discarded/unused |

Some entries use `id` to distinguish multiple instances or variants of a class. For example, `PASS`, `ICRN`, `MEDA`, `IDSC`, `SYRI`, `SERU`, and `BKPK` have multiple IDs. Do not assume these IDs correspond to inventory slot numbers without further evidence.

#### Weapon class codes

The following codes occur in entries with `type="weapon"`. Names are cross-referenced with the supplied modding guide where a plausible match exists.

| `classtype` | Likely weapon / note | `ammo` value |
|---|---|---|
| `BEAT` | Bat / melee weapon | Not specified |
| `CLUB` | Club or golf-club-like melee weapon | Not specified |
| `UBET` | Unknown; possibly a weapon variant | Not specified |
| `CROS` | Cross/hockey-stick-related code; exact mapping uncertain | Not specified |
| `CSAW` | Chainsaw | `elec` |
| `GUN` | Pistol / generic firearm | `bullet` |
| `FLGU` | Flare gun | `bullet` |
| `FLBA` | Flare-related weapon; exact name uncertain | `bullet` |
| `TASE` | Taser | `elec` |
| `CBOW` | Crossbow | `bullet` |
| `SHOT` | Shotgun | `bullet` |
| `UZI` | Uzi | `bullet` |
| `UBFL` | Uber flashlight | `elec` |
| `DYNA` | Dynamite | `quantity` |
| `FLBG` | Flashbang or flash-ball-related weapon; exact mapping uncertain | `quantity` |

The `ammo` values should be treated as engine categories. For example, `elec` may indicate an electrical charge or energy resource rather than conventional ammunition.

The modding guide lists weapon models such as `bat_pc`, `chainsaw_pc`, `cross_pc`, `crossbow_pc`, `dynamite_pc`, `flaregun_pc`, `flashball_pc`, `flashbang_pc`, `flashlight_pc`, `golfclub_pc`, `gun_pc`, `shotgun_pc`, `taser_pc`, `uberflashlight_pc`, and `uzi_pc`. These model names provide useful clues, but a class code should not be mapped to a specific model unless the relationship is confirmed.

### 2.3. `light_param`: lighting parameters

```xml
<light_param type="omni" att2="0.00001" att0="0" att1="0.015" />
```

| Attribute | Value |
|---|---|
| `type` | `omni` |
| `att0` | `0` |
| `att1` | `0.015` |
| `att2` | `0.00001` |

`omni` suggests an omnidirectional light. `att0`, `att1`, and `att2` resemble constant, linear, and quadratic attenuation coefficients used in some lighting systems. This is a plausible interpretation, not a confirmed description of the engine's implementation.

### 2.4. `savepoints`: save-point identifiers

Example:

```xml
<savepoints>
    <savepoint id="0110" string_id="0C204001" />
    <savepoint id="0210" string_id="0C204002" />
    <savepoint id="0310" string_id="0C20401C" />
</savepoints>
```

Each entry has:

- `id`: a save-point identifier.
- `string_id`: an associated text/string identifier.

The supplied file contains multiple IDs, including `0110`, `0210`, `0310`, `0320`, `0330`, `0410`, `0510`, `0520`, `0610`, `0620`, `0660`, `0670`, `0710`, `0720`, `0730`, `0810`, `0820`, `0910`, `0920`, `0930`, `1010`, `1110`, `1120`, `1130`, `1210`, `1230`, and `1240`.

The IDs may follow a chapter, level, or checkpoint naming scheme, but the pattern alone does not prove how they are organized. No world coordinates are present in these records, so this block should be described as a registry of save-point IDs rather than a list of physical locations.

### 2.5. `chests`: chest contents

Example:

```xml
<chests>
    <chest>
        <item code="TASE" />
    </chest>
    <chest>
        <item code="FLGU" />
        <item code="AMFG" quantity="3" />
    </chest>
</chests>
```

The file contains seven `<chest>` entries:

| Entry | Contents |
|---:|---|
| 1 | `TASE` |
| 2 | `CBOW` |
| 3 | `FLBA` |
| 4 | `FLGU`; `AMFG` with quantity `3` |
| 5 | `UBFL` |
| 6 | `UZI` |
| 7 | `12_0` with quantity `0` |

These entries appear to define chest loadouts or predefined chest contents. No coordinates or room IDs appear here, so the file does not show where each chest is placed in a level.

`AMFG` appears in a chest entry but is not present among the supplied `toe` definitions. The modding guide associates `amfg_pc` with a package of bullets, suggesting that `AMFG` may be an ammunition item. This should be verified against other configuration files.

The final entry (`code="12_0"`, `quantity="0"`) is unusual and may be a special case, placeholder, or empty/disabled entry. Its purpose is unknown.

## 3. `kines`: cinematic or visual-resource definitions

The `kines` section contains many `<kine>` records identified by `id`. The records fall into two visible groups.

### 3.1. Sequence-like IDs

Examples:

```xml
<kine id="MENU" width="512" height="256" skip="0" do_16_9="0" />
<kine id="MRS" width="512" height="256" skip="1" do_16_9="1" />
<kine id="HYDR" width="512" height="256" skip="1" do_16_9="0" />
<kine id="01_1" width="512" height="256" loc="1" sub="1" />
```

IDs include `MENU`, `MRS`, `HYDR`, `ATTR`, chapter-like IDs such as `01_1`, `02_2`, and `12_9`, and IDs beginning with `RTC` such as `RTC4`, `RTCC`, `RTCK`, `RTCR`, `RTCS`, and `RTCW`.

| Attribute | Tentative interpretation |
|---|---|
| `id` | Identifier for a sequence or visual resource. |
| `width`, `height` | Base or reference dimensions. |
| `skip` | Likely indicates whether the sequence can be skipped. |
| `do_16_9` | Likely controls a widescreen (16:9) behavior or variant. |
| `loc` | Possibly a localization or variant flag. |
| `sub` | Possibly a subtitle flag or variant. |

These entries may refer to in-engine cinematics or other presentation resources. The XML alone does not establish that every entry is a video file. The meanings of `loc` and `sub` are especially tentative and should be confirmed by comparing the entries with actual game behavior or related resources.

### 3.2. Weapon-associated IDs

The final group uses IDs that match weapon class codes:

`GUN`, `SHOT`, `CROS`, `CLUB`, `BEAT`, `CBOW`, `TASE`, `CSAW`, `DYNA`, `UBFL`, `FLBA`, `UZI`, `FLBG`, and `FLGU`.

Example:

```xml
<kine id="GUN"
      width="256"
      height="256"
      rwidth="256"
      rheight="192"
      center="1"
      alpha="1" />
```

| Attribute | Tentative interpretation |
|---|---|
| `width`, `height` | Resource dimensions or base layout dimensions. |
| `rwidth`, `rheight` | Rendered, reference, or content dimensions. |
| `center` | Likely requests centering. |
| `alpha` | Likely enables or indicates alpha/transparency handling. |

Because these IDs overlap with weapon codes in `settings/toe`, they likely describe visual resources or presentation settings associated with those weapons. The exact type of resource—icon, preview, overlay, or something else—cannot be determined from this file alone.

## 4. `anim_files`: animation resource paths

```xml
<anim_files>
    <file path="Characters\Boy0\anims.zwo" />
    <file path="Characters\Boy1\anims.zwo" />
    <file path="Characters\Boy2\anims.zwo" />
    <file path="Characters\Boy3\anims.zwo" />
    <file path="Characters\Gir0\anims.zwo" />
    <file path="Characters\Gir1\anims.zwo" />
    <file path="Characters\Gir2\anims.zwo" />
    <file path="Characters\Gir3\anims.zwo" />
</anim_files>
```

This section lists eight `.zwo` animation resources, organized under four `Boy` directories and four `Gir` directories.

The supplied modding guide describes `.zwo` as a format used for models and animations in Obscure 1 and Obscure 2. The paths therefore appear to reference character animation resources. The precise correspondence between `Boy0`–`Boy3` / `Gir0`–`Gir3` and `BOY1`–`BOY4` / `GIR1`–`GIR4` remains unverified because the numbering differs.

## 5. `zoe_files`: resource directories

```xml
<zoe_files>
    <file path="Assets\Door\" />
    <file path="Assets\hcase\" />
    <file path="Assets\Weapons\" />
    <file path="Assets\Heart\" />
</zoe_files>
```

The section lists four directory paths:

- `Assets\Door\`
- `Assets\hcase\`
- `Assets\Weapons\`
- `Assets\Heart\`

These appear to be resource directories consumed by the game's engine or resource loader. The supplied modding guide mentions Zoe as a multiplatform 3D engine, but that does not by itself establish the exact meaning of the element name `zoe_files` or the contents of each directory.

## 6. What this file appears to tell us about the game

At a high level, `game.xmc` appears to bring together global configuration and references used by several systems:

- **Character state:** character IDs, life values, level IDs, position IDs, and controller codes.
- **Inventory catalogue:** item, document, and weapon definitions, with text IDs and behavior flags.
- **Progression:** save-point IDs and predefined chest contents.
- **Lighting:** a small set of lighting parameters.
- **Presentation:** sequence-like records and weapon-associated visual settings.
- **Resources:** paths to character animation files and other resource directories.

The supplied XML does **not** expose all gameplay logic. It does not show chest coordinates, complete weapon behavior, character AI, map geometry, or the full implementation of saving. Those details may be stored in other files or handled by the engine.

## 7. Suggested follow-up files for cross-referencing

To turn the tentative interpretations into better-supported documentation, inspect:

1. **`projects/chapters.xmc`** — to compare chapter, level, and progression identifiers.
2. **`characters/cbox.xmc` and `characters/combos.xmc`** — to investigate character-related configuration, collision boxes, and combat combinations, if their contents confirm those roles.
3. **`menus/inventory_pc.xmc` and `menus/menu_pc.xmc`** — to cross-reference item codes and inventory presentation.
4. **Text/localization resources (`.lng` or related tables)** — to resolve `string_id`, `inv_name_id`, and `desc_id` values to displayed names and descriptions.
5. **Weapon and item models under `loadpack/assets/weapons` and `cachpack/assets/items`** — to compare class codes with model names and textures.
6. **Level and resource files** — to determine whether save-point IDs, chest entries, and sequence IDs are referenced elsewhere.

Useful codes to search for across the files include `8500008`, `04500058`, `0C204001`, `AMFG`, `B101`, `CHC1`, and `CHTM`.

## 8. Documentation confidence and cautions

When documenting `.xmc` files, it is useful to label findings as:

- **Observed:** directly present in the XML, such as `nbMedikitMax="3"`.
- **Inferred:** a plausible interpretation based on naming or cross-file matches, such as `sub` possibly relating to subtitles.
- **Unknown:** not yet supported by evidence, such as the purpose of `attr_B3DFCA20`.

XML attribute order is not semantically significant. For example, reordering `id`, `life`, and `controller` in a `<character>` element does not change the element's XML meaning.

This document describes the supplied `game.xmc` XML dump and the accompanying modding notes. It should be updated as additional files or runtime evidence confirm the meaning of individual fields.
