# `fx.xmc` Analysis

## Overview

`fx.xmc` is a configuration file for visual effects in *Obscure 2*. Its root element is `tag_9DF1BDF8`. The file defines named effects, their parameters and texture references, effect groupings, color sequences, and references to external custom-particle definition files.

The file contains general effect definitions, grouped effect types, post-processing settings, and numerous `pscustom` entries that reference external `.txt` files.

The interpretations below are based on the names and attributes in the supplied XML. The file alone does not document the engine's implementation.

## 1. General Effect Definitions

| Effect name | Notable attributes / child elements | Interpretation |
|---|---|---|
| `bloom` | `blurness="1.85"`, `luminosity="-0.2"`, `alpha="70"`, `contrast="1.35"` | Bloom or glow post-processing settings. |
| `electricity` | Textures `FX_Elec`, `FX_Elec_mini`; `alpha="additive"`; noise, map-scale, frame-count, and ribbon-width parameters | Electrical effect with texture references and animation/noise controls. |
| `electricity_bolt` | Texture `FX_Elec_bolt_texture` | Electrical bolt effect. |
| `tentacle_shadow` | Texture `fx_tentacle_shad` | Tentacle-related shadow effect. |
| `corpse_shadow` | `red="0"`, `green="0"`, `blue="0"` | Color parameters set to black; likely used for a corpse shadow. |
| `dark_aura_whirl` | Texture `fx_dark_aura_whirl` | Dark, swirling aura effect. |
| `water` | Texture `fx_water`; `GridWidth="10"`, `Size="1500"`, `WaveHeight="10"`, `WaveSpeed="2.0"`, `MapScale="4"` | Water surface effect with grid, size, and wave parameters. |
| `water_spec` | Texture `fx_water_spec`; `FadeOutDistStart="200"`, `MaxDist="700"`, `GridWidth="6"`, `Size="350"` | Water-specular or water-highlight effect with distance limits. |
| `display_noise` | Texture `fx_noise` | Noise overlay or display effect. |
| `water_droplet` | `texture_wave="fx_droplet_wave"`, `texture_splash="fx_droplet_splash"` | Water-droplet effect with wave and splash textures. |
| `floor_decal` | Texture `fx_explo_smoke`; `FadeInPos="0"`, `FadeOutPos="0.5"`, `Size="400"`, `PoolSize="10"`, `Duration="10"` | Floor decal using an explosion-smoke texture, with fade, size, pool, and duration settings. |
| `weapon_trail` | Texture `fx_fuse_light`; width, height, grid, and rigidity parameters | Weapon trail effect. |
| `flower_tentacle` | Texture `fx_flower_tntcl`; wave, growth, grid, count, length, and transition parameters | Animated or growing flower-tentacle effect. |
| `kenny_steam` | `textureJet="fx_kenny_steam_jet"`, `textureGaz="fx_kenny_steam_gaz"` | Steam effect with jet and gas textures, apparently associated with Kenny. |
| `tentacle_system` | Texture `fx_tentacle_system` | Tentacle system effect. |
| `spark` | Texture `fx_spark`; three child `<color>` elements | Spark effect with three color definitions. |
| `woodchip` | Texture `fx_woodchip`; four child `<color>` elements | Wood-chip effect with four color definitions. |

### Parameter Observations

- `bloom` has numeric values that appear to control blur, luminosity, alpha, and contrast.
- `electricity` includes an additive alpha mode and parameters that appear to control texture mapping, noise, animation frames, and ribbon width.
- `water` and `water_spec` use capitalized attribute names such as `GridWidth`, `Size`, and `MapScale`. Preserve this capitalization when documenting or editing the source.
- `flower_tentacle` contains the attributes `wavePeriode` and `lentght` as written in the XML. Their exact meaning is not established by this file.
- `spark` and `woodchip` define color sequences using child `<color>` elements with `red`, `green`, `blue`, and `alpha` attributes.

## 2. Effect Groups Using `<type>`

These entries group named effect types rather than defining a texture directly.

### `scene_impact`

Contains two types:

- `Junk`
- `ImpactMetal`

The names suggest effects for environmental or object impacts, including debris and metal impacts.

### `character_impact`

Contains ten types:

- `Blood`
- `BloodJet`
- `UziBlood`
- `UberBloodJet`
- `ChainsawBlood1`
- `ChainsawBlood2`
- `GunBlood`
- `BloodHead`
- `BloodSpot`
- `BloodSpray`

These are blood and character-impact effect identifiers, based on their names.

### `weapon_ps`

Contains fourteen types:

- `FlareSpark`
- `FlarePowder`
- `FlareSmoke`
- `FlareSmokeTrail`
- `FlareMain`
- `ShotGunDust`
- `FlashBallDust`
- `FlashBallDust2`
- `FlashBallHeat`
- `ExplosionDust`
- `ExplosionSmoke`
- `ExplosionSpot`
- `ExplosionHeat`
- `ExplosionFlame`

