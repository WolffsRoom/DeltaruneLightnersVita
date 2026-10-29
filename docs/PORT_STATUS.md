# Development status — Lightners Live Plus for PS Vita

**Current release: v1.0 (PCK22).** Earlier Vita logs informed these fixes. The final data and patcher are validated on PC; final device performance and native trophy registration still need hardware confirmation. Report device issues with `ux0:data/deltalightplusvita/logs/`.

| Component | Current state |
| :--- | :--- |
| Boot / LiveArea | Animated 960 × 544 startup, custom LiveArea |
| Opening | Recreation of the first Lightners Live stage from Chapter 3, then the title menu |
| Menus | Centered Audio & Video / Game / Controls / Data tabs; brightness and language with audio/video |
| Gameplay difficulty | Super easy / Easy / Normal / Hard adjust error penalties and failure tolerance, including boss hits |
| Café | Conversations with the original stage cast and expanded Swatchling banter |
| Song selection | Square toggles soundtrack/chart-difficulty order; START retains alternate music; selected chart stays selected |
| Songs | All 121 built-in songs; notes in sync with the music; hold notes drawn natively |
| Story mode | Songs unlock in OST order; chapters open after their final boss |
| Fun-O-Meter / Determination Power | Square activates it; prepared sounds/frames, bounded shine pool and trophy disk writes deferred until results |
| Boss battles | King, Queen, Tenna, Titan and every Undertale song; grazing gives points |
| Results | CONCERT RESULTS with rank |
| Trophies | 30 goals and in-game list; native bridge checks cancellation, timeout, queue retention and retry backoff; registration remains unconfirmed |
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
- Supplied Vita logs show native trophy context creation succeeded, but setup timed out and a later interrupted attempt disabled native trophies. A system data-corruption warning was also reported. Native registration/unlock is not yet confirmed.
- Power/font changes passed host rendering and gameplay checks; final Vita frame timing and memory usage still need verification.

## Public files policy

The public release ships the VPK and a patcher that reconstructs the data from the player's own copies of both games. The ready-made game-data archive is not a public release asset.

## v1.0 validation

- Generated package: 2,722 resource entries checked byte for byte, 121 song folders and 135 audio streams.
- Godot checks cover settings, the three language layouts, gameplay/boss difficulty, original stage interactions, sorted selection identity, preview restart/volume restoration, font pages, bounded power effects, note timing and controller navigation.
- Native bridge mock checks cover successful/canceled/timed-out setup, retry backoff and retention/acknowledgement of queued awards.
- The rendered font probe used 1,179,648 atlas pixels at 1× sampling versus 26,345,472 at the previous 10× setting. This is a host measurement, not a Vita memory reading.

## References

- [Lightners Live Plus on itch.io](https://ezioeagle.itch.io/lightners-live-plus)
- [Godot 4 Vita](https://github.com/WolffsRoom/godot4-vita)
- [README](../README.md)
