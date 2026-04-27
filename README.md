# Source Engine Resources Viewer (SERV)

**Source Engine Resources Viewer**, usually shortened to **SERV**, is a fan-made Windows tool suite for viewing, inspecting, browsing, and launching different kinds of Source Engine resource files.

SERV is designed for people who work with, study, organize, test, or inspect files from Source Engine games and Source-based projects. It brings a collection of separate resource tools together under one native Hub, while still keeping each viewer and inspector as its own standalone program.

> **SERV is a fan-made utility suite. It is not affiliated with Valve, Steam, or any official Source Engine development team.**

---

## Current Release

**Current public build:** `SERV Beta 2`  
**Build direction:** Full native C++ / Qt recode  
**Release type:** Beta / public test release  
**Platform:** Windows

SERV Beta 2 is a major rewrite of the older Python-based SERV tool suite. The new version uses native C++ applications, Qt-based interfaces, and dedicated DLL backends for many tools.

This release is meant to be the new foundation for SERV going forward.

---

## Downloads

### Installer

Use this if you want SERV installed like a normal Windows program.

**Download SERV Beta 2 Setup:**

https://github.com/sonicFanTech/SourceEngineResourcesViewer/releases/download/B2/SERV.BETA.2.SETUP.exe

### Portable Build

Use this if you want to extract SERV into a folder and run it without installing.

**Download SERV Beta 2 Portable:**

https://github.com/sonicFanTech/SourceEngineResourcesViewer/releases/download/B2/SERV_PB2.7z

---

## About SERV

SERV is a collection of Source Engine resource utilities. Instead of having one giant program trying to do everything, SERV is built as a hub with many separate tools.

The Hub is used to organize, detect, launch, and manage tools. The viewers and inspectors are separate executables inside the `Tools` folder.

This makes SERV easier to maintain because each tool can be updated, replaced, fixed, or expanded without needing to rebuild the entire suite.

SERV can be used for things like:

- Browsing Source Engine archives.
- Inspecting map, model, texture, material, script, sound, scene, and resource files.
- Viewing metadata from Source Engine formats.
- Previewing supported assets.
- Extracting readable references from binary files.
- Building launch options for Source games.
- Playing or inspecting Source demo files.
- Organizing Source Engine research and development utilities in one place.

SERV is especially useful for modders, Source Engine fans, tool developers, archive explorers, and people who want a cleaner way to inspect Source Engine game files.

---

## SERV Beta 2 / C++ Recode

Beta 2 is not just a small update. It is a large recode of SERV into native C++ tools.

The older Python version helped prove the idea of SERV, but the new C++ version is meant to be faster, cleaner, more stable, and easier to expand.

### Main Beta 2 goals

- Rebuild the SERV Hub in C++.
- Rebuild most old Python tools as C++ tools.
- Use a cleaner `Tools` folder layout.
- Use metadata files so the Hub can detect tools automatically.
- Move format-specific logic into DLLs.
- Keep the tool EXEs focused mostly on UI.
- Make each tool easier to update without breaking the rest of SERV.
- Improve long-term performance and maintainability.

### What changed compared to the older Python version

- The Hub is now a native C++ / Qt application.
- Tools are now native C++ / Qt applications.
- Many tools have their own custom management DLLs.
- Tool detection is handled through `tool.servtool.json`.
- The folder structure is cleaner.
- Tools are grouped into Viewers, Inspectors, and Other utilities.
- Most old tools have been remade.
- Some tools are still early prototypes and will continue improving over time.

---

## Important Status Notes

SERV Beta 2 is working, but it is still a beta.

Some tools are more complete than others. Some tools are currently inspectors rather than full viewers. Some advanced features, like full Source model rendering or demo playback handling, may still need more work.

Known Beta 2 notes:

- **MDL Viewer / Inspector** can inspect models and attempt real mesh rendering, but full Source model rendering and texture resolving are still experimental.
- **DEMO Player / Inspector** can inspect demos and launch a Source game with `playdemo`, but playback behavior depends on the game, demo location, and Source branch.
- **PCF Inspector** currently focuses on extracting readable particle-related strings and references. Full binary PCF/DMX parsing is planned for later.
- **SAV Inspector** is a general binary/save inspector and may not fully decode every game’s save format.
- **SWATCH Inspector** and **EXE/DLL Inspector** are not remade in C++ yet.

---

## Tool Suite Overview

SERV Beta 2 currently includes the following major tools:

