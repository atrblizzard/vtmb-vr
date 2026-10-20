# Bloodlines VR 0.5 preview

VR for *Vampire: The Masquerade – Bloodlines* with Unofficial Patch 11.5.

**Tested:** the full tutorial with SteamVR on Valve Index and Oculus headsets: shooting,
melee, feeding, hacking, dialogue, menus and inventory. Other SteamVR headsets should
work, but are less tested. **Native OpenXR (`-vr -openxr`) and Virtual Desktop (`-vr -openxr -vdxr`) are
experimental.**

**Requirements:** Windows, a Vulkan-capable GPU, a licensed copy of the game with
Unofficial Patch 11.5, and SteamVR. Add `-vr` to your launch arguments, for example
`Vampire.exe -game Unofficial_Patch -vr -console -novid -window -w 1920 -h 1080`.

See `README.txt` in the archive for installation, controls and troubleshooting.

## Highlights since 0.3

**Cutscenes**
- Optional 2D cutscenes. Turn on **2D cutscenes** on the Comfort page (or
  `vr_config Cutscenes2D true`) to watch scripted camera shots and stealth kills on a
  fixed screen in front of you, with the game's own camera angles. Stereo returns when
  the shot ends. It is off by default; while it is on, it takes over from the
  camera-track and stealth-kill camera settings.

**Feeding**
- Your character's animated head now stays visible during first-person feeding.
- When feeding ends, the camera returns to the first- or third-person view you had
  before, instead of being left in the feeding camera mode.

**Dialogue and cinematic cameras**
- Dialogue and stealth kills now default to the game's own camera
  (`DialogueCameraMode=0`, `StealthKillCameraMode=0`) instead of your eye position
  (mode 2 in 0.3). Head tracking still applies on top.
- Dialogue camera mode 0 always uses the dialogue HUD. Dialogue placed beside the
  NPC applies in modes 1 and 2; run `vr_config DialogueCameraMode 2` for the 0.3
  behaviour.
- New `DialogueWorldFacePlayer` option, on by default: dialogue placed beside the
  NPC turns to face you while staying upright. Both eyes share the same placement.

**Keyboard and mouse**
- In first person, unarmed and melee attacks show the game's own rotating target
  marker at your aim point, and the centre crosshair hides while it is shown.
- Menus and panels use an arrow pointer instead of a cross.
- The Windows cursor is hidden over the game window during gameplay.
- Tutorial popups and notes no longer show a pointer, since any click or key closes
  them.

## Upgrading from 0.3

- Replace all files, including `VR/config.txt`. Back up your old config first if you
  tuned it. The dialogue and stealth-kill camera defaults have changed (see above),
  and the new `Cutscenes2D` setting is off by default.
- If buttons seem wrong, select this version's **default binding** in SteamVR's
  controller binding settings.

## Known limitations

- No physical melee, roomscale collision or physical crouch.
- Left-handed mode keeps the simpler hand rendering instead of full body arms.
- Exact projection for angled (canted) displays has not been tried on such a headset.
- Quest controllers on SteamVR have no default body-shortcut button.
- Some scripted camera moments may briefly feel off; 2D cutscenes can help.

When reporting a problem, please attach `vrmod_log.txt` (copy it before relaunching,
as it is cleared each launch) and say which headset, runtime and launch arguments you used.
Report issues at https://github.com/atrblizzard/vtmb-vr/issues.

## Support

If you've enjoyed Bloodlines VR or want to support my other work, including Project
Embrace, you can contribute through [Ko-Fi](https://ko-fi.com/atrblizzard),
[Patreon](https://patreon.com/atrblizzard) or
[Buy Me a Coffee](https://buymeacoffee.com/atrblizzard). Support is entirely optional
and comes with my sincere thanks. There are no perks for Bloodlines VR, though Project
Embrace offers its own supporter benefits.

*Vampire: The Masquerade – Bloodlines belongs to its respective rights holders. This is
an unofficial fan project and requires the original game.*
