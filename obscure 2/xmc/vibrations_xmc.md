# vibrations.xmc — Analysis

## Overview

The `vibrations.xmc` file defines vibration configurations associated with animation identifiers. It contains shared vibration entries and additional configurations specific to individual characters.

The XML root element is `tag_F9090459`, with two main sections: `common` and `specific`.

## Structure

### `common`

Contains shared vibration configurations. Each `vibration` entry may include the following attributes:

| Attribute | Description |
|---|---|
| `anim_id` | Identifier associated with an animation or event. Its exact meaning is not confirmed. |
| `lintensity` | Likely represents left-side controller vibration intensity. |
| `rintensity` | Likely represents right-side controller vibration intensity. |
| `start` | Likely represents the vibration's start offset or delay. |
| `duration` | Vibration duration. The unit is unknown. |
| `priority` | Priority value associated with the vibration. Its behavior is undocumented. |

Not every entry necessarily uses the same parameter values. Some entries use zero values, while others specify different intensities, start offsets, durations, and priorities.

### `specific`

Contains character-specific vibration configurations.

The analyzed file includes entries for the following characters:

**BOY1**
- `3C1A`: start 600, duration 200, left intensity 8, right intensity 0, priority 4.
- `JCF1`: start 0, duration 957, left intensity 10, right intensity 1, priority 5.
- `JCF2`: start 0, duration 3960, left intensity 10, right intensity 1, priority 5.

**BOY4**
- `HCLE`: start 0, duration 2200, left intensity 6, right intensity 0, priority 6.
- `HCPL`: start 850, duration 1500, left intensity 7, right intensity 0, priority 5.
- `HCRA`: start 2200, duration 900, left intensity 8, right intensity 1, priority 4.
- `HCRI`: start 0, duration 1500, left intensity 6, right intensity 0, priority 5.

## Animation Identifiers

The `anim_id` values identify individual animation-related entries. Examples found in the file include:

- `HIT1`–`HIT9`
- `HI10`–`HI18`
- `HI20`–`HI22`
- `DMG1`
- `DMG2`
- `DIE1`
- `SGA1`
- `SGA3`
- `UZ1A`
- `CS3A`
- `RTFN`
- `COLD`

Identifiers such as `HIT`, `DMG`, and `DIE` may suggest hit, damage, and death-related events, respectively. These interpretations are inferred from their names and have not been confirmed against the game's executable or source code.

## Observations

- The `common` section provides shared vibration definitions.
- The `specific` section contains additional entries for `BOY1` and `BOY4`.
- Some identifiers appear in both sections with different intensity values. For example, `JCF1` and `JCF2` have left intensity 11 in their common entries and intensity 10 in the `BOY1` entries.
- This may indicate character-specific adjustments or overrides, but the game's actual configuration-merging behavior is unknown.
- The `priority` attribute may affect how simultaneous vibration events are handled, but this has not been verified.
- The meaning of the intensity scale, the time units, and the exact relationship between animation events and vibration playback remain undetermined.

## Conclusion

`vibrations.xmc` is a configuration file for animation-associated controller vibration. It defines vibration parameters in a shared section and provides character-specific configurations for selected characters.

Further investigation of the game's executable, animation resources, or runtime behavior would be required to confirm the exact meaning of each attribute and how the game applies these configurations.