# EHM Realism Engine (v1.0)
A lightweight runtime realism & stability engine for Eastside Hockey Manager (Steam 1.5).

## Features
- **Modern NHL Three-Zone Balance**: Balanced 55/55 shot & passing attribute weights, realistic .902-.905 league-wide save percentages, and symmetric multiplier bounds (72-138).
- **Dynamic Salary Cap Escalator**: Starts at $95.5M ($70.6M floor) with +5%/yr annual cap growth across all leagues.
- **Realistic Player Primes & Aging**: Shifts skater prime development to ages 24-27 and goaltender primes to 26-29.
- **Global World & Crash Protection**: Unlocks 127 retained nations at database creation, patches empty tournament stage `malloc(0)` exits (`comp_stats.cpp`), suppresses non-fatal assertion popups, and enables 4GB Large Address Aware memory support.

## Installation
1. Extract this ZIP anywhere on your PC.
2. Right-click `Install_EHM_Realism.ps1` -> **Run with PowerShell**.
3. Launch Eastside Hockey Manager normally via Steam!
