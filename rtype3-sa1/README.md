# R-Type III (USA) SA-1 TREX

Apply `R-Type III (USA) SA-1 TREX.ips` to **R-Type III: The Third Lightning (USA)**, CRC32 `642B656B` (2 MiB, no header). The patch grows the ROM to 4 MiB. Patched ROM CRC32: `6A5208C3`.

## Features

- **SA-1 conversion**: the game logic runs on the SA-1 chip at 10.74 MHz, which removes almost all of the original's slowdown. Needs an emulator, flash cart or FPGA core with SA-1 support.

## High score table (added)

The original has no saved high score table. This patch adds a **top 10 table with initials, saved to battery RAM**, made to look like part of the original game:

- R-Type III's own lettering, taken from the game.
- A sprite starfield behind it, to suit the shoot 'em up.
- Initials entry after the continue screen (YES or NO) for a top 10 score; the table also shows every other time the title is left idle, before the demo.

## FastROM and missed frames

**FastROM: added**, and the game logic moved to the SA-1 (10.74 MHz).

Missed (lag) frames, bot play: the original misses between 63 and 1317 frames per 5000 on stage 1 alone (5-30% of frames all through the stages). The SA-1 build misses 0-41 frames per 5000 over a 120,000-frame run, nearly all of them on stage loads.

## How the SA-1 conversion was done

No SA-1 version of R-Type III existed, so this one was built from scratch. The aim was to keep the game itself untouched and change only where it runs.

### 1. FastROM check first

The cart is already marked FastROM, but the game turns the fast ROM speed off in parts of its NMI, and about 43% of everything it executes is stage code that it copies from ROM into work RAM (WRAM) and runs there. WRAM always runs at 2.68 MHz. Forcing FastROM on everywhere only cut lag by about 6%, so FastROM alone was not worth a release, and the SA-1 became the real fix.

### 2. Tracing the whole game

snes9x was built from source with extra tracing: for every executed instruction it records the CPU context (main loop, NMI, IRQ or game logic), the register widths, the data bank, the direct page, and which memory each access touched. It also logs every DMA and DMA register write. Bot runs (invulnerable random play, deaths, charged shots, every stage, the attract demos, the ending and the second loop) were merged into one trace. The trace showed that all the code running from WRAM runs only inside the per-frame game logic call, which made a clean split possible: the SA-1 runs the logic, and the SNES CPU keeps the NMI, the raster IRQs and the hardware I/O.

### 3. Moving work RAM into BW-RAM

The SA-1 can't see the SNES WRAM, so all of the game's 128 KiB of work RAM was moved into the cart's BW-RAM, which both CPUs can see:

| Original | New |
|---|---|
| WRAM `$7E:0000-1FFF` (low RAM, direct page) | BW-RAM `$40:0000-1FFF`, also seen at `$6000-$7FFF` in the system banks; direct page moved to `$6000` |
| WRAM `$7E:2000-FFFF` | BW-RAM `$40:2000-FFFF` (same 16-bit addresses) |
| WRAM `$7F:0000-FFFF` | BW-RAM `$41:0000-FFFF` |

The stage code the game copies into RAM lands at the same 16-bit addresses in BW-RAM, so jumps inside it still work. The SNES CPU keeps only its stack in real WRAM.

A relocation script turns the trace into byte patches, each checked against the original bytes: long addresses `$7E`/`$7F` become `$40`/`$41`, low RAM references get `+$6000`, MVN/MVP banks, direct page set-ups, pointer bank bytes and data bank set-ups are moved. The game keeps several copies of the same code in ROM for different stages, so every patch is applied to every copy. That came to roughly a thousand patch sites. Places too short to patch in place go through small hook stubs in a new bank, and `TDC` used as "load zero" (which breaks once the direct page isn't 0) goes through a `BRK` trap that emulates it.

### 4. Cart and header

The ROM grows from 2 MiB to 4 MiB with an SA-1 header (map mode `$23`, cart type `$35`: ROM + SA-1 + battery RAM, 256 KiB BW-RAM). The SA-1 memory controller maps the original ROM to the same addresses as before and puts the new code banks at `$C0+`. A small boot routine starts the SA-1 at reset.

### 5. Handing the game logic to the SA-1

Each frame the SNES NMI asks the SA-1 to run the game logic and the sprite builder (OAM). The logic's own hardware register accesses (PPU, DMA, multiply/divide and so on) were rewritten to go through a mailbox in the SA-1's I-RAM: the SNES serves those requests, and the DMAs go through a fix-up routine that points their sources at BW-RAM. Register writes at sites that can't take a hook use `BRK` traps.

### 6. Keeping the screen and timing identical

- **Top of screen:** the NMI turns the display on from a line 6 IRQ, which waits for the vblank DMA part to finish. The extra DMA fix-up made it late (a flickering band at the top). The fix-up now skips fixed ROM/WRAM sources, checks banks inline, and the NMI's `CLI` was moved up.
- **Charged shot:** a scanline wait before an optional DMA lost whole frames (a black flash) when the NMI ran late. The NMI keeps forced blank until the line 6 IRQ, so the wait could be removed.
- **HUD split:** the raster IRQs at lines 207 and 215 use delay loops to land their writes in h-blank. The SA-1 build's IRQ entry costs about 140 master cycles more, so the loops were shortened from 5 to 3 passes. The writes now land within 1-2 pixels of the original's.
- **Ending and second loop:** the logic waits for the SNES main loop in 8 places, which could deadlock under SA-1. The SA-1 now hands that wait back to the SNES.
- **Attract demos:** the demo stage set-ups start VRAM DMAs straight from the logic; those four DMA blocks are run on the SNES.

### 7. Testing

The conversion was checked against the original in snes9x and an accuracy-focused bsnes built from source: the title, all 6 stages, both loops, the ending, the three attract demos, game over and continue, and every trainer option. The top 10 table and trainer were added on top of the finished conversion. It has also been played on MiSTer.

### MiSTer note

The save is 256 KiB, because the game's work RAM now lives in the battery-backed BW-RAM and changes every frame. That can't be made smaller without dropping the saved table, and it means the MiSTer SNES core writes the whole 256 KiB save every time the OSD is opened, which takes a moment. To avoid that, turn the core's OSD autosave off and use "Save Backup RAM" after a new high score.

## Trainer options

| Option | |
|---|---|
| INFINITE LIVES | Lives never go down. |
| INVULNERABLE | The ship can't be hit. |
| START STAGE | Start on stage 1-6. |

Only player 1's score goes into the table in 2-player mode.
