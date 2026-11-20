# SNES ROM hacks

IPS patches that add a saved top 10 high score table and a trainer menu to SNES games, and speed some of them up. No ROMs are included: apply each patch to your own clean, unheadered USA ROM with any IPS patcher (Floating IPS, Lunar IPS, or soft-patching in your emulator or flash cart).

| Game | Folder | Original ROM CRC32 | FastROM | Adds |
|---|---|---|---|---|
| Axelay (USA) | [axelay](axelay) | `F812B533` | Added | Top 10 table, trainer |
| R-Type III: The Third Lightning (USA) | [rtype3-sa1](rtype3-sa1) | `642B656B` | Added + SA-1 | SA-1 conversion (no slowdown), top 10 table, trainer |
| Wild Guns (USA) | [wild-guns](wild-guns) | `085D8D14` | Added | Battery-saved ranking, trainer |
| Space Megaforce / Super Aleste (USA) | [super-aleste](super-aleste) | `11202781` | Not needed | Two top 10 tables (standard and short game), trainer |
| Pocky & Rocky (USA) | [pocky-rocky](pocky-rocky) | `2B0E7EA3` | Added | Top 10 table, trainer |
| Pocky & Rocky 2 (USA) | [pocky-rocky-2](pocky-rocky-2) | `FC00BB1B` | Added | Battery save, top 10 table, trainer |
| Plok (USA) | [plok](plok) | `BBD678F6` | Already in original | Top 10 table, trainer |

Common to all of them:

- The trainer menu appears at power on. Up/Down picks an option, Left/Right/A/B changes it, START plays.
- High scores are saved to battery SRAM, with 3 initials per entry. Scores are only saved when every trainer option is off (and the start stage is 1).
- The table also shows for 10 seconds when the title screen is left idle, with the music still playing.
- The patches add no lag, slowdown or display glitches to the original game. Each game's page gives its missed-frame counts before and after.

If the patched game shows a different CRC32 from the one in its folder, check that the original ROM matches the CRC above and has no 512-byte copier header.
