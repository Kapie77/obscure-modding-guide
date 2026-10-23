# streams.xmc — Analysis

## Overview

The `streams.xmc` file is an audio-resource catalog for *Obscure 2*. It associates numeric identifiers and descriptive names with audio filenames, indicating whether each resource is configured as a beginning segment, a loop, or both.

The XML root element is `<streams>`, which contains 299 `<stream>` entries.

## Structure

Each `<stream>` entry may contain these attributes and child elements:

| Attribute or element | Description |
|---|---|
| `id` | Numeric identifier assigned to the audio resource. |
| `display` | Descriptive name, often associated with a chapter, location, character, or event. |
| `volume` | Numeric volume-related value. The exact scale and interpretation are not documented in this XML. |
| `<begin filename="..." />` | Reference to an audio file used as a beginning segment or as a non-loop entry. |
| `<loop filename="..." />` | Reference to an audio file configured for loop playback. |

An entry may contain only `begin`, only `loop`, or both. For example, `ch03_03_hall` contains both elements, while `ch03_04_stairs1` contains only `begin`.

## Entry Distribution

The 299 entries are distributed as follows:

| Configuration | Number of entries |
|---|---:|
| `begin` only | 143 |
| `loop` only | 120 |
| Both `begin` and `loop` | 36 |
| **Total** | **299** |

A total of 196 entries specify a `volume` attribute; 103 do not.

These figures describe the XML configuration and do not necessarily correspond to the number of distinct physical audio files in the game.

## Audio Categories and Context

Names in the `display` and `filename` attributes suggest several broad categories. These classifications are inferred from naming conventions and are not formally documented in the XML.

| Category | Examples | Likely context |
|---|---|---|
| Menus | `m_menu_l`, `m_save_l` | Main-menu and save-screen audio. |
| Chapter 1 | `ch01_01_extchambre`, `ch01_bt_01_grillons` | Environmental audio, music, and events. |
| Chapters 2–5 | `ch02_04_jardin_confrerie`, `ch04_04_river`, `ch05_12_jun_monster` | Environments, music, and narrative events. |
| Chapters 6–8 | `ch06_19_kennyboss_l`, `ch07_04_electricity_l`, `ch08_11_eau_l` | Character events, encounters, and environmental sounds. |
| Chapters 9–12 | `ch09_04_jeddidiah_attk`, `ch11_08_tunnel_jed`, `ch12_boss_l` | Narrative events, environments, and confrontations. |
| Character-specific sequences | `leo_background_l`, `kenny3_zik_1_b` | Audio associated with particular characters or situations. |
| Cinematic/video-related entries | `ch06_boss_temp_video`, `ch01_bt_video`, `ch04_video_corey` | Audio associated with scenes or video sequences. |

## Music, Ambient Audio, and Events

Several naming patterns suggest likely audio types:

- **Music:** names containing `zik`, `music`, `violons`, `choir`, or `theme`.
- **Ambient audio:** names containing `grillons` (crickets), `vent` (wind), `river`, `eau` (water), `lac` (lake), or `electricity`.
- **Narrative events:** names containing `scream`, `death`, or `attk` (possibly attack), as well as names associated with opening doors.
- **Character-related audio:** names such as `kenny`, `corey`, `sven`, `amy`, `jed`, and `leo`.

These are interpretations of the identifiers rather than verified descriptions of the actual audio content.

## Volume Values

The file contains negative `volume` values, including `-121`, `-529`, `-1024`, and `-10000`. The XML does not explain their scale or whether they represent decibels, internal attenuation values, or another audio-system convention.

Examples:

| ID | `display` | Volume |
|---:|---|---:|
| `1004` | `ch02_05_chat1girl` | `-10000` |
| `1021` | `ch03_02_cam_entering` | `-121` |
| `1003` | `ch02_04_jardin_confrerie` | `-841` |
| `1034` | `ch04_04_river` | `-1681` |
| `1047` | `ch05_08_residence` | `-3249` |

The value `-10000` appears in three entries. Its exact runtime meaning cannot be established from this file alone.

## Notable Details and Potential Anomalies

- **Mixed ID ranges:** the file uses IDs such as `1`–`124` and `1001`–`1180`, with gaps in the sequences. All 299 entries have distinct IDs.
- **Filename suffixes are not fully consistent:** many `begin` filenames end in `_b` and many `loop` filenames end in `_l`, but this is not universal.
- **Unusual suffix/element combinations:** `ch04_09_zik_volant` references `ch04_09_zik_volant_b` inside a `loop` element. `ch06_08_zik_aftermother` similarly uses a filename ending in `_b` within `loop`. These may be intentional or may reflect different naming conventions.
- **Names containing spaces:** examples include `ch09_01_avance jardin JEd` and `ch11_03_cour centrale`. Preserve these names exactly when searching for matching resources.
- **Potential encoding corruption:** `ch12_entr�e_confr�rie` and `ch12_mus�e_confrerie` contain replacement characters in the supplied XML text. Check the original file's encoding before attempting to correct these names.
- **Every entry references audio:** all 299 entries contain at least one `begin` or `loop` element.

## Conclusion

`streams.xmc` is a catalog of audio streams in *Obscure 2*. Its 299 entries connect numeric IDs and descriptive labels to audio filenames and, in many cases, volume-related values. The catalog covers menu music, ambient sounds, location-based audio, character events, and chapter-related sequences.

Further analysis of the referenced audio files and the game's audio playback code would be needed to confirm the actual content of each resource, the volume scale, and how `begin` and `loop` entries are played together.
