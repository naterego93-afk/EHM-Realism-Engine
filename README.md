# EHM Realism Engine v1.0.2
A lightweight runtime realism & stability engine for Eastside Hockey Manager (Steam 1.5).

> **Save warning:** saving while the mod is active writes the modified salary cap, progression and world settings into that `.sav` file. Back up your saves before testing.

## Features
- **Modern NHL three-zone balance:** 55/55 shot & passing attribute weights, league save percentages around .900, symmetric multiplier bounds (72-138).
- **Dynamic salary cap escalator:** starts at $95.5M ($70.6M floor) and grows +5%/yr across all leagues.
- **Realistic primes & aging:** skater development peaks shift to 24-27, goalies to 26-29; optional rookie development boost and veteran decline grace.
- **Match intensity:** fewer penalty calls in the playoffs, rivalry and coach tactical adjustments, optional goal horn audio.
- **World & crash protection:** 127 retained nations at database creation, U20/senior national pool refills, the empty tournament stage `malloc(0)` crash fixed (comp_stats.cpp), non-fatal assertion popups suppressed, 4GB Large Address Aware flag.

## Install (Windows)
1. Extract **EHM_Realism_Engine_v1.0.2.zip** (don't run anything from inside the zip).
2. Close Eastside Hockey Manager, then double-click **Install_EHM_Realism.exe**. It finds your game through Steam's library list (any drive), backs up `ehm.exe` once, and tells you exactly what it did.
3. Launch the game through Steam.

**Check it loaded:** open `ehm_hook.log` in the game folder. The first line shows `v1.0.2`, followed by 24 `INSTALLED` lines and 3 `PATCHED` lines. No log file means the mod did not load.

## Install (Linux / Steam Deck / Proton)
Run the installer once through Proton (or copy the contents of `ModFiles` next to `ehm.exe` by hand), then set the Steam launch option:
```
WINEDLLOVERRIDES="dsound=n,b" %command%
```
Without it, Wine uses its built-in dsound and the mod never loads.

## Settings
Everything is in `ehm_hook.cfg` in the game folder (100 = vanilla for any `_pct` value). Upgrading keeps your `ehm_hook.cfg`; the newest defaults are always written to `ehm_hook.default.cfg` so you can compare. Example: `nhl_salary_cap_usd=88000000` starts the cap at $88M and still escalates +5%/yr.

`high_priority=1` runs the game at High CPU priority for faster sims. It is off by default because it can starve other programs.

## Uninstall
Double-click **Uninstall_EHM_Realism.exe**. It removes the mod files, restores the backed-up `ehm.exe`, and keeps your settings as `ehm_hook.cfg.saved` (a later reinstall picks them up again). If no backup exists, use Steam > Properties > Installed Files > Verify integrity.
