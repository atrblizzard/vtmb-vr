# Vampire the Masquerade: Bloodlines VR

An unofficial, experimental VR mod for **Vampire: The Masquerade - Bloodlines**,
targeting the 32-bit game with **Unofficial Patch 11.5**. Explore Los Angeles in
stereoscopic first person with tracked head movement, motion-controller aiming,
two-handed weapon support, first-person feeding, and controller-operated menus,
dialogue and computer terminals.

The mod uses a Direct3D 9 proxy with DXVK and supports **SteamVR / OpenVR** and
**native OpenXR**, including a Virtual Desktop VDXR launch option. VR is opt-in
with `-vr`; `-nohmd` overrides it.

> Status: **0.5 preview**. The full tutorial has been played through with
> SteamVR on Valve Index and Oculus headsets: shooting, melee, feeding, hacking,
> dialogue, menus and inventory. Other SteamVR headsets should work but are
> less tested. Native OpenXR and Virtual Desktop (VDXR) are experimental. See
> the [0.5 release notes](RELEASE-NOTES-0.5-preview.md) for what changed.

## Features

### Stereo rendering and head tracking

- Stereoscopic world rendering with 6DOF head tracking, headset-recommended eye
  sizes, IPD, asymmetric eye fields of view and canted-eye projection support.
- Pose-tagged frame submission and GPU frame transfer through DXVK/Vulkan.
- Configurable solid-world head clearance to reduce leaning through walls.
  This constrains the rendered head position; it does not move the player body.
- Smooth or snap turning, recentering, world-scale/IPD adjustment and stair-camera
  smoothing. Ordinary gameplay stays in first person by default.
- Stick-heading movement by default, with optional headset-relative or
  controller-relative walking and an optional analog movement mode.
- Separate camera modes for dialogue, hacking and scripted tracks: retain the
  authored camera, allow free head rotation at its position, or use player-eye
  position. Native scene timing and interaction rules continue to apply.
  All three default to the authored camera with head tracking (mode 0).
- Stealth kills keep the native cinematic by default, with optional free head
  look or player-eye position.
- Optional 2D cutscenes: scripted camera tracks and stealth kills render once on
  a stationary screen with their native camera angles, and stereo resumes when
  the shot ends. Disabled by default.

### Weapons, hands and body

- Tracked weapon placement and controller aiming, with configurable handedness,
  six-axis calibration and optional one-handed aim smoothing.
- Two-handed aiming: hold the offhand grip while supporting the weapon. Strength,
  support distance and smoothing are adjustable; valid support consumes the grip
  press so it does not also reload or crouch.
- Per-weapon calibration profiles, optional calibrated support-grip sockets and
  a virtual shoulder stock for supported rifle/SMG aiming.
- World-depth weapon rendering and an optional traced weapon-aim reticle.
- A tracked offhand, textured GLB hand assets when supplied, fallback hand
  rendering and procedural trigger/grip finger curls. These curls are not
  skeletal finger tracking.
- Native arm IK with reach clamping, stretch limits and elbow smoothing. It
  targets right-handed firearms; left-handed mode keeps the simpler hand rendering.
- Native torso/legs, head hiding, body alignment and world-weapon attachment.
  Native arms, the visible body and world weapons are enabled by default as the
  tested configuration, and each can be turned off.
- Native melee, kick and block animations retain control during attacks;
  controller takeover resumes at idle. Damage and attack timing remain native.
- Experimental controller-origin ranged shooting with obstruction clamping,
  disabled by default. Without it, controller aim does not relocate the game's
  native shot origin. This is a calibrated controller anchor, not a muzzle socket.

### Feeding, disciplines and interaction

- First-person feeding through the bite, drinking and release, with free head
  look and adjustable distance from the victim. The body keeps its native feeding
  animation and head, and the camera returns to your previous first- or
  third-person view afterwards. Other native grapples using the same driver are
  covered too. The stock feeding cinematic can be restored.
- Five configurable custom command actions for feeding, discipline casting,
  hotkeys and other native game commands.
- Controller dialogue navigation with the left stick and trigger/Menu Select,
  including numbered responses and skipping the current NPC line.
- Dialogue uses the regular HUD in the default dialogue camera mode 0. In modes
  1 and 2 it is placed beside the NPC in world space and turns to face you while
  staying upright; unavailable targets fall back to the HUD.
- Controller dismissal of tutorial and sign popups using their native close path.
- A custom terminal keyboard with pointer typing, Backspace, Enter, Escape and
  **Hack (Ctrl-C)**. Grab its move bar to reposition it beside the terminal.

### Menus, HUD and configuration

