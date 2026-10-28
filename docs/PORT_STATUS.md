# Development status — Lightners Live Plus for PS Vita

**Current release: v1.0.** Tested on the PC build of the Vita data; report hardware issues with the logs in `ux0:data/deltalightplusvita/logs/`.

| Component | Current state |
| :--- | :--- |
| Boot / LiveArea | Animated 960 × 544 startup, custom LiveArea |
| Opening | Recreation of the first Lightners Live stage from Chapter 3, then the title menu |
| Menus | Deltarune-style title, options, song select, dialog boxes and loading screen |
| Songs | All 121 built-in songs; notes in sync with the music; hold notes drawn natively |
| Story mode | Songs unlock in OST order; chapters open after their final boss |
| Fun-O-Meter / Determination Power | Touch the SOUL to activate; double points |
| Boss battles | King, Queen, Tenna, Titan and every Undertale song; grazing gives points |
| Results | CONCERT RESULTS with rank |
| Trophies | 30 trophies through NoTrpDrm |
| Audio | Music, notes, character voices and UI sounds |
| Loading | Game data packed into a single `game.pck` |
| Custom maps | Same interface as the song select |
| Languages | English, Spanish and Brazilian Portuguese |
| Patcher | Builds the Vita data from the original games and checks every file by SHA-256 |

## Rendering

The Vita runtime used by this port draws rectangles and textured sprites only. Godot style boxes, panels, sliders, lines, polygons, particles and shaders do not appear on the device, so the port's interface (dialog boxes, bars, menus, sparks, bullet boards) is built entirely from those two primitives.

## Loading

The game's data is packed into a single `game.pck`. A small bootstrap mounts it before the game's own scripts load, and Godot then reads every resource and folder listing from the pack instead of searching the memory card.

## Audio and sync

Music plays through the Vita's BGM audio port at 48 kHz. The MIDI note clock is calibrated against the music position once a song starts. The song opening holds the MIDI clock and the music until the stage lights come up, so it does not affect note timing. Boss battles pause the lane notes only; the music keeps playing.

## Patcher

The patcher reads the original Lightners Live Plus `.pck` and applies small binary patches to it, and rebuilds the DELTARUNE sprites and sounds the port uses from the DELTARUNE `data.win` files. The result is compared file by file with the release build by size and SHA-256.

## Trophies

The trophy set (`DLLP40001_00`) is an unsigned local set for NoTrpDrm. The game drops unlocked trophy ids into `ux0:data/deltalightplusvita/trophy_queue/`, and the loader registers the set (once, with the system dialog) and unlocks them. If the setup is interrupted, trophies are disabled until `trophy_disabled` is deleted; see `logs/trophy.log`.

## Known issues

- Store and web links do not open anything on the Vita.
- Touch on the SOUL and the trophy setup have not been confirmed on every console yet.

## Public files policy

This repository contains documentation only. No game files are provided; the release ships the VPK and the patcher.

## References

- [Lightners Live Plus on itch.io](https://ezioeagle.itch.io/lightners-live-plus)
- [Godot 4 Vita](https://github.com/WolffsRoom/godot4-vita)
- [README](../README.md)