| Tool | Type | Status | Purpose |
|---|---|---:|---|
| SERV Hub | Hub | Working | Launches and organizes all SERV tools |
| VPK Browser | Viewer | Working | Opens and browses Valve VPK archive files |
| VTF Viewer | Viewer | Working | Opens and previews Valve Texture Format files |
| VMT Viewer | Viewer / Inspector | Working | Opens and parses Valve material files |
| Source BSP Explorer | Viewer | Working / Beta | Views and inspects Source BSP map files |
| MDL Viewer / Inspector | Viewer / Inspector | Experimental | Inspects and previews Source model files |
| VMF Viewer / Inspector | Viewer / Inspector | Working | Opens and inspects Hammer VMF map source files |
| NUT Viewer / Inspector | Inspector | Working | Opens and inspects Squirrel script files |
| VCD Viewer / Inspector | Inspector | Working | Opens and inspects Source choreography scene files |
| PCF Inspector | Inspector | Working / Early | Inspects particle system files |
| SND Inspector | Inspector | Working | Inspects sound scripts and audio metadata |
| RES Inspector | Inspector | Working | Inspects Source resource/reference files |
| SAV Inspector | Inspector | Working | Inspects save/binary files and readable strings |
| Launch Options Builder | Utility | Working | Builds Source/Steam launch command options |
| DEMO Player / Inspector | Inspector / Player shell | Working / Experimental | Inspects and launches demo playback |

---

# SERV Hub

The **SERV Hub** is the main launcher and management program for SERV.

It scans the `Tools` folder, reads tool metadata files, checks dependencies, displays tool status, and launches selected tools.

The Hub itself does not try to parse every Source file format. Instead, it launches the correct tool for the job.

## Hub features

- Native C++ / Qt interface.
- Tool list with categories.
- Tool metadata support.
- Tool status checking.
- Missing dependency warnings.
- Search/filtering.
- Open selected tool folder.
- Launch selected tool.
- About and legal sections.
- Support for hidden/internal tools.
- Support for broken-tool detection.
- Designed around a clean multi-tool folder layout.

## Hub categories

Tools are usually organized into categories like:

- Viewers
- Inspectors
- Other
- Broken
- Hidden/Internal

The Hub reads the category from each tool’s `tool.servtool.json` file.

---

# Tool Metadata

Each SERV tool should include a metadata file named:

```text
tool.servtool.json
```

The Hub uses this file to identify and launch the tool.

Example:

```json
{
  "id": "VTFViewer",
  "name": "VTF Viewer",
  "version": "0.1.0",
  "category": "Viewers",
  "type": "viewer",
  "executable": "VTFViewer.exe",
  "description": "Open, inspect, preview, and export Valve Texture Format files.",
  "icon": "icon.png",
  "working_dir": ".",
  "args": [],
  "hidden": false,
  "requires": [
    "VALVETEXManagement.dll"
  ],
  "supported_files": [
    ".vtf"
  ],
  "developer": "sonic Fan Tech"
}
```

## Important metadata fields

### `id`

A unique internal identifier for the tool.

### `name`

The display name shown in the SERV Hub.

### `version`

The current tool version.

### `category`

The Hub category.

Recommended categories:

```text
Viewers
Inspectors
Other
```

### `type`

The tool type, such as:

```text
viewer
inspector
utility
hub
```

### `executable`

The executable file the Hub should launch.

### `description`

A short explanation of what the tool does.

### `requires`

A list of DLLs or files that should exist beside the tool.

The Hub can use this to show missing dependency warnings.

### `supported_files`

File extensions supported by the tool.

---

# Folder Layout

A normal SERV Beta 2 folder may look like this:

```text
SERV/
├─ SERV Hub.exe
├─ SERVManagement.dll
├─ Tools/
│  ├─ Viewers/
│  │  ├─ VPKBrowser/
│  │  ├─ VTFViewer/
│  │  ├─ VMTViewer/
│  │  ├─ SourceBSPExplorer/
│  │  ├─ MDLViewer/
│  │  └─ VMFViewer/
│  ├─ Inspectors/
│  │  ├─ NUTViewer/
│  │  ├─ VCDViewer/
│  │  ├─ PCFInspector/
│  │  ├─ SNDInspector/
│  │  ├─ RESInspector/
│  │  ├─ SAVInspector/
│  │  └─ DEMOPlayerInspector/
│  └─ Other/
│     └─ LaunchOptionsBuilder/
├─ legal/
├─ config/
└─ logs/
```

