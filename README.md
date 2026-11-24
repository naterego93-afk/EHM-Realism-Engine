# EHM Realism Engine v1.0.4
A lightweight runtime realism & stability engine for Eastside Hockey Manager (Steam 1.5).

> **Save warning:** saving while the mod is active writes the modified salary cap, progression and world settings into that `.sav` file. Back up your saves before testing.

## Features
- **Modern NHL three-zone balance:** 55/55 shot & passing attribute weights, tunable goalie save scale, symmetric multiplier bounds (72-138).
- **Dynamic salary cap escalator:** starts at the real 2026-27 NHL cap ($104M, $76.9M floor) and grows +5%/yr across all leagues.
- **Realistic aging:** skaters start declining around 28-29 instead of vanilla 32-34, goalies around 31; optional rookie development boost and veteran decline grace.
- **Match intensity:** fewer penalty calls in the playoffs, rivalry and coach tactical adjustments, optional goal horn audio.
- **World & crash protection:** 127 retained nations at database creation, U20/senior national pool refills, the empty tournament stage `malloc(0)` crash fixed (comp_stats.cpp), non-fatal assertion popups suppressed, 4GB Large Address Aware flag.

## Install (Windows)
1. Extract **EHM_Realism_Engine_v1.0.4.zip** (don't run anything from inside the zip).
2. Close Eastside Hockey Manager, then double-click **Install_EHM_Realism.exe**. It finds your game through Steam's library list (any drive), backs up `ehm.exe` once, and tells you exactly what it did.
3. Launch the game through Steam.

**Check it loaded:** open `ehm_hook.log` in the game folder. The first line shows `v1.0.4`, followed by 24 `INSTALLED` lines and 3 `PATCHED` lines. No log file means the mod did not load.

## Install (Linux / Steam Deck / Proton)
Run the installer once through Proton (or copy the contents of `ModFiles` next to `ehm.exe` by hand), then set the Steam launch option:
```
WINEDLLOVERRIDES="dsound=n,b" %command%
```
Without it, Wine uses its built-in dsound and the mod never loads.

## Settings
Everything is in `ehm_hook.cfg` in the game folder (100 = vanilla for any `_pct` value). Upgrading keeps your `ehm_hook.cfg`; the newest defaults are always written to `ehm_hook.default.cfg` so you can compare. Example: `nhl_salary_cap_usd=88000000` starts the cap at $88M and still escalates +5%/yr.

`high_priority=1` runs the game at High CPU priority for faster sims. It is off by default because it can starve other programs.

## Realism targets (real NHL, 2025-26 / 2026-27)
| Stat | Real NHL | Setting that moves it |
|---|---|---|
| Goals per team per game | 3.08 / 3.16 | `goalie_save_scale_pct` (through save %) |
| League save % | .896 / .891 | `goalie_save_scale_pct` (default 99; 1 point = about 1% fewer saves) |
| Shots per team per game | 27.6 / 27.3 | no direct setting (game engine) |
| Power plays per team per game | 2.88 / 3.11 | `penalty_call_pct` (100 = vanilla) |
| Salary cap / floor | $95.5M / $70.6M, then $104M / $76.9M | `nhl_salary_cap_usd`, `nhl_salary_floor_usd` |

After a simulated season, compare your league stats screen with this table. If league save % is above .900, lower `goalie_save_scale_pct` by 1 and sim again; below .885, raise it by 1. Change the cap values only before starting a new game.

## Uninstall
Double-click **Uninstall_EHM_Realism.exe**. It removes the mod files, restores the backed-up `ehm.exe`, and keeps your settings as `ehm_hook.cfg.saved` (a later reinstall picks them up again). If no backup exists, use Steam > Properties > Installed Files > Verify integrity.
