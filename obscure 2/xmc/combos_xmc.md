# `combos.xmc` --- Weapon and Combat Combo Definitions

## Overview

`combos.xmc` defines weapon parameters and combat attack sequences. Its
root element is `tag_9927918E`, containing two main sections:

-   `<weapons>`: per-weapon configuration, including targeting/lock
    parameters, animation identifiers, ammunition, dimensions, teammate
    timing, and power values.
-   `<combos>`: attack sequences associated with weapon types, including
    animation IDs, hit definitions, timing windows, damage values,
    directional vectors, and conditions for chaining attacks.

The file contains 16 weapon definitions and 27 top-level combo
definitions. Nested combo elements bring the total to 46 `<combo>`
elements.

## Structural inventory

  Element / property                                Count or value
  ----------------------------------------------- ----------------
  Root element                                      `tag_9927918E`
  `<weapons>` sections                                           1
  `<weapon>` definitions                                        16
  `<combos>` sections                                            1
  Top-level `<combo>` definitions                               27
  All `<combo>` elements, including nested ones                 46
  `<anim>` elements inside combos                               46
  `<hit>` elements inside combos                                45
  `<boy>` timing/configuration elements                         43
  `<gir>` timing/configuration elements                         43
  `<dir>` direction vectors                                     52
  `weapons/@DMGMax`                                        `700.0`

The `DMGMax="700.0"` value is declared on the `<weapons>` element. The
XML does not explain how this limit is applied.

## 1. Weapon definitions

There are 16 distinct `weaponType` values:

`CSAW`, `CROS`, `CLUB`, `BEAT`, `UBET`, `CBOW`, `DYNA`, `FLGU`, `FLBA`,
`FLBG`, `FLAS`, `GUN`, `SHOT`, `TASE`, `UBFL`, and `UZI`.

### 1.1 Configuration coverage

  ------------------------------------------------------------------------------
  Weapon      Lock     Animation   Ammunition   Dimension    Power     Teammate
  type                    set                                           timing
  -------- ---------- ----------- ------------ ----------- ---------- ----------
  `CSAW`      Yes         Yes         Yes          Yes        Yes         No

  `CROS`      Yes         Yes          No          Yes        Yes         No

  `CLUB`      Yes         Yes          No          Yes        Yes         No

  `BEAT`      Yes         Yes          No          Yes        Yes         No

  `UBET`      Yes         Yes          No          Yes        Yes         No

  `CBOW`      Yes         Yes         Yes          No         Yes         No

  `DYNA`      Yes         Yes         Yes          No          No        Yes

  `FLGU`      Yes         Yes         Yes          No         Yes         No

  `FLBA`      Yes         Yes         Yes          No         Yes         No

  `FLBG`      Yes         Yes         Yes          No         Yes        Yes

  `FLAS`       No         Yes          No          No          No         No

  `GUN`       Yes         Yes         Yes          No         Yes         No

  `SHOT`      Yes         Yes         Yes          No         Yes         No

  `TASE`      Yes         Yes         Yes          Yes        Yes         No

  `UBFL`      Yes         Yes         Yes          No         Yes         No

  `UZI`       Yes         Yes         Yes          No         Yes         No
  ------------------------------------------------------------------------------

Counts across the weapon definitions:

-   15 weapons have a `<lock>` element; `FLAS` does not.
-   All 16 have an `<anims>` element.
-   11 have an `<ammos>` element.
-   14 have a `<power>` element; `DYNA` and `FLAS` do not.
-   Six have a `<dim>` element.
-   Two have a `<teammate>` element: `DYNA` and `FLBG`.

### 1.2 Weapon dimensions

Only six weapon definitions contain a `<dim>` element:

  Weapon type     `length`
  ------------- ----------
  `CSAW`           `150.0`
  `CROS`           `175.0`
  `CLUB`           `175.0`
  `BEAT`           `175.0`
  `UBET`           `175.0`
  `TASE`           `150.0`

The XML does not specify the unit used by `length`.

### 1.3 Lock and targeting parameters

Most weapon definitions include a `<lock>` element. Common attributes
include:

-   `distance`
-   `fightDistance`
-   `deltaZMin` and `deltaZMax`
-   `angleMin` and `angleMax`
-   `lockBreakables`
-   `fightDistanceMin`
-   `maxDamageDistance`

The values vary by weapon. For example:

  --------------------------------------------------------------------------
  Weapon type     `distance`   `fightDistance`    `deltaZMin`    `deltaZMax`
  ----------- -------------- ----------------- -------------- --------------
  `CSAW`             `500.0`           `200.0`        `-50.0`        `250.0`

  `CROS`             `500.0`           `200.0`        `-50.0`        `500.0`

  `CBOW`            `1500.0`           `500.0`       `-150.0`       `1000.0`

  `FLGU`            `1500.0`           `400.0`       `-150.0`       `1000.0`

  `GUN`             `1500.0`           `350.0`       `-150.0`       `1000.0`

  `SHOT`            `1000.0`           `250.0`       `-150.0`       `1000.0`

  `TASE`            `1500.0`           `400.0`       `-150.0`       `1000.0`
  --------------------------------------------------------------------------

