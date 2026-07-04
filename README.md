# The Riftbreaker — AMP Generic-module template

A [CubeCoders AMP](https://cubecoders.com/AMP) Generic-module template to run **The Riftbreaker
Dedicated Server** fully headless (`cli=1`) as an AMP instance.

## Install (in AMP)
1. **Configuration → Instance Deployment → Add a Configuration Repository**
2. Paste: `Skywardhigh/Riftbreaker-AMPTemplate:main` → **Fetch** → refresh the browser
3. **Create New Instance** → pick **The Riftbreaker**

## What it does
- Installs the DS via anonymous **SteamCMD** (Steam app `4114030`) — no login/second copy needed.
- Launches the DS **headless, directly**: `4114030\bin\DedicatedServer.exe cli=1 app_mode=server server_name="..." campaign="..." ...` (working dir `4114030/bin`).
- Exposes the server settings as AMP options: name, password, RCON password, max players (1–4),
  visibility, pause-when-empty, and the game mode / map / difficulty.

## Game mode ↔ map ↔ difficulty (must match)
- **Open Campaign** → a `campaigns/open/headquarters_*` map + `easy|normal|hard|brutal`
- **Story Campaign** → no map (leave Map on the Story option) + `coop_campaign_*`
- **Survival** → a `survival/*` map + `coop_*`

## Notes
- **Networking default:** ships with `disable_steam=1` (LAN / direct-IP) — the stable, tested mode.
  Steam networking (`disable_steam=0`) may fail during startup with `STEAM: SteamGameServer_Init failed!`
  under AMP's service account, so it's off by default.
- **Console / status via log tail:** the DS logs to its own file (not stdout), so AMP reads it natively —
  `App.AdminMethod=TailLogFile` + `App.TailLogFilePath=C:\Windows\ServiceProfiles\NetworkService\Documents\The Riftbreaker\exor_logs.txt`
  (the AMP service account's Documents; the absolute path tails fine). Ready-state fires on
  `ControllerState … activating: ServerGameplayState`; joins parse from
  `ServerGameplayState: Player '…':'name':'steamid'`. All instances run under the same service account and
  share this one log, so run **one at a time** for clean per-instance console/player tracking. LAN listen port: `6321`.
- **First create** may hit SteamCMD `Missing configuration`; the manual **Update** button is the known-good workaround.
- **Stop** is `OS_CLOSE`/kill (autosave runs ~every 10 min; pause-when-empty protects the base).
- **Server names with spaces** are passed quoted through AMP formatted args (`server_name="..."`).

Built by reverse-engineering the DS + the official EXOR headless guide, then aligned with the AMP configuration generator output. Community-made, not official.
