# EHM Realism Engine (v1.0)

A lightweight runtime realism & stability engine for **Eastside Hockey Manager (Steam 1.5)**.

> **Important Save Warning:** Saving a game while this mod is active permanently writes modified salary cap, progression, and world settings into that `.sav` file. Always back up your existing save files before testing.

## Compatibility
* **Databases:** Works out-of-the-box with Sports Interactive's default base database (2014) as well as all custom databases (Premier Pivot Rosters, TBL Rosters, historical databases, and custom edits) with zero database modifications required.
* **Platforms:** Built for **Windows** (and **Linux / Steam Deck** via Proton with `WINEDLLOVERRIDES="dsound=n,b" %command%`).

## Features
* **Modern NHL Three-Zone Balance:** Balanced 55/55 shot & passing attribute weights, realistic `.902–.905` league-wide save percentages, and symmetric multiplier bounds (`72–138`).
* **Dynamic Salary Cap Escalator:** Starts at `$95.5M` (`$70.6M` floor) with `+5%/yr` annual cap growth across up to 128 leagues.
* **Realistic Player Primes & Aging:** Shifts skater prime development to ages `24–27` and goaltender primes to `26–29`.
* **Global World & Crash Protection:** Unlocks `127` retained nations at database creation, patches empty tournament stage `malloc(0)` exits (`comp_stats.cpp`), suppresses non-fatal assertion popups, and enables **4GB Large Address Aware** memory support.

## Installation
1. Download and extract **`EHM_Realism_Engine_GitHub_v1.0.zip`** from the [Releases](https://github.com/naterego93-afk/EHM-Realism-Engine) section.
2. Double-click **`Install_EHM_Realism.exe`** (automatically detects your Steam EHM folder, backs up vanilla files, and applies the 4GB memory patch).
3. Launch **Eastside Hockey Manager** normally through Steam!

*(Every setting can be customized or reverted to vanilla (`100`) inside **`ehm_hook.cfg`** in your game folder. To uninstall at any time, double-click **`Uninstall_EHM_Realism.exe`**.)*
