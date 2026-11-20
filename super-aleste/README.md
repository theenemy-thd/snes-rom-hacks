# Space Megaforce / Super Aleste (USA) TREX

Apply `Space Megaforce (USA) TREX.ips` to **Space Megaforce (USA)**, CRC32 `11202781` (1 MiB, no header). Patched ROM CRC32: `7DB79AFB`.

## At a glance

- **High scores:** Both: two new top 10 tables (standard and short game), saved to battery SRAM (the original keeps one record per mode, lost at power off).
- **Trainer:** INFINITE LIVES, INFINITE BOMBS, INVULNERABLE, KEEP WEAPON POWER, START AREA (1-12).

## High scores: two new top 10 tables + saver

The original keeps one record each for the standard and the short game, lost at power off. This patch adds **two top 10 tables with initials, one per mode, saved to battery SRAM**, made to look like part of the original game:

- The game's own font, read from the game.
- A sprite starfield behind it, to suit the shoot 'em up.
- The game's own records (1,500,000 standard, 300,000 short) are the 1st place defaults, and the title screen's records and the HUD HI show each table's top score.
- Initials entry at the continue screen, after the short game's results and after the ending. When the title is left idle the two tables take turns with the demo, with the title music still playing.

## FastROM and missed frames

**FastROM: not added.** The original has almost no slowdown, so it wasn't needed.

Missed (lag) frames, the same bot input for 8000 frames in each of the 12 areas: 0-9 per area, identical on the original and the patched game. The patch adds no lag.

## Trainer options

The trainer menu appears at power on. Up/Down picks an option, Left/Right/A/B changes it, START plays. High scores are only saved when every option is off and the game starts from the first stage or area.

| Option | |
|---|---|
| INFINITE LIVES | Lives never go down. |
| INFINITE BOMBS | Bombs never run out. |
| INVULNERABLE | Hits do no harm (being crushed by scenery still kills). |
| KEEP WEAPON POWER | A hit doesn't lower the weapon power level. |
| START AREA | Start on area 1-12. |
