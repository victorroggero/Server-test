# LoLServer — What You Can Edit (`GameInfo.json`) + In-Game Commands

## Champion
- Field: `"champion"`
- Use the **Champion Code** column, not the display name
- Examples: `Garen`, `Ezreal`, `MasterYi` (Master Yi), `Chogath` (Cho'Gath), `MonkeyKing` (Wukong), `FiddleSticks`, `JarvanIV` (Jarvan IV), `Khazix` (Kha'Zix), `KogMaw` (Kog'Maw), `Velkoz` (Vel'Koz), `XinZhao` (Xin Zhao), `DrMundo` (Dr. Mundo), `TwistedFate` (Twisted Fate)
- Case-sensitive

## Skin
- Field: `"skin"`
- Number = skin index, `0` = default

## Team / Side
- Field: `"team"`
- `"BLUE"` or `"RED"`

## Summoner Spells
- Fields: `"summoner1"`, `"summoner2"`
- Confirmed working values: `SummonerFlash` (Flash), `SummonerHeal` (Heal), `SummonerDot` (Ignite), `SummonerSmite` (Smite), `SummonerHaste` (Haste/Ghost)
- Example: `"summoner1": "SummonerFlash", "summoner2": "SummonerSmite"`

## Runes
- Field: `"runes"` — object of slot number → rune ID
- Rune ID examples (Greater tier, common picks):
  - `5245` = Greater Mark of Attack Damage
  - `5273` = Greater Mark of Magic Penetration
  - `5317` = Greater Seal of Armor
  - `5289` = Greater Glyph of Magic Resist
  - `5335` = Greater Quintessence of Attack Damage
  - `5357` = Greater Quintessence of Ability Power
- Example: `"1": 5245, "2": 5245, ... "10": 5317, ... "19": 5289, ... "28": 5335`
- ⚠️ Wrong/invalid IDs can crash the client — only use IDs from the official ID list

## Masteries/Talents
- Field: `"talents"` — object of talent ID → points spent
- Example from a working config: `"4111": 1, "4112": 3, "4211": 2`
- IDs are specific to the old 2015 mastery tree; safest to copy an existing working block and only tweak point values

## Player Name / Rank Display
- Fields: `"name"`, `"rank"` (e.g. `"CHALLENGER"`, `"SILVER"`, `"GOLD"`, `"BRONZE"`), `"ribbon"`, `"icon"`
- Cosmetic only, no gameplay effect

## Number of Players / Slots
- Add or remove objects in the `"players"` array
- Each one needs its own `"playerId"` (unique number) and a `"blowfishKey"` (can reuse the same key across all slots)

## Map
- Field: `"map"` inside `"game"`
- Examples: `1` = Summoner's Rift (2011 version), `10` = Twisted Treeline, `12` = Howling Abyss (ARAM), `11` = Summoner's Rift (current visual update)
- Only works if the content package actually supports that map's logic

## Game Mode
- Field: `"gameMode"` inside `"game"`
- Example: `"CLASSIC"`

## Mana Costs On/Off
- Field: `"MANACOSTS_ENABLED"` inside `"gameInfo"` — `true`/`false`

## Cooldowns On/Off
- Field: `"COOLDOWNS_ENABLED"` inside `"gameInfo"` — `true`/`false`

## Cheats On/Off
- Field: `"CHEATS_ENABLED"` inside `"gameInfo"` — `true`/`false`

## Minion Waves On/Off
- Field: `"MINION_SPAWNS_ENABLED"` inside `"gameInfo"` — `true`/`false`

## Damage Numbers Visible to Everyone or Just You
- Field: `"IS_DAMAGE_TEXT_GLOBAL"` inside `"gameInfo"` — `true`/`false`

## Game Force-Start Timer
- Field: `"forcedStart"` (top level) — seconds before the game starts regardless of who's connected
- Example: `60`

---

# In-Game Chat Commands

Type these directly into the in-game chat box, starting with `!`

| Command | What it does |
|---|---|
| `!help` | Lists all commands |
| `!ad <amount>` | Add/remove Attack Damage (negative number removes) |
| `!ap <amount>` | Add/remove Ability Power |
| `!health <amount>` | Add/remove HP |
| `!mana <amount>` | Add/remove Mana |
| `!gold <amount>` | Add/remove gold |
| `!xp <amount>` | Add/remove XP |
| `!speed <amount>` | Add/remove movement speed |
| `!size <amount>` | Grow/shrink your champion model |
| `!level <number>` | Set your champion level |
| `!skillpoints` | Gives 17 skill points instantly |
| `!revive` | Respawn if dead |
| `!tp <x> <y>` | Teleport to coordinates |
| `!coords` | Show your current coordinates |
| `!ch <champion>` | Change your champion mid-game (buggy) |
| `!changeteam <teamId>` | Change your team mid-game (buggy) |
| `!model <model>` | Change your model — ⚠️ invalid name crashes everyone |
| `!spawn <minionsblue\|minionspurple>` | Spawn 4 random minions for that team |
| `!kill <minionsblue\|minionspurple>` | Kill all minions of that team |
| `!spawnstate <0\|1>` | Disable/enable minion spawns |
| `!mobs <teamId>` | Ping positions of all mobs on that team |
| `!inhib` | Spawns a baron where you're standing |
| `!reloadscripts` | Reload champion/buff/item scripts (causes brief lag) |
| `!rainbow` | Flashing rainbow screen — ⚠️ epilepsy warning |

---

# Connecting / Playing With Others

- Each client connects using: `<ip> <port> <blowfishKey> <playerId>`
- Confirmed working: `127.0.0.1` (same PC), and RadminVPN (across machines)
- No bots — every slot in `"players"` needs an actual client connecting to it