Each tool folder usually contains:

```text
ToolName/
├─ ToolName.exe
├─ tool.servtool.json
├─ required custom DLLs
├─ Qt runtime DLLs
└─ platforms/
   └─ qwindows.dll
```

---

# VPK Browser

The **VPK Browser** is used to open and inspect Valve VPK archives.

VPK archives are commonly used by Source Engine games to store materials, models, sounds, scripts, maps, particles, scenes, and other game content.

## Features

- Opens `.vpk` files.
- Supports `_dir.vpk` style archive sets.
- Displays folder and file structure.
- Shows file metadata where possible.
- Supports searching/filtering.
- Supports extracting selected files.
- Supports extracting visible/filtered files.
- Helps locate materials, textures, models, scripts, sounds, and maps.

## Example use cases

- Browse Portal 2 VPK files.
- Extract a `.vmt` or `.vtf` file for inspection.
- Find model references.
- Search for scripts, scenes, or sound files.
- Extract resources needed by another SERV tool.

## DLL

The VPK Browser uses:

```text
VALVE-PK_Management.dll
```

This DLL handles VPK archive management and file listing logic.

---

# VTF Viewer

The **VTF Viewer** opens and previews Valve Texture Format files.

VTF files are Source Engine texture files. They are often referenced by VMT material files.

## Features

- Opens `.vtf` files.
- Reads VTF header information.
- Shows texture dimensions.
- Shows version information.
- Shows mipmap count.
- Shows texture format.
- Displays supported texture previews.
- Allows mipmap selection.
- Exports the current preview as PNG.

## Supported texture formats

Prototype support includes common formats such as:

- DXT1
- DXT3
- DXT5
- RGBA8888
- ABGR8888
- ARGB8888
- BGRA8888
- RGB888
- BGR888
- I8
- A8

Support may improve over later builds.

## DLL

The VTF Viewer uses:

```text
VALVETEXManagement.dll
```

This DLL handles VTF header parsing and image decoding.

---

# VMT Viewer

The **VMT Viewer** opens Valve Material Type files.

VMT files describe how Source Engine textures and materials should behave. They often point to VTF textures through keys like `$basetexture`.

## Features

- Opens `.vmt` files.
- Shows raw VMT text.
- Parses shader name.
- Parses material key/value pairs.
- Detects common material keys.
- Shows material details.
- Detects `$basetexture`.
- Detects `$bumpmap`.
- Detects `$surfaceprop`.
- Detects `$envmap`.
- Detects transparency-related settings.
- Attempts to find matching VTF files.
- Exports a material summary.

## Useful keys

Common VMT keys include:

```text
$basetexture
$bumpmap
$surfaceprop
$envmap
$translucent
$alphatest
$phong
$selfillum
```

## DLL

The VMT Viewer uses:

```text
VALVE-MAT_Management.dll
```

This DLL handles VMT parsing and material summary logic.

---

# Source BSP Explorer

**Source BSP Explorer** is used to open, inspect, and view Source Engine BSP map files.

BSP files are compiled map files used by Source Engine games.

## Features

Exact features may depend on the current SBSPE build, but the tool is intended for:

- Opening `.bsp` files.
- Viewing map information.
- Inspecting lumps.
- Inspecting entities.
- Inspecting textures/materials.
- Viewing map geometry.
- Testing or launching maps in Source games.
- Exporting or analyzing map resources.

## Supported files

```text
.bsp
```

## Notes

SBSPE is one of the larger SERV tools and may have more complex dependencies than smaller inspectors.

When adding it to SERV Hub, make sure its `tool.servtool.json` file points to the correct executable and required DLLs.

---

# MDL Viewer / Inspector

The **MDL Viewer / Inspector** opens Source Engine model files.

Source models are more complex than many other Source formats because the visible model data is split across multiple companion files.

## Source model file set

A typical Source model may use:

```text
model.mdl
model.vvd
model.dx90.vtx
model.dx80.vtx
model.sw.vtx
model.phy
```

The `.mdl` file contains the model header and metadata.  
The `.vvd` file contains vertex data.  
The `.vtx` files contain mesh/strip information.  
The `.phy` file contains physics/collision data.

## Features

