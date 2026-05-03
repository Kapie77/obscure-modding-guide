<div align="center">
  <h1 style="font-size: 28px; margin: 10px 0;">Obscure Modding Guide</h1>
  <p>Modification guide for all versions of Obscure 1, Obscure 2, and Final Exam.</p>
</div>

# Formats

| Format                   | What is it                           | Game                        |
|--------------------------|--------------------------------------|-----------------------------|
| .hvp                     |   Contains, in compressed form, the game files  | Obscure 1, Obscure 2, Final Exam        |
| .zwo                     |   Models (weapons, characters, map) and animations | Obscure 1, Obscure 2        |
| .dic/.dip                |   Textures                           | Obscure 1, Obscure 2, Final Exam        |
| .hvt                     |   Textures          | Obscure 2 (Wii), Final Exam       |
| .lng                     |   Texts and lines          | Obscure 1, Obscure 2, Final Exam        |
| .sub                     |   Video subtitles          | Obscure 1, Obscure 2        |
| .sav                     |   Save files          | Obscure 1, Obscure 2        |
| .pso                     |   Pixel shader          | Obscure 1, Obscure 2        |
| .vso                     |   Vertex shader          | Obscure 1, Obscure 2        |
| .xmc                     |   Used for the UI (.xmc is just a compiled XML file)         | Obscure 1, Obscure 2        |
| .hoe                     |   Events, collisions of the map of the room          | Obscure 1, Obscure 2        |
| .dat                     |   Holds data about a character or something similar the data includes files to load and their content like meshes, skeletons and animations          | Obscure 1        |
| .map                     |  I think it stores something related to objectives, NPCs, relations between rooms, etc but I'm not sure (and I'm not even sure they're used in the game) (there's a tool made by Ran-J that parses it, but he's not too sure it works properly)          | Obscure 1        |
| .cre                     |   Credits, it's just plain text          | Obscure 1       |
| .ipt                     |   Default inputs (keyboard and controller configs)          | Obscure 1        |
| .sen                     |   Plain text, mostly comments, and I don't know what the rest is (the comments are in french)          | Obscure 1        |
| .txe                     |             | Obscure 1        |
| .noe                     |   Physics file.          | Obscure 1        |
| .tm                     |   these files store information on the NPCs coordinates, the camera angles, the descriptions of the different things in the room that you can inspect (by pressing A/X/Enter) and the items (the parts of this format related to the items and the general structure can be found in the Drive folder and can be modified with my randomizer and my fileparser)          | Obscure 1        |


# Tools
## For game files
- [obscure-hvp](https://github.com/YouKnow-sys/obscure-hvp) - Cross-platform CLI tool for extracting .hvp files from Obscure 1, Obscure 2, and Final Exam.

## For models
- [zwoBlender](https://github.com/Al-Hydra/zwoBlender) - A Blender extension for importing and exporting models from Obscure 1 and 2, including characters, weapons, maps, etc, and animations. **The tool isn't 100% finished yet and needs a few fixes**.

## For textures
- [Obscure Textures Tool](https://github.com/Al-Hydra/zwoBlender/blob/main/zwoLib/texDict.py) - A tool for extracting and repacking textures from Obscure 1 and 2. **It does not yet support the Wii version and .hvt**.
- [ObsCure Texture Editor](https://github.com/HeitorSpectre/ObsCure-Texture-Editor) - A UI tool for accessing, extracting, editing, and repacking textures from Obscure 1, Obscure 2 and Final Exam.

## For texts
- [Obscure LNG Tool](https://github.com/Kapie77/Obscure-LNG-Tool) - A cross-platform CLI tool for extracting and editing text from Obscure 1 and 2.


## 010 Editor Templates
- [Obscure 010 Editor Templates](https://github.com/Al-Hydra/HydraVision-Obscure-010-Editor-Templates) - [010 Editor](https://www.sweetscape.com/010editor/) templates for Obscure 1 and 2 files.

## Frida scripts
- [Frida scripts for Obscure 2.](https://github.com/bartlomiejduda/Tools/tree/master/NEW%20Tools/ObsCure%202) - [Frida](https://github.com/frida/frida) scripts for Obscure 2.

## Map Parser
- [ObsCure 1 Map Parser](https://github.com/ran-j/obscure1-map-parser) - A desktop application for parsing and analyzing map files from Obscure 1.