This table shows selected attributes only; it is not a complete
representation of every `<lock>` element.

Most lock definitions contain separate `<boy>` and `<gir>` child
elements. These provide character-specific values such as `lockH` and,
in some cases, `clavFactor`. The values are not identical between the
two elements. `FLAS` has no lock definition, so it has no such entries
here.

### 1.4 Animation identifiers

Each weapon has an `<anims>` element, but the attributes differ. The
file uses identifiers for animation roles such as:

-   `wrist`
-   `fold`
-   `lock`
-   `lockStart`
-   `reload`
-   `light`

Some entries also define reload timing attributes, such as
`reloadTime0`, and the `SHOT` definition includes multiple reload times
and ammunition-reload counters.

Examples from the XML:

  -----------------------------------------------------------------------
  Weapon type                         Animation identifiers / attributes
  ----------------------------------- -----------------------------------
  `CSAW`                              `wrist="CSWR"`, `fold="CSFO"`,
                                      `lock="CSLK"`

  `CBOW`                              `reload="CBRE"`, `lock="CBLK"`,
                                      `wrist="CBWR"`, `fold="CBFO"`

  `FLGU`                              `reload="FGRE"`, `light="LIGU"`,
                                      `fold="GUFO"`, `lock="GULK"`,
                                      `wrist="GUWR"`

  `GUN`                               `light="LIGU"`, `reload="GURE"`,
                                      `lock="GULK"`, `fold="GUFO"`,
                                      `wrist="GUWR"`

  `SHOT`                              `reload="SGRE"`, `fold="SGFO"`,
                                      `wrist="SGWR"`, `light="LISH"`,
                                      `lock="SGLK"`

  `TASE`                              `lock="GULK"`, `wrist="GUWR"`,
                                      `fold="GUFO"`, `light="LIGU"`,
                                      `reload="GURE"`

  `UZI`                               `reload="UZRE"`, `fold="UZFO"`,
                                      `wrist="UZWR"`, `light="LIGU"`,
                                      `lock="UZLK"`
  -----------------------------------------------------------------------

These are animation/resource identifiers, not the animation data
themselves. Their actual content is not included in this XML.

### 1.5 Ammunition parameters

Eleven weapons have an `<ammos>` element. Attributes used in these
definitions include `nb`, `nbLimit`, `type`, `damage`, `DMG`,
`damageRadius`, and `attackRate`.

  -----------------------------------------------------------------------
  Weapon type                         Values explicitly declared in
                                      `<ammos>`
  ----------------------------------- -----------------------------------
  `CSAW`                              `nb="0.0"`

  `CBOW`                              `nb="2.0"`, `nbLimit="2"`,
                                      `damage="125"`, `type="AMCR"`,
                                      `damageRadius="250.0"`

  `DYNA`                              `damage="180"`,
                                      `damageRadius="800.0"`,
                                      `nbLimit="3"`

  `FLGU`                              `nbLimit="9"`, `type="AMFG"`,
                                      `attackRate="500"`, `damage="10"`,
                                      `DMG="65.0"`, `nb="1.0"`

  `FLBA`                              `type="AMFB"`, `nb="4.0"`,
                                      `nbLimit="12"`, `DMG="15.0"`,
                                      `damage="30"`

  `FLBG`                              `damage="250"`, `nbLimit="3"`,
                                      `damageRadius="800.0"`

  `GUN`                               `nbLimit="21"`, `nb="7.0"`,
                                      `DMG="15.0"`, `attackRate="650"`,
                                      `type="AMGU"`

  `SHOT`                              `DMG="32.5"`, `nb="5.0"`,
                                      `type="AMSH"`, `nbLimit="10"`,
                                      `attackRate="1000"`

  `TASE`                              `nb="5.0"`

  `UBFL`                              `nb="5.0"`

  `UZI`                               `nbLimit="90"`, `DMG="5.0"`,
                                      `nb="30.0"`, `type="AMUZ"`
  -----------------------------------------------------------------------

The XML contains both `damage` and `DMG` attributes. They are preserved
as separate fields here; the file does not explain whether they
represent different calculations or contexts.

### 1.6 Power values

Fourteen weapons define a `<power>` element. Its attributes refer to
categories such as `NPCBoss`, `NPCStunned`, `NPCHeavy`, `NPCStrong`,
`NPCNormal`, `NPCWeak`, and `PJUsingTaser`.

These are category-specific numeric values, not necessarily directly
comparable damage values. For example:

-   `CSAW`: `NPCStunned="9"`, `NPCStrong="4"`, `NPCHeavy="1"`,
    `NPCNormal="7"`, `PJUsingTaser="9"`, `NPCWeak="9"`.
-   `CBOW`: `NPCBoss="6"`.
-   `GUN`: values are provided for boss, stunned, normal, strong, and
    heavy NPC categories.
-   `TASE`: values are provided for strong, heavy, normal, and stunned
    NPC categories.

`DYNA` and `FLAS` have no `<power>` element in this file.

### 1.7 Teammate timing

Two weapons define a `<teammate>` element:

  Weapon type   Attribute
  ------------- -------------------------
  `DYNA`        `attackInterval="5000"`
  `FLBG`        `attackInterval="5000"`

The XML does not state the time unit or describe the runtime behavior
controlled by this interval.

## 2. Combat combo definitions

The `<combos>` section contains 27 top-level `<combo>` elements. Because
some combos contain nested `<combo>` elements, there are 46 combo
elements in total.

Each combo is associated with a `weaponType`. Many contain:

-   `<anim>`: animation identifier and optional animation parameters.
-   `<hit>`: hit type, damage, and character-specific timing/direction
    data.
-   Nested `<combo>` elements: additional steps in a sequence.

There are 46 `<anim>` elements and 45 `<hit>` elements. The `UBFL` combo
is a notable exception: its definition contains an animation but no
`<hit>` element.

### 2.1 Top-level combo distribution

  Weapon type     Top-level combo definitions
  ------------- -----------------------------
  `CSAW`                                    3
  `CROS`                                    3
  `CLUB`                                    3
  `BEAT`                                    3
  `UBET`                                    3
  `DYNA`                                    2
  `FLBG`                                    2
  `GUN`                                     1
  `FLGU`                                    1
  `UZI`                                     1
  `TASE`                                    1
  `CBOW`                                    1
  `FLBA`                                    1
  `SHOT`                                    1
  `UBFL`                                    1
  **Total**                            **27**

The nested combo trees are especially prominent for `CROS`, `CLUB`,
`BEAT`, and `UBET`.

### 2.2 Animation attributes

The `<anim>` elements use attributes including:

-   `id`: animation identifier.
-   `onHighBody`: present on several firearm-related entries.
-   `recenterOnTarget`: present on many melee/combat entries.
-   `animReturn`: return-animation identifier.
-   `timeFactor`: animation timing factor.

Examples of animation IDs include:

`gu1a`, `uz1a`, `gu1b`, `cba1`, `sga1`, `cs1a`, `cs1b`, `cs4a`, `cs2a`,
`cs2b`, `ca4a`, `ca1a`, `ca1b`, `ca1c`, `ca1d`, `ca3a`, `ca3b`, `da2c`,
`da1c`, and `ub1a`.

The IDs are referenced by the combo definitions; the corresponding
animation assets are not embedded in this XML.

### 2.3 Hit definitions

The `<hit>` elements use attributes such as:

-   `type`
-   `damage`

The file includes hit types `1`, `2`, `3`, `4`, `5`, `101`, `200`,
`201`, and `202`.

Examples of explicitly declared damage values include:

  Weapon / combo context                  Hit type   Damage
  ------------------------------------- ---------- --------
  `GUN`                                      `200`     `15`
  `UZI`                                      `202`     `50`
  Nested `TASE` combo                        `101`      `5`
  Nested `CSAW` combo                          `5`     `50`
  `CSAW` combo with `ZDiffMax="61.0"`          `3`     `20`
  `CROS` close-range combo                     `3`     `15`
  `CROS` middle-range opening hit              `2`      `7`
  `CLUB` middle-range opening hit              `2`      `7`
  `BEAT` middle-range opening hit              `2`      `7`
  `UBET` middle-range opening hit              `2`      `9`

Not every `<hit>` declares a `damage` attribute. Some nested combo
animations also carry a `damage` attribute, which is distinct from the
attributes on `<hit>` elements and should not be assumed to have the
same meaning without runtime evidence.

### 2.4 Character-specific hit timing and direction

Many `<hit>` elements contain `<boy>` and `<gir>` children. These can
define:

-   `hitTime0` and `hitTime1`: timing boundaries.
-   `hitAngle0` and `hitAngle1`: angle boundaries.
-   `<dir>`: directional vector with `X`, `Y`, and `Z` components.

The file contains 43 `<boy>` elements, 43 `<gir>` elements, and 52
`<dir>` elements. Not every character-specific element has a `<dir>`
child.

The values can differ between `boy` and `gir`, including hit windows and
direction vectors. Therefore, the two sets of parameters should be
documented separately rather than treated as identical.

## 3. Combo conditions and chaining

