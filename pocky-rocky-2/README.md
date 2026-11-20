# Pocky & Rocky 2 (USA) TREX

Apply `Pocky & Rocky 2 (USA) TREX.ips` to **Pocky & Rocky 2 (USA)**, CRC32 `FC00BB1B` (1.5 MiB, no header). The patch grows the ROM to 2 MiB. Patched ROM CRC32: `70E6928A`.

## At a glance

- **High scores:** Both: a new top 10 table, saved to battery SRAM (the original has no score table), plus a battery save of game progress.
- **Trainer:** INVINCIBILITY, INFINITE LIVES, KEEP POWER-UPS, FREEZE TIMER, START STAGE (1-9).

## Features

- **Battery save**: the game saves at every stage clear (stage, score, lives, gold and keys). Choose PASSWORD on the title: the saved stage's password is already filled in, and START carries on with everything restored. (START on the title is always a new game, with the training. Dying before a stage is cleared doesn't make a save.)

## High scores: new top 10 table + saver

The original has no score table at all. This patch adds a **top 10 table with initials, saved to battery SRAM**, made to look like part of the original game:

- The game's own password-screen font and look: black letters in orange-bordered white panels with drop shadows, over the blue diamond pattern, all taken from the ROM.
- Initials entry at game over and at the last stage clear (the game never returns to the title after its ending); the table also shows when the title is left idle, with the title music still playing.

## FastROM and missed frames

**FastROM: added.** The original is SlowROM.

Missed (lag) frames, the same scripted input for 3000 frames in each of the nine stages:

| | Before | After |
|---|---|---|
| Total, 9 stages | 348 | 17 |
| Stage 7 (worst) | 258 | 17 |
| Stage 8 | 72 | 0 |

## Trainer options

The trainer menu appears at power on. Up/Down picks an option, Left/Right/A/B changes it, START plays. High scores are only saved when every option is off and the game starts from the first stage or area.

| Option | |
|---|---|
| INVINCIBILITY | Hits do no harm (pits and running out of time still cost a life). |
| INFINITE LIVES | Lives never go down. |
| KEEP POWER-UPS | A hit doesn't lose power-ups. |
| FREEZE TIMER | The stage timer stops. |
| START STAGE | Start on stage 1-9. |

## Testing

Every trainer option was play-tested in an emulator (with INVINCIBILITY the same 6000 frames of input lost no lives or power, against 5 lives and 2 power levels lost without it). A first hands-on play-test was also OK. This is the newest patch here, so reports of any problems are welcome.
