# `cbox.xmc` --- Character CBE Resource References

## Overview

`cbox.xmc` is a resource-reference list. Its root element is
`tag_920227DB`, and its 22 `<cbe>` entries each point to a `.cbe` file
through the `path` attribute.

The file does not define character properties, animations, behavior,
visual settings, or gameplay logic. It only identifies resource paths.

## Structural inventory

  ------------------------------------------------------------------------
  Element                                      Count Notes
  --------------------- ---------------------------- ---------------------
  Root element                                     1 `tag_920227DB`

  `<cbe>` entries                                 22 Each contains one
                                                     `path` attribute

  Distinct base names                             13 Names before any
                                                     `_fx_elec` suffix

  Base resource entries                           13 Entries without
                                                     `_fx_elec`

  `_fx_elec` variant                               9 Additional paths with
  entries                                            the electric-effect
                                                     suffix
  ------------------------------------------------------------------------

## Referenced resources

  Base name   Base resource     `_fx_elec` variant
  ----------- ----------------- -------------------------
  `shom`      `shom\shom.cbe`   `shom\shom_fx_elec.cbe`
  `ogre`      `ogre\ogre.cbe`   `ogre\ogre_fx_elec.cbe`
  `homm`      `homm\homm.cbe`   `homm\homm_fx_elec.cbe`
  `ram`       `ram\ram.cbe`     `ram\ram_fx_elec.cbe`
  `fly`       `fly\fly.cbe`     `fly\fly_fx_elec.cbe`
  `boy0`      `boy0\boy0.cbe`   Not listed
  `moth`      `moth\moth.cbe`   `moth\moth_fx_elec.cbe`
  `prog`      `prog\prog.cbe`   `prog\prog_fx_elec.cbe`
  `ken1`      `ken1\ken1.cbe`   Not listed
  `ken2`      `ken2\ken2.cbe`   Not listed
  `ken3`      `ken3\ken3.cbe`   Not listed
  `jedi`      `jedi\jedi.cbe`   `jedi\jedi_fx_elec.cbe`
  `nleo`      `nleo\nleo.cbe`   `nleo\nleo_fx_elec.cbe`

## Variant coverage

Nine base names have a corresponding `_fx_elec` resource:

-   `shom`
-   `ogre`
-   `homm`
-   `ram`
-   `fly`
-   `moth`
-   `prog`
-   `jedi`
-   `nleo`

Four base names have no `_fx_elec` entry in this file:

-   `boy0`
-   `ken1`
-   `ken2`
-   `ken3`

This only describes which paths are present in `cbox.xmc`. It does not
prove that the corresponding variants are absent from the game or from
other resource lists.

## Directory organization

Each resource is stored in a directory named after its base name. The
base resource uses the same name for both its directory and filename,
for example:

``` text
shom\shom.cbe
```

The electric-effect variant, where listed, is stored in the same
directory and adds `_fx_elec` to the filename:

``` text
shom\shom_fx_elec.cbe
```

The XML uses Windows-style backslashes in all paths.

## Interpretation and limitations

The `_fx_elec` suffix strongly suggests an association with an electric
visual or effect variant, but the XML does not describe what the effect
contains or when it is used. The meaning of the base names (`shom`,
`ogre`, `homm`, and so on) is also not defined here.

The file does not provide:

-   Character display names or descriptions.
-   A mapping between these resource names and in-game character IDs.
-   Animation lists, skeletons, meshes, or material definitions.
-   Conditions for selecting the `_fx_elec` variants.
-   Any information about the internal contents of the referenced `.cbe`
    files.

Those details would require examination of the `.cbe` resources or other
game data.

## Conclusion

`cbox.xmc` acts as a compact index of 22 character-related `.cbe`
resource paths. It lists 13 base resources, nine of which have a
matching `_fx_elec` variant. Four entries (`boy0`, `ken1`, `ken2`, and
`ken3`) appear only as base resources in this file. No character
behavior or detailed resource metadata is defined in the XML itself.
