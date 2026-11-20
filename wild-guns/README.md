# Wild Guns (USA) TREX

Apply `Wild Guns (USA) TREX.ips` to **Wild Guns (USA)**, CRC32 `085D8D14` (1 MiB, no header). The patch grows the ROM to 2 MiB. Patched ROM CRC32: `B3A58B89`.

## At a glance

- **High scores:** Saver only: the game's own top 5 RANKING is kept in battery SRAM instead of being lost at power off. No new table.
- **Trainer:** INFINITE LIVES, INVULNERABLE, INFINITE BOMBS, INFINITE GUN AMMO, STAGE SELECT.

## High scores: saver only (the game's own ranking)

Wild Guns already has its own **top 5 RANKING** (scores, initials and character portraits), but the original loses it at power off. This patch **keeps the game's own ranking in battery SRAM**, so it survives a power cycle. The game's font, screen, initials entry and attract loop are left exactly as they were; it shows a little longer when there's nothing to enter (6 s) and any button leaves early.

## FastROM and missed frames

**FastROM: added.** The original is SlowROM.

Missed (lag) frames, scripted play for 2.5 minutes (9000 frames) per stage:

| Stage | Before | After |
|---|---|---|
| Desolation Canyon | 431 | 9 |
| Armored Train | 20 | 8 |
| Gold Mine | 8 | 8 |
| Ammunition Depot | 4 | 4 |
| Whole game, 30-minute bot run | 700-745 | 89-105 |

## Trainer options

The trainer menu appears at power on. Up/Down picks an option, Left/Right/A/B changes it, START plays. High scores are only saved when every option is off and the game starts from the first stage or area.

| Option | |
|---|---|
| INFINITE LIVES | Lives never go down. |
| INVULNERABLE | Shots and knock-downs do no harm. |
| INFINITE BOMBS | Bombs never run out. |
| INFINITE GUN AMMO | Special guns never run out of shots. |
| STAGE SELECT | Turns on the game's hidden stage select for every game. |