- Opens `.mdl` files.
- Reads MDL header information.
- Detects companion files.
- Shows model name.
- Shows version.
- Shows checksum.
- Shows counts such as bones, textures, body parts, hitboxes, and sequences.
- Provides an OpenGL preview panel.
- Attempts real mesh loading from VVD and VTX files.
- Falls back to a bounds/cube preview when full mesh loading fails.
- Includes a texture/material browser window.
- Exports a model summary.

## Experimental features

The following areas are still experimental:

- Full Source model mesh assembly.
- Correct VTX strip handling.
- Texture resolving.
- VMT/VTF loading for models.
- Material preview.
- Accurate rendering across all Source branches.

## DLLs

The MDL Viewer uses multiple DLLs so different parts can be updated separately:

```text
VALVE-MDL_Core.dll
VALVE-MDL_Mesh.dll
VALVE-MDL_RenderSupport.dll
VALVE-MDL_Material.dll
VALVE-MDL_Texture.dll
VALVE-MDL_VVD.dll
VALVE-MDL_VTX.dll
VALVE-MDL_PHY.dll
```

## Why so many DLLs?

Source models are complicated. Splitting the backend into multiple DLLs keeps the EXE mostly focused on the GUI and OpenGL viewer, while each DLL handles a different part of model support.

---

# VMF Viewer / Inspector

The **VMF Viewer / Inspector** opens Hammer VMF map source files.

VMF files are text-based map source files used by Valve Hammer Editor.

## Features

- Opens `.vmf` files.
- Shows raw VMF text.
- Parses VMF block structure.
- Shows VMF tree view.
- Shows selected node properties.
- Counts entities.
- Counts solids.
- Counts sides.
- Counts materials.
- Counts visgroups, cameras, and cordons.
- Lists material references.
- Lists entity classes.
- Supports text search.
- Exports a VMF summary.

## Example use cases

- Inspect a Hammer map source file.
- Find all material references.
- Count map entities.
- Look through brush/solid information.
- Search for specific entity classes.

## DLL

The VMF Viewer uses:

```text
VALVE-VMF_Management.dll
```

---

# NUT Viewer / Inspector

The **NUT Viewer / Inspector** opens Squirrel `.nut` script files.

Some Source and Source-based games use Squirrel scripts for gameplay logic, scripted events, tools, or game-specific behavior.

## Features

- Opens `.nut` files.
- Shows raw script text.
- Provides simple syntax highlighting.
- Extracts function names.
- Extracts class names.
- Extracts include/require-like references.
- Detects TODO/FIXME/HACK comments.
- Shows script statistics.
- Shows a symbol tree.
- Shows a symbol table.
- Allows jumping near symbol lines.
- Exports a script summary.

## DLL

The NUT Viewer uses:

```text
VALVE-NUT_Management.dll
```

---

# VCD Viewer / Inspector

The **VCD Viewer / Inspector** opens Source choreography scene files.

VCD files are used by Source Engine games for scenes, dialogue, gestures, facial animation timing, actor events, and choreography data.

## Features

- Opens `.vcd` files.
- Shows raw VCD scene text.
- Parses actors.
- Parses channels.
- Parses events.
- Parses timing values where possible.
- Extracts referenced sounds.
- Extracts scene text/caption-like strings where possible.
- Shows a scene tree.
- Shows an event table.
- Shows a referenced sounds list.
- Supports searching.
- Exports a scene summary.

## DLL

The VCD Viewer uses:

```text
VALVE-VCD_Management.dll
```

---

# PCF Inspector

The **PCF Inspector** inspects Source particle system files.

PCF files are often binary particle files, commonly used for effects like smoke, sparks, explosions, glows, portals, energy effects, and other visual effects.

## Features

- Opens `.pcf` files.
- Extracts readable strings.
- Detects possible particle system names.
- Detects possible operators.
- Detects possible renderers.
- Detects material and texture-related strings.
- Shows string offsets.
- Shows type hints.
- Supports search/filtering.
- Exports a PCF summary.

## Notes

Full PCF parsing may require deeper binary DMX-style parsing. Prototype 0.1 focuses on useful inspection and string extraction.

## DLL

The PCF Inspector uses:

```text
VALVE-PCF_Management.dll
```

---

# SND Inspector

The **SND Inspector** inspects Source sound script files and some audio files.

Source sound scripts define sound names and properties used by games.

## Features

- Opens Source sound script files.
- Parses sound entries.
- Shows channel.
- Shows sound level.
- Shows volume.
- Shows pitch.
- Shows wave references.
- Opens WAV files and reads RIFF/WAVE metadata.
- Performs basic MP3/ID3 detection.
- Extracts readable strings from binary files.
- Supports raw text search.
- Exports a sound summary.