- Stationary curved menu surfaces, adjustable distance/width/curvature and
  optional head-following placement, with controller pointing and clicking.
- Inventory, weapon/armor selectors, barter, hotkeys, character sheet/quests,
  map, item information and tutorial/note panels can preserve the stereo world
  behind their native UI.
- Stereo native 3D model previews, including character creation. Text and buttons
  remain on the panel; opaque menus/loading retain their screen presentation.
- Adjustable overall HUD scale and placement, plus individual health, blood,
  dialogue and notification layouts.
- Wrist/centered shortcut menu, the game's ten-slot hotkey wheel, and optional
  configurable body-position command zones. Shortcut actions may need binding.
- In-headset settings for comfort, interface, weapons, hands, controllers and HUD.
- Live configuration reload, console commands and persistent saving.
- Controller trigger feedback and optional UI/support-grip pulses. These are
  input feedback, not confirmed shot/hit events or external vest/gunstock effects.
- Desktop recording view with a cropped right-eye scene and full-size native HUD,
  with optional crosshair hiding; no additional world render is needed.
- Diagnostic logs, optional performance logging and native regression probes.

### Keyboard and mouse

- Keyboard and mouse play in the headset, chosen automatically when no controller
  is tracked at startup or set under **Controller > Input mode**. The game's own
  bindings, sensitivity and inversion are kept.
- Head tracking stays independent of mouse aim; mouse pitch aims without tilting
  the world. The game's **Toggle Camera** key (Z) switches first and third person.
- In first person, unarmed and melee attacks show the game's own rotating target
  marker at the aim point, replacing the centre crosshair while it is shown.
- An arrow pointer on menu and stereo panels, direct typing into hacking
  terminals, **F10** for VR settings and **F11** to recenter.

## Requirements

- Windows and a Vulkan-capable GPU/driver compatible with the bundled DXVK path.
- A licensed installation of **Vampire: The Masquerade - Bloodlines** with
  **Unofficial Patch 11.5**. Hooks and signatures target its 32-bit binaries;
  other executable/patch combinations are not a compatibility guarantee.
- A tracked VR headset and motion controllers, using either SteamVR/OpenVR or
  a compatible **32-bit OpenXR runtime with Vulkan support**.

Controller profiles and runtime support do not establish tested compatibility
for every headset. SteamVR and native OpenXR should be checked separately.

## Install and launch

1. Obtain a complete Bloodlines VR package, or build and use
   `stage/Bloodlines-Release` from the implementation source checkout.
2. Back up existing root-level mod DLLs and your `VR` configuration/bindings.
3. Copy the complete package beside `Vampire.exe`: `d3d9.dll`, `openvr_api.dll`,
   `openxr_loader.dll` and the `VR` directory, including its action manifests,
   controller bindings and supplied hand assets. Preserve existing
   `Bin/loader/loader.ini` and `Bin/d3d9.dll`.
4. Keep the Unofficial Patch launch argument and add the VR arguments below.
   Windowed mode is recommended; the console is useful for configuration.

**SteamVR / OpenVR:** start SteamVR, then launch with:

```text
Vampire.exe -game Unofficial_Patch -vr -console -novid -window -w 1920 -h 1080
```

**Native OpenXR:** select a compatible OpenXR runtime, then launch with:

```text
Vampire.exe -game Unofficial_Patch -vr -openxr -console -window -w 1920 -h 1080
```

**Virtual Desktop / VDXR:** connect the headset through Virtual Desktop and use:

```text
Vampire.exe -game Unofficial_Patch -vr -openxr -vdxr -console -window -w 1920 -h 1080
```

`-vdxr` selects the Streamer's Win32 runtime manifest for this process without
changing system registration. The OpenXR path still needs the packaged
`openvr_api.dll` as a linked dependency, but does not start an OpenVR session.

To play without VR, omit `-vr` or add `-nohmd`. To uninstall, remove the files
added by the package and restore anything backed up before installation.

## Controls

These are the shipped Touch/Index conventions; saved or custom SteamVR bindings
can override them. SteamVR actions are editable in its controller binding editor.
Native OpenXR custom gameplay actions use `OpenXRCustomAction1Binding` through
`OpenXRCustomAction5Binding` in `VR/config.txt`.

