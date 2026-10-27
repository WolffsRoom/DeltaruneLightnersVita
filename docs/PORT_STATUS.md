# Development status — Lightners Live Plus for PS Vita

**Public status: no public build yet.**

These are development tests, not guarantees about a release build.

| Area | Status | Notes |
| --- | --- | --- |
| Boot | Working on physical Vita | Animated 960×544 splash, then native GXM |
| Game data | Working on physical Vita | One `game.pck` instead of ~1,600 loose files |
| Songs | Working on physical Vita | 121 built-in songs; notes in sync with the music |
| Hold notes | Fixed, under test | Tails, lane borders and hold sparks redrawn with rectangles and sprites |
| Opening / title | Under test | Chapter 3 stage recreation, Start Game / Options / Credits |
| Options | Under test | Tabbed Deltarune-style screen; values save with the game's settings |
| Song select | Under test | Rebuilt for speed; the old list dropped to ~23 FPS on the Vita |
| Show opening / ending | Under test | Tenna announces each song; audience applause at the end |
| Custom maps | Under test | Same interface as the song select |
| Languages | Under test | English, Spanish and Brazilian Portuguese |
| Fun-O-Meter / Star Power | Under test | Double points shown as a bonus; saved high scores unchanged |
| Results screen | Under test | Blue results screen with Retry / Café / Next song |
| Public downloadable build | Not available | No game files are distributed |

## Rendering

The Vita runtime used by this port draws rectangles and textured sprites only. Godot style boxes, panels, sliders, lines, polygons, particles and shaders do not appear on the device, so the port's interface (dialog boxes, bars, menus, sparks) is built entirely from those two primitives. Elements of the original game that relied on lines or particles were redrawn the same way.

## Loading

The game's data is packed into a single `game.pck`. A small bootstrap mounts it before the game's own scripts load, and Godot then reads every resource and folder listing from the pack instead of searching the memory card.

## Audio and sync

Music plays through the Vita's BGM audio port at 48 kHz. The MIDI note clock is calibrated against the music position once a song starts. The song opening holds the MIDI clock and the music until the stage lights come up, so it does not affect note timing. Missed notes only change the music volume briefly.

## Known issues

- Store and web links do not open anything on the Vita.
- The new screens have been tested on the PC build of the Vita data; full hardware testing is in progress.

## Public files policy

This repository contains documentation only. No VPK, compiled port, game files or imported game caches are provided.

## References

- [Lightners Live Plus on itch.io](https://ezioeagle.itch.io/lightners-live-plus)
- [Godot 4 Vita](https://github.com/WolffsRoom/godot4-vita)
- [README](../README.md)