## DLL

The SND Inspector uses:

```text
VALVE-SND_Management.dll
```

---

# RES Inspector

The **RES Inspector** opens Source resource/reference files.

RES files can contain references to materials, sounds, models, scenes, scripts, and other files.

## Features

- Opens `.res` files.
- Shows raw RES text.
- Extracts quoted key/value pairs.
- Guesses reference types.
- Groups references by category.
- Supports search/filtering.
- Shows selected entry details.
- Exports a summary.

## Reference categories

The inspector may identify:

- Material
- Texture
- Model
- Sound
- Scene
- Particle
- Script
- UI Resource
- Other

## DLL

The RES Inspector uses:

```text
VALVE-RES_Management.dll
```

---

# SAV Inspector

The **SAV Inspector** opens save files and unknown binary files for inspection.

Different games use different save formats, so this tool focuses on metadata, readable strings, references, and hex preview rather than full game-specific decoding.

## Features

- Opens `.sav`, `.dat`, `.bin`, and unknown binary files.
- Shows file/header metadata.
- Detects save-like headers where possible.
- Extracts readable ASCII strings.
- Detects probable embedded paths/references.
- Shows reference type guesses.
- Shows hex preview.
- Supports string search/filtering.
- Exports a summary.

## Possible reference types

- Map
- Model
- Material/Texture
- Sound
- Steam/User data
- Save data
- Other

## DLL

The SAV Inspector uses:

```text
VALVE-SAV_Management.dll
```

---

# Launch Options Builder

The **Launch Options Builder** helps create Source and Steam launch option strings.

It is useful for testing mods, launching games with custom settings, debugging, changing display modes, or building reproducible launch commands.

## Features

- Builds Source/Steam launch option strings.
- Provides common presets.
- Supports display/window mode options.
- Supports developer/debug options.
- Supports insecure/mod testing options.
- Allows selecting a game EXE.
- Allows selecting a game folder.
- Allows enabling/disabling options in a table.
- Allows editing option values.
- Allows adding custom launch options.
- Shows a live command-line preview.
- Copies command line to clipboard.
- Exports a launch summary.
- Includes basic profile save/load placeholder.
- Shows warnings for conflicting, legacy, or risky options.

## DLL

The Launch Options Builder uses:

```text
VALVE-LAUNCH_Management.dll
```

---

# DEMO Player / Inspector

The **DEMO Player / Inspector** opens Source demo files and can help launch demo playback in a Source game.

Source demo files usually use the `.dem` extension.

## Inspector features

- Opens `.dem` files.
- Reads Source demo header fields where possible.
- Shows map name.
- Shows game directory.
- Shows server name.
- Shows client name.
- Shows demo protocol.
- Shows network protocol.
- Shows tick count.
- Shows frame count.
- Shows playback time.
- Shows signon length.
- Extracts readable strings from binary demo data.
- Guesses referenced maps, sounds, models, materials/textures, and console/CVar strings.
- Shows a hex preview.
- Exports a summary.

## Playback features

- Select Source game EXE.
- Select working directory.
- Select game/mod folder.
- Add extra launch arguments.
- Toggle common launch options.
- Build a `+playdemo` command.
- Copy launch command.
- Play selected demo.
- Manage demo playlists in a separate window.
- Save/load playlist files.

## Playback notes

Demo playback depends on the game and Source branch.

Some Source games do not like absolute paths passed to `playdemo`. The DEMO tool may copy the selected demo to the game/mod folder and launch playback by demo name instead.

Example command style:

```text
-game "portal2" -console -novid +playdemo "demo"
```

If a demo does not play:

- Make sure the demo is from the same game.
- Make sure the correct game EXE is selected.
- Make sure the working directory is correct.
- Try copying the `.dem` file into the game folder.
- Try launching the game manually and running `playdemo demoname`.
- Check the game console for errors.

## DLL

The DEMO Player / Inspector uses:

```text
VALVE-DEMO_Management.dll
```

---

# Remaining Tools Not Yet Remade

Most of the old SERV tool list has now been remade in C++.

The remaining tools not yet remade are:

```text
SWATCH Inspector
EXE/DLL Inspector
```

These may be added in a future SERV update.

---

# Common Workflows

## Browse a game archive and open a texture