Combo elements can declare conditions and control attributes, including:

-   `ZDiffMin` and `ZDiffMax`
-   `delayMin` and `delayMax`
-   `stayPressed` and `stayPressedTime`
-   `justPressed` and `justUnPressed`
-   `stayLocked`
-   `loop`
-   `randomCheckRange`
-   `testLockDistance` and `lockDistanceMax`

These attributes are used in different combinations throughout the file.

### 3.1 Vertical-difference ranges

The `CROS`, `CLUB`, `BEAT`, and `UBET` combo groups each have three
top-level definitions using these ranges:

  Range condition   Values
  ----------------- ---------------------------------------
  Upper bound       `ZDiffMax="61.0"`
  Middle range      `ZDiffMin="60.0"`, `ZDiffMax="180.0"`
  Lower bound       `ZDiffMin="179.0"`

`CSAW` also has a top-level combo with `ZDiffMax="61.0"`, but its other
two top-level definitions do not declare these range attributes.

The small overlaps between the numeric boundaries (`60.0`/`61.0` and
`179.0`/`180.0`) are present in the XML and should not be silently
normalized.

### 3.2 Nested attack sequences

Several weapon types use nested combos to define follow-up attacks.

-   `CSAW`: includes a looping/stay-pressed sequence and a two-step
    sequence using `cs2a` and `cs2b`.
-   `CROS`: includes a middle-range chain using `ca1a`, `ca1b`, and
    alternative follow-up branches `ca1c` and `ca1d`.
-   `CLUB`: uses a similar `ca1a` → `ca1b` structure, with `ca1c` and
    `ca1d` follow-up branches.
-   `BEAT`: also uses the `ca1a`, `ca1b`, `ca1c`, and `ca1d` animation
    sequence.
-   `UBET`: uses the same general animation-ID pattern for its
    middle-range chain, with its own hit values and timing.
-   `TASE`: contains a nested follow-up combo using `gu1b`.
-   `DYNA` and `FLBG`: each define two top-level actions with `da2c` and
    `da1c`.
-   `UBFL`: defines a looping, stay-pressed animation using `ub1a`,
    without a `<hit>` element.

The repeated animation IDs do not mean the associated attacks are
identical: their weapon types, timing, hit types, damage, and direction
data can differ.

### 3.3 Random follow-up branches

The melee chains for `CROS`, `CLUB`, `BEAT`, and `UBET` contain nested
follow-up combos with `randomCheckRange="2"` and `randomCheckRange="3"`.

This indicates that the XML provides multiple conditional follow-up
definitions. The exact selection algorithm is not specified in the file.

### 3.4 Lock-distance checks

The `DYNA` and `FLBG` combo definitions include entries with:

-   `testLockDistance="1"`
-   `lockDistanceMax="800.0"`

Their other entries use `justPressed="0"` and `justUnPressed="1"`
without those lock-distance attributes.

The XML records these conditions but does not define the code that
evaluates them.

## 4. Important observations

1.  `combos.xmc` is both a weapon-configuration file and a
    combat-sequence file; it is not limited to combo animation names.
2.  The 16 weapon definitions do not all expose the same configuration
    fields. `FLAS`, for example, contains only an animation set.
3.  Weapon ammunition fields distinguish `damage` from `DMG`; both
    spellings occur in the source.
4.  The combo system uses nested `<combo>` elements to represent
    multi-step attacks and follow-up branches.
5.  Character-specific hit timing and direction data are explicitly
    represented for `boy` and `gir`.
6.  Some combo definitions use spatial conditions (`ZDiffMin`,
    `ZDiffMax`) while others use button-state, delay, loop, or
    lock-distance conditions.
7.  The XML references animation IDs and ammunition type IDs, but does
    not include the corresponding animation or ammunition resource
    definitions.

## 5. What the XML does not establish

The file does not independently explain:

-   The real-world names or descriptions associated with each
    `weaponType` code.
-   The units used for distances, dimensions, angles, damage, or timing
    values.
-   The exact formula behind `power`, `DMGMax`, `damage`, and `DMG`.
-   The implementation of targeting, lock acquisition, hit detection, or
    combo selection.
-   The meaning of every hit `type` value.
-   The actual content of the referenced animation IDs.
-   The runtime meaning of every combo condition or how random branches
    are selected.

Those details would require additional game resources, executable/code
analysis, or controlled runtime testing.

## Conclusion

`combos.xmc` is a central data definition for weapon behavior and combat
sequences. It describes 16 weapon types with differing targeting,
animation, ammunition, dimension, teammate, and power settings. Its
combo section contains 27 top-level definitions and 46 combo elements
overall, including nested attack chains, character-specific hit windows,
directional vectors, and conditional follow-ups. The file provides
substantial combat configuration data, but does not include the
implementations or assets that interpret these values.
