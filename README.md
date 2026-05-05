# LK Anticheat — CS 1.6

Anticheat for Counter-Strike 1.6. Designed to be **simple** — the player just opens the launcher and plays. No complicated setup, no extra steps. Unlike many other anticheats out there, this one doesn't require the client to do anything specific.

> **Source code:** free upon request. Write to **zideriaglink@gmail.com** and I'll send it to you, no payment required.

---

## Files

| File | Description |
|---|---|
| `LKAnticheat.exe` | Launcher. Keep it open while you play |
| `LKHook.dll` | Protection module injected into the game client |
| `lk_anticheat.amxx` | Server plugin compiled for AMX Mod X 1.10 |

---

## Installation

### Client

1. Open **LKAnticheat.exe** — before or after launching CS 1.6, either works.
2. The launcher automatically downloads, verifies and injects the protection module into the game.
3. Keep it open while you play. You can minimize it to the system tray.

That's it. The player doesn't need to do anything else — just play normally.

> On first launch it will create a desktop shortcut automatically.

### Server

1. Copy `lk_anticheat.amxx` into `cstrike/addons/amxmodx/plugins/`.
2. Add `lk_anticheat.amxx` to `plugins.ini`.
3. Restart the server.

---

## How it works

**LKAnticheat.exe** detects when CS 1.6 is open, downloads and verifies the protection module, and injects it into the game process. It keeps the module up to date by checking versions against the server on every session.

**LKHook.dll** runs inside the game process and performs continuous real-time analysis. It detects and shuts down the game if unauthorized software or memory modifications are found during the session. It communicates with the server through the plugin to report the client's status.

**lk_anticheat.amxx** handles verification for each player on connect. Players without the module active or that fail verification are kicked automatically. Admins have commands to check status and run manual scans.

---

## Admin commands

Require `ADMIN_KICK` flag (`d`).

| Command | Description |
|---|---|
| `lkac_check <player>` | Show a player's anticheat status |
| `lkac_ping <player>` | Check if the module is responding |
| `lkac_scancommands <player>` | Run a manual scan |

---

## Server cvars

| Cvar | Default | Description |
|---|---|---|
| `lkac_logs` | `0` | Enable (`1`) or disable (`0`) informational server logs |

When `lkac_logs 0`, only kick events are printed to the server console. Set to `1` if you want to see full verification and scan activity.

---

## Kick reasons

| Message | Cause |
|---|---|
| `LK Anticheat: module not detected` | Module not active or was blocked |
| `LK Anticheat: verification failed` | Authenticity check did not pass |
| `LK Anticheat: unauthorized module` | External injected software detected |
| `LK Anticheat: hidden module detected` | Hidden code found in memory |
| `LK Anticheat: unauthorized tool` | Cheat tool detected during session |
| `LK Anticheat: memory modification` | Game code was altered |
| `LK Anticheat: hack detected` | Known hack commands registered |
| `LK Anticheat: no response` | Module stopped responding mid-session |

---

## Requirements

- Windows 10 / 11 (x64)
- Counter-Strike 1.6 (Steam or non-Steam)
- Server running AMX Mod X 1.10

---

## Notes

- **No VAC ban risk.** LK Anticheat does not modify any game files and does not interfere with Valve's systems in any way. It has been tested extensively without triggering VAC. You can use it safely on any server.
- No Visual C++ Redistributable required.
- Works with multiple CS instances open at the same time.
- The module is downloaded and verified automatically on every launch — no manual updates needed.