1. Open SERV Hub.
2. Launch VPK Browser.
3. Open a game `_dir.vpk`.
4. Search for a `.vtf` file.
5. Extract the `.vtf`.
6. Launch VTF Viewer.
7. Open the extracted texture.
8. Export a PNG if needed.

## Inspect a material

1. Launch VMT Viewer.
2. Open a `.vmt` file.
3. Check the shader name.
4. Check `$basetexture`.
5. Use VTF Viewer to inspect the matching texture.

## Inspect a model

1. Launch MDL Viewer / Inspector.
2. Open a `.mdl` file.
3. Make sure matching `.vvd`, `.vtx`, and `.phy` files are nearby.
4. Check model counts and companion file status.
5. Use the preview panel.
6. Open the texture/material browser if needed.

## Inspect a map source file

1. Launch VMF Viewer / Inspector.
2. Open a `.vmf` file.
3. Browse the tree.
4. Check entity classes.
5. Check material references.
6. Export a summary if needed.

## Build Source launch options

1. Launch Launch Options Builder.
2. Select the game EXE.
3. Select the game folder.
4. Enable desired options.
5. Add custom options if needed.
6. Copy the generated command.

## Play a demo

1. Launch DEMO Player / Inspector.
2. Open a `.dem` file.
3. Open the Playback window.
4. Select the correct game EXE.
5. Select the correct working directory and game/mod folder.
6. Click play.
7. Check the Source console if playback does not begin.

---

# Troubleshooting

## The Hub does not show a tool

Check that the tool folder contains:

```text
tool.servtool.json
```

Also check that:

- The JSON file is valid.
- There is no trailing comma.
- The `executable` value matches the EXE name.
- The category is correct.
- `hidden` is not set to `true`.
- The file is inside a scanned `Tools` folder.

## A tool says a DLL is missing

Make sure the required DLLs listed in `tool.servtool.json` are next to the tool EXE.

Example:

```text
VTFViewer.exe
VALVETEXManagement.dll
```

## A Qt tool does not open

Make sure the Qt runtime files are present.

Common required files include:

```text
Qt6Core.dll
Qt6Gui.dll
Qt6Widgets.dll
platforms/qwindows.dll
```

OpenGL-based tools may also need:

```text
Qt6OpenGL.dll
Qt6OpenGLWidgets.dll
```

## MDL model opens but only shows a box

That means the MDL header loaded, but the full mesh could not be assembled.

Check for companion files:

```text
.mdl
.vvd
.dx90.vtx
.phy
```

The MDL renderer is still experimental.

## MDL model has no textures

Make sure the related material and texture files are available.

Typical layout:

```text
materials/models/.../texture.vmt
materials/models/.../texture.vtf
```

Texture resolving is still experimental and may not work for every model yet.

## DEM file opens but playback does not start

Try:

- Selecting the correct game EXE.
- Selecting the correct game folder.
- Selecting the correct `-game` folder.
- Copying the demo into the game folder.
- Running `playdemo demoname` manually in the game console.
- Checking if the demo was recorded in the same game and game version.

---

# Legal / Third-Party Notes

SERV is a fan-made tool suite.

SERV is not affiliated with Valve, Steam, or any official Source Engine development team.

Some included or optional third-party tools may have their own licenses, permissions, or redistribution notes. Check the `legal` folder and any included third-party documentation for details.

Valve, Source, Steam, Half-Life, Portal, Team Fortress, Counter-Strike, and related names are property of their respective owners.

---

# Closed Source Notice

SERV is a closed-source project.

This repository and release page are for public downloads, documentation, release notes, and issue tracking where applicable.

Source code, build instructions, and compile instructions are intentionally not included.

---

# Project Status

SERV Beta 2 is a major milestone for the project.

It is now a native C++ / Qt tool suite with a rewritten Hub and many remade tools. Some tools are still prototype-level, but the suite is functional and ready for wider beta testing.

Future updates may focus on:

- Improving MDL mesh rendering.
- Improving MDL texture resolving.
- Improving DEM playback and playlist behavior.
- Adding SWATCH Inspector.
- Adding EXE/DLL Inspector.
- Improving VPK extraction workflows.
- Improving Hub tool icons and dependency checking.
- Reducing warnings and improving DLL interfaces.
- Adding more documentation and examples.
- Improving installer and portable deployment.

---

## Credits

Developed by **sonic Fan Tech**.

SERV exists because Source Engine files are interesting, useful, and fun to explore.
