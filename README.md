# Hitbox Fixer ![C/C++ CI](https://github.com/MajR0N/hitbox_fixer/workflows/CMake/badge.svg)
This module fixes incorrect player server-side hitboxes in Counter-Strike 1.6, Half-Life and AG. (Create issue if want support for your mod).
This is a fork of [Garey27/hitbox_fixer](https://github.com/Garey27/hitbox_fixer) with extra fixes. All credit for the original plugin goes to **Garey27 (Gary)**.

## In simple words
In CS 1.6 the server has its own copy of every player's body, and it uses that copy to decide if a shot hit.
Sometimes this copy is wrong: it stands in a different pose, or in a different place, than the one you see on your screen.
Then you shoot at the head, you hear the hit sound, and nothing happens.

This plugin makes the server build each player's body the same way your game does, at the same moment you saw it.
So what you hit on your screen is what the server checks.

## Requirements
One of:
* HLDS version 8648 
* [REHLDS](https://github.com/dreamstalker/rehlds/releases) version 3.10 or above 
## Fixes
- [x] Fixes absolutely broken hitboxes when numblends == 1 (ducking/standing in reload weapon or plant c4 animation).
- [x] Hitbox backtrack based on client-side position.
- [x] Fixes broken hitbox position on spawn (since of correct backtrack)
- [x] Smooth changes between animations (landing, switching weapons) instead of an instant jump. The old pose is kept for 0.2 seconds, like in the client.
- [x] Players always stand upright on the server. A player can no longer tilt the hitboxes by sending a strange view angle.
- [x] A player cannot choose a longer "rewind time" than the server allows (limited to 0.1 seconds, like the engine does).
- [x] A new player no longer starts with legs turned the wrong way for the first moment.
- [x] Non-player entities (monsters, hostages) use the client-estimated frame (extrapolated from animtime) instead of the stale think-time frame.
## Downloads
* [Release builds](https://github.com/MajR0N/hitbox_fixer/releases)
## How to install
1. Download the zip from Releases and copy the `addons` folder into your game folder (for example `cstrike`).
2. Add one line to `addons/metamod/plugins.ini`:
   * Windows: `win32 addons/hitboxfixer/hitbox_fix_mm.dll`
   * Linux: `linux addons/hitboxfixer/hitbox_fix_mm_i386.so`
3. Restart the server or change the map. Done. You need [Metamod](https://github.com/theAsmodai/metamod-r) for this.

## Settings
Settings are in `addons/hitboxfixer/hbf.cfg`. You can also type them in the server console.

| Setting | What it does |
|---|---|
| `hbf_enabled 1` | `1` = plugin on, `0` = plugin off. |
| `hbf_developer 0` | Only for finding problems. `0` = off, `1` = prints short messages (animation changes, broken bones), `2` = also prints a status line for each player twice a second, `3` = also draws green boxes (1 second) around the hitboxes the server tests, for a player who is shooting. Compare them with the model you see. Use together with `hbf_developer_player`. |
| `hbf_developer_player 0` | Print messages for one player only. Use the player number from the messages (`p3` = `3`). `0` = all players. |

## Credits
* **[Garey27](https://github.com/Garey27)** - author of the original Hitbox Fixer. The plugin and the idea are his; this fork builds on his work.
* This project is licensed under the GNU GPL v3 (see `LICENSE`), the same as the original.