| Input/action | Gameplay / UI behavior |
| --- | --- |
| Left stick | Walk; navigate menus/dialogue |
| Right stick horizontal | Smooth or snap turn |
| Right stick vertical | Previous/next item |
| Weapon-hand trigger | Primary attack; pointer click; confirm dialogue or hurry NPC speech |
| Other trigger | Native secondary attack / melee block |
| Right A / B (Touch and Index) | Jump / use; menu select / back |
| Left X (Touch) / left A (Index) | Cast selected discipline |
| Left Y (Touch) / left B (Index) | Pause / centered shortcut menu, according to UI state |
| Left stick click | Feed in gameplay with the shipped custom action; recenter in menus |
| Right stick click | Switch weapon/discipline selection side |
| Left grip / right grip | Reload / crouch unless consumed by two-handed support |
| Offhand grip in a valid support stance | Two-handed aiming |
| Pause held + Recenter action | Toggle in-headset VR settings |
| BodyShortcut action | Activate a nearby body shortcut or open the wrist menu |
| Keyboard F10 / F11 | Toggle VR settings / recenter headset and panels |

The Index default assigns BodyShortcut to left thumbpad force press. Touch
requires a binding if you want that action. Face buttons/sticks retain their
physical-hand assignments when handedness changes; weapon/support roles swap.
If feeding owns left stick click, bind the separate Recenter action where needed
or run `vr_settings` from the console to open settings.

Release buttons and center sticks when entering/leaving dialogue, terminals,
menus or after tracking/focus loss. Held actions require release before gameplay
input resumes. Melee is driven by native attack/block commands; there are no
physical punch, grenade-throw or magazine-pull reload gestures.

## Configuration

Settings live in `VR/config.txt`. File edits reload automatically. Use the
in-headset settings panel or the game console for live changes:

```text
vr_settings
vr_config
vr_config SnapTurning true
vr_config LeftHanded true
vr_config MenuDistanceMeters 1.5
vr_config DialogueCameraMode 2
vr_save
```

`vr_config <name>` reads one setting; `vr_config <name> <value>` changes it.
Changes remain session-only until `vr_save`. `vr_reload` reloads the file and
`vr_reload_hands` reloads hand assets. Enable the console with `-console`.

Optional features that are disabled by default: `ControllerShootingEnabled`,
`AnalogMovementEnabled`, `Cutscenes2D` and `VirtualStockEnabled` (the shipped
MAC-10 weapon profile turns the stock on for that weapon). The tested defaults
enable `NativeArmIK`, `NativeBodyVisible`, `NativeBodyWorldWeapon`,
`FingerAnimationEnabled`, `BodyShortcutsEnabled`, `FirstPersonFeeding`,
`DialogueWorldAnchorEnabled` and `DialogueWorldFacePlayer`; set the first three
to `false` for simpler hand rendering.

`DialogueCameraMode`, `HackingCameraMode`, `CameraTrackMode` and
`StealthKillCameraMode` all default to `0`: the game's authored camera (with head
tracking) and the native stealth-kill cinematic. Mode `1` keeps the authored
position with free head look, and mode `2` uses your own eye position. World
dialogue beside the NPC needs dialogue mode `1` or `2`. Back up personal settings
and custom bindings before replacing a package.

## Reporting bugs

Open an issue at [github.com/atrblizzard/vtmb-vr/issues](https://github.com/atrblizzard/vtmb-vr/issues).
Include the game/Unofficial Patch version, mod build, headset, controller type,
runtime (OpenVR/OpenXR/VDXR), launch arguments and reproduction steps. Attach
`vrmod_log.txt` (it is cleared on every launch, so copy it before starting the
game again) and relevant configuration/binding details. Describe whether the
problem occurs in gameplay, dialogue, a terminal, menus, loading or after
focus/tracking loss. Include a save or screenshot when it helps reproduce it.

## Credits

Built on DXVK, the OpenVR/OpenXR SDKs, MinHook, Dear ImGui and cgltf, and
derived from [L4D2VR](https://github.com/sd805/l4d2vr). Exact per-eye projection,
head collision and GPU timing were adapted from
[Spec Ops: The Line VR](https://github.com/Mavic-Pro/SpecOpsTheLineVR) by
Mavic-Pro, with ideas from other community VR projects. Respect the
licenses and attribution accompanying each dependency and any supplied assets.

Vampire: The Masquerade - Bloodlines belongs to its respective rights holders.
This is an unofficial community project and requires the original game.

## Donations

If you've enjoyed Bloodlines VR or want to support my other work, including
Project Embrace, you can contribute through Patreon or Ko-Fi.

Support is entirely optional and comes with my sincere thanks.
There are no perks for Bloodlines VR, though Project Embrace offers its own
supporter benefits.

[Ko-Fi](https://ko-fi.com/atrblizzard)
[Patreon](https://patreon.com/atrblizzard)
[Buy Me a Coffee](https://buymeacoffee.com/atrblizzard)