# EHM Realism Mod
A lightweight runtime realism & stability engine for Eastside Hockey Manager (Steam 1.5). No database edits, no changes to the game's code on disk: it loads next to the game and adjusts the match engine, player development and stability while you play.

> **Save warning:** saving while the mod is active writes the modified salary cap, progression and world settings into that `.sav` file. Back up your saves before testing.

## How it is balanced
Like OOTP's "lock league totals": the league-wide environment targets the real NHL three-season average (2023-24 to 2025-26, hockey-reference), and player ratings decide everything else. The same engine runs every league, so differences between leagues come from their players, not from per-league tuning.

Numbers marked measured come from the game: all-league rows from the mod's own counters over every league the save simulates, NHL rows from the NHL standings of a simulated 2030-31 season.

| Per team per game | Real NHL | Vanilla-level scoring (measured) | v1.2.0 (measured) |
|---|---|---|---|
| Goals, all leagues | n/a | 3.17 (333 games; 3.20 over 13,911 in v1.0.5) | 2.88 (327 games) |
| Goals, NHL standings | 3.06 | 3.34 (618 NHL games) | about 3.04 (estimated from the all-league change) |
| Power-play goals, all leagues | 0.61 (NHL) | 0.66 | 0.61 |
| Penalties drawn, all leagues | 2.87 (NHL) | 2.86 (with `penalty_call_pct` 79) | 2.95 |

**How scoring is set:** `goal_trim_pct` turns that share of the game's goal-path shot outcomes into saves. It is measured and close to linear (each point is about -0.7% goals; 30 gave -21%), and it scales every league by the same factor, so leagues keep their natural differences. 12 brings the NHL from 3.34 to about 3.06.

## Features
- **Match engine:** shot & passing attribute weights (55/55), scoring and penalty rates calibrated to the NHL, fewer penalties in the playoffs, more in rivalry games, coaches adapt tactics in-game.
- **Realistic aging:** skaters stop growing around 27 and decline from 28 (vanilla: 32-34); goalies later. Elite prospects (potential 135+) develop 25% faster; stars (ability 140+) aged 29-35 decline 45% slower. A share of 17-18-year-old prospects, more of them goalies, get a one-time potential boost so the game keeps producing NHL-calibre goalies.
- **Salary cap:** `nhl_salary_cap_usd` / `nhl_salary_floor_usd` (default: real 2026-27 NHL, $104M / $76.9M) are minimums the mod applies when the game does its yearly cap update at the season rollover. The first season of a new game still shows the database's cap, and a cap the game raises above these values is left alone.
- **World & crash protection:** 127 retained nations at database creation, U20/senior national pool refills, the empty tournament stage `malloc(0)` crash fixed (comp_stats.cpp), non-fatal assertion popups suppressed, 4GB Large Address Aware flag.

## Install (Windows)
1. Extract **EHM_Realism_Engine_v1.2.0.zip** (don't run anything from inside the zip).
2. Close Eastside Hockey Manager, then double-click **Install_EHM_Realism.exe**. It finds your game through Steam's library list (any drive), backs up `ehm.exe` once, and tells you exactly what it did.
3. Launch the game through Steam.

**Check it loaded:** open `ehm_hook.log` in the game folder. The first line shows `v1.2.0`, followed by 24 `INSTALLED` lines and 3 `PATCHED` lines. No log file means the mod did not load.

**Upgrading from an older version:** your `ehm_hook.cfg` is kept. `goal_trim_pct=12` is added if it is missing, and balance settings still at an older release's default are moved to the v1.2.0 defaults; anything you changed yourself, and your salary cap, stay as they are. The installer says which happened and keeps the old file as `ehm_hook.cfg.bak_pre_v110`.

## Install (Linux / Steam Deck / Proton)
Run the installer once through Proton (or copy the contents of `ModFiles` next to `ehm.exe` by hand), then set the Steam launch option:
```
WINEDLLOVERRIDES="dsound=n,b" %command%
```
Without it, Wine uses its built-in dsound and the mod never loads.

## Compatibility
- **Game:** Eastside Hockey Manager on Steam, version 1.5.
- **Existing saves:** yes. Match-engine and development settings take effect within 10 seconds, even mid-save. Cap values apply to new games only; never change them mid-save.
- **Database / graphics / skin mods:** compatible (the mod changes nothing on disk except the 4GB flag on `ehm.exe`).
- **Other `dsound.dll` mods:** not compatible, only one can load.
- **Online leagues:** results come from the computer that runs the sim, so that computer's mod and `ehm_hook.cfg` decide the results.

## Settings
Everything is in `ehm_hook.cfg` in the game folder (100 = vanilla for any `_pct` value). The newest defaults are always written to `ehm_hook.default.cfg` so you can compare.

`high_priority=1` runs the game at High CPU priority for faster sims. It is off by default because it can starve other programs.

**Check your own league:** after a simulated season, compare the NHL standings (goals for / games played) with 3.06. Off by X%: move `goal_trim_pct` by about X / 0.7 (up = fewer goals). Too many power plays: lower `penalty_call_pct` by 5. `goalie_save_scale_pct` (default 100) is capped at 100.

## FAQ
**Can it make the game 64-bit?** No. `ehm.exe` is a closed 32-bit program; only the developer can rebuild it as 64-bit. It also would not help: a full world sim measured 0.7 GB of memory (peak) against the 4 GB the mod's Large Address Aware flag already allows.

## Uninstall
Double-click **Uninstall_EHM_Realism.exe**. It removes the mod files, restores the backed-up `ehm.exe`, and keeps your settings as `ehm_hook.cfg.saved` (a later reinstall picks them up again). If no backup exists, use Steam > Properties > Installed Files > Verify integrity.