This group includes names associated with flares, shotgun dust, flash-ball effects, and explosion particles.

## 3. Other Settings

| Entry | Attributes | Interpretation |
|---|---|---|
| `flash_light` | Texture `fx_light_glow` | Light-glow effect. |
| `torch_flare` | `m_FacingCameraMaxAngle="0.25"`, `m_FacingCameraFadeStartAngle="0.5"`, fade-in/out durations of `1000` | Torch-flare behavior with camera-angle and fade parameters. |
| `saturation` | `value="208"` | Saturation setting or value. The scale is not specified in this file. |

## 4. Custom Particle Definitions (`pscustom`)

The file contains numerous entries named `pscustom`. Each uses its `value` attribute to reference a `.txt` file. These appear to be external particle-effect definitions, but the XML does not describe the text-file format or its internal parameters.

The following groups are based on filename themes. They are descriptive conveniences, not categories explicitly declared by the XML.

### Vapor, Smoke, and Steam

- `vapor.txt`
- `vapor2.txt`
- `vapor3.txt`
- `vapor4.txt`
- `smog.txt`
- `smog2.txt`
- `steamt.txt`
- `steamt2.txt`
- `steamt3.txt`
- `steamt4.txt`
- `steam_part1.txt`
- `steam_part2.txt`
- `SteamBreath.txt`
- `FallSteam.txt`
- `FxSteamBroke.txt`
- `ElecSmoke.txt`
- `ChainsawSmoke.txt`
- `ExplosionSmoke.txt`
- `FlareSmoke.txt`
- `FlareSmokeTrail.txt`

### Blood and Gore

- `blood.txt`
- `bloodHead.txt`
- `bloodSpray.txt`
- `bloodSpot.txt`
- `BloodPiece.txt`
- `BloodJet.txt`
- `UberBloodJet.txt`
- `UziBlood.txt`
- `GunBlood.txt`
- `ChainsawBlood.txt`
- `ChainsawBlood1.txt`
- `ChainsawBlood2.txt`
- `ChainsawBlood3.txt`
- `ChainsawBloodJet.txt`
- `MothProgBlood.txt`
- `NeoLeoBloodJet.txt`
- `ProgBlood.txt`

### Impacts, Debris, and Breakage

- `break1.txt`
- `wbreakfalldust.txt`
- `wbreakbasedust.txt`
- `wbreakjunk.txt`
- `junk.txt`
- `ImpactMetal.txt`
- `dustfoot.txt`
- `ProgPiece.txt`
- `MothProgPiece.txt`
- `FxGravas.txt`
- `FxEboulis.txt`
- `FxEboulis2.txt`
- `FxGlassL.txt`
- `Fxpuppetbreak.txt`
- `FxK003grav1.txt`
- `FxK003grav2.txt`
- `ChainsawWoodChipJet.txt`

### Explosions, Heat, and Weapons

- `explose_aura.txt`
- `ExplosionDust.txt`
- `ExplosionHeat.txt`
- `ExplosionFlame.txt`
- `ExplosionSpot.txt`
- `FlareMain.txt`
- `FlareSpark.txt`
- `FlarePowder.txt`
- `DAExplosionMain.txt`
- `FlashBallHeat.txt`
- `FlashBallDust.txt`
- `FlashBallDust2.txt`
- `ShotGunDust.txt`
- `brulure.txt`

### Water, Falls, and Splashes

- `BerkSplash.txt`
- `FallSplash.txt`
- `FallSplash2.txt`
- `Fxwaterfall.txt`
- `Fxwaterimpact.txt`
- `Fxwaterspeed.txt`
- `FxDroplet2.txt`

### Electricity and Environmental Effects

- `ElecGround.txt`
- `ElecEdge.txt`
- `FxLeaf.txt`
- `Fx_Fog.txt`
- `FxExtinc.txt`
- `spore.txt`
- `Fx_spore.txt`
- `Fxkenny01.txt`
- `Fxkenny02.txt`
- `Fxkenny03.txt`
- `Fxkenny04.txt`

The XML also references additional particle files, including `Fx_Fog.txt`, `Fx_spore.txt`, and various explosion, blood, steam, and environmental effects. Original filename capitalization is preserved where listed.

## 5. Summary

`fx.xmc` acts as a visual-effects registry. It defines rendering and environmental effects, named groups of impact and weapon particle types, color data for selected effects, and references to custom particle definitions stored in `.txt` files.

Texture names and parameter values provide useful leads for locating associated assets and investigating how the game configures each effect.

## Limitations

- The XML does not define the implementation or units for most numeric parameters.
- Texture references do not establish the exact appearance or in-game use of an effect.
- The meaning of the root element `tag_9DF1BDF8` is not established by this file.
- The external `.txt` files are referenced but their contents are not included, so their particle configurations cannot be analyzed from this XML alone.