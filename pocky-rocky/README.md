# Pocky & Rocky (USA) TREX

Apply `Pocky & Rocky (USA) TREX.ips` to **Pocky & Rocky (USA)**, CRC32 `2B0E7EA3` (1 MiB, no header). The patch grows the ROM to 2 MiB. Patched ROM CRC32: `F807C5AC`.

## At a glance

- **High scores:** Both: a new top 10 table, saved to battery SRAM (the original has no score table).
- **Trainer:** INFINITE LIVES, INFINITE HEALTH, INFINITE BOMBS, KEEP POWER-UPS, FREEZE TIMER, START STAGE (1-6).

## High scores: new top 10 table + saver

The original has no score table at all. This patch adds a **top 10 table with initials, saved to battery SRAM**, made to look like part of the original game:

- The game's own font, taken from its Options screen, with missing letters drawn in the same banded style.
- A dusk sky gradient with falling cherry blossom petals.
- Initials entry at game over for both players, each on their own joypad; the table also shows when the title is left idle, with the title music still playing.

## FastROM and missed frames

**FastROM: added.** The original is SlowROM.

Missed (lag) frames in the attract demos, about 4400 frames each:

| Demo | Before | After |
|---|---|---|
| Stage 1 (Haunted Shrine) | 11-17 | 5-7 |
| Stage 2 (Enchanted Forest) | 105-110 | 11-13 |

Scripted play, 10,000 frames per stage: 0 missed frames in stages 1-5 and 2 in stage 6 (7 before).

## Trainer options

The trainer menu appears at power on. Up/Down picks an option, Left/Right/A/B changes it, START plays. High scores are only saved when every option is off and the game starts from the first stage or area.

| Option | |
|---|---|
| INFINITE LIVES | Lives never go down. |
| INFINITE HEALTH | Hits do no damage. |
| INFINITE BOMBS | Bombs never run out. |
| KEEP POWER-UPS | A hit doesn't lower the shot power. |
| FREEZE TIMER | The stage timer stops. |
| START STAGE | Start on stage 1-6. |
