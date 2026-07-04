# The Riftbreaker — AMP Generic-module template

A [CubeCoders AMP](https://cubecoders.com/AMP) Generic-module template to run **The Riftbreaker
Dedicated Server** fully headless (`cli=1`) as an AMP instance.

## Install (in AMP)
1. **Configuration → Instance Deployment → Add a Configuration Repository**
2. Paste: `Skywardhigh/Riftbreaker-AMPTemplate:main` → **Fetch** → refresh the browser
3. **Create New Instance** → pick **The Riftbreaker** (grouped under the `Sky` prefix)

## What it does
- Installs the DS via anonymous **SteamCMD** (Steam app `4114030`) — no login/second copy needed.
- Launches headless: `bin\DedicatedServer.exe cli=1 app_mode=server campaign=… mission=… difficulty=… server_name=… …`
- Exposes the server settings as AMP options: name, password, RCON password, max players (1–4),
  visibility, pause-when-empty, and the game mode / map / difficulty.

## Game mode ↔ map ↔ difficulty (must match)
- **Open Campaign** → a `campaigns/open/headquarters_*` map + `easy|normal|hard|brutal`
- **Story Campaign** → no map (leave Map on the Story option) + `coop_campaign_*`
- **Survival** → a `survival/*` map + `coop_*`

## Notes
- **No port-forwarding** in the default Steam mode — The Riftbreaker uses Steam Datagram Relay;
  players join via the in-game server browser or the join link. Only `disable_steam=1` (LAN) uses a direct port.
- **Status** is process up/down (the DS logs to `Documents\The Riftbreaker\exor_logs.txt`, not stdout).
- **Stop** is a process kill (autosave runs ~every 10 min; pause-when-empty protects the base).
- **Server names with spaces** are passed quoted (`server_name="{{ServerName}}"`, mirroring the Valheim template) — verify on first boot.

Built by reverse-engineering the DS + the official EXOR headless guide, mirroring the Astroneer template. Community-made, not official.
