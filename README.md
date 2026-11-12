# SkyFactory 4 — FTB Quests Progression Book

A full tutorial-to-endgame FTB Quests quest book for **SkyFactory 4** (Minecraft 1.12.2),
built because the pack ships without FTB Quests and new players often don't know
what to do next. ~113 quests across 10 chapters, in English, with short
what/why/next descriptions on every quest.

Built by reverse-engineering SkyFactory 4's own original advancement data
(`config/triumph/script/sf4/*`, a Triumph-mod advancement tree bundled with the
pack but hidden from normal play) and the pack's CraftTweaker scripts, so the
progression order and item IDs match the actual intended pack design wherever
possible.

## What's in the book

| # | Chapter | Notes |
|---|---|---|
| 1 | Tutorial | First log → first cobblestone |
| 2 | Age 1 | Sky Orchards saplings, first metals, cauldron |
| 3 | Age Farming | Bonsai pots, market, animal seeds |
| 4 | Age Enhancement | Full Tinkers' Construct + Smeltery line |
| 5 | Age Power | **Choice branch**: Mekanism *or* NuclearCraft, plus mandatory Deep Mob Learning |
| 6 | Age Storage | **Choice branch**: Applied Energistics 2 *or* Simple Storage Network |
| 7 | Age Exploration | Nether, End, dragon kill, rare ores |
| 8 | Astral Sorcery *(side branch, optional)* | |
| 9 | Mystical Agriculture *(side branch, optional)* | |
| 10 | Age AllTheThingsOMGLOL | Endgame capstone — "You Win!" |

Choice branches use `dependency_requirement: "one_completed"` — you only need to
finish **one side**, not both, to clear the chapter. Side branches are fully
optional and don't block main progression at all.

Every chapter (except Tutorial) ends in a loot crate reward. Rewards throughout
are themed to the quest (e.g. the Dirt Sapling quest rewards dirt, the Obsidian
quest rewards flint and steel) instead of generic XP.

## Requirements

This drops into a stock SkyFactory 4 instance. You need three extra mods that
SkyFactory 4 doesn't ship with — grab the exact versions below from CurseForge
(forgecdn.net CDN links, official source):

| Mod | Version | File |
|---|---|---|
| FTB Library | 5.4.7.2 | `FTBLib-5.4.7.2.jar` |
| FTB Quests | 1202.9.0.15 | `FTBQuests-1202.9.0.15.jar` |
| Item Filters | 1.0.4.2 | `ItemFilters-1.0.4.2.jar` (hard dependency of FTB Quests — verified via the jar's `required-after` annotation) |

Get them from:
- https://www.curseforge.com/minecraft/mc-mods/ftblib
- https://www.curseforge.com/minecraft/mc-mods/ftb-quests-forge
- https://www.curseforge.com/minecraft/mc-mods/item-filters

Drop all three `.jar` files into your instance's `mods/` folder.

## Installation

1. Back up your `config/` folder first (seriously, always back up before copying
   someone else's config into your instance).
2. Install the three mods above into `mods/`.
3. Copy this repo's `config/ftbquests/normal/` folder into your instance's
   `config/ftbquests/normal/` folder (create the path if it doesn't exist).
4. Launch the world. The quest book should populate automatically. If nothing
   shows up, check `logs/latest.log` for a line like
   `[FTB Quests]: Failed to read ...` — that means a file didn't parse (SNBT is
   picky about commas), and that specific error message tells you exactly which
   file and where.

### Optional: auto-give the Quest Book on first join

SkyFactory 4 already has a "give starting items" function that runs the first
time a player joins a new world (it's what hands you the torch, coffee, and
Builder's Wand). You can make it hand over the FTB Quests book too:

Open `config/triumph/functions/startingitems.txt` and add this line:

```
give @p ftbquests:book
```

This only fires for **new** worlds (or players who haven't hit the "tutorial"
gamestage yet). For an existing save, just run `/give @p ftbquests:book` once
yourself, or `/function triumph:startingItems` to re-trigger the whole starter
kit.

## Known rough edges

A handful of item IDs couldn't be fully verified against this exact pack build
and may need a quick JEI check / icon fix on your end:

- `tconstruct:cast` in the "First Casting" quest matches any cast regardless of
  NBT (intentional simplification, not a bug).
- A few Mystical Agriculture / Astral Sorcery item sources (e.g. where Aquamarine
  actually comes from in this pack) weren't fully traceable from config files
  alone — see the quest text for a "check JEI" nudge where relevant.
- The Mystical Agriculture branch's first quest hands you starter Inferium Seeds
  as a reward, because this pack disables both the normal ore-based and mob-drop
  sources for them (config/mysticalagriculture.cfg). Without that reward the
  whole branch is a dead end on a fresh world.

If something's flat-out broken (wrong icon, quest won't complete), open an issue
with the quest title and what you see — item ID typos are the most likely culprit
and easy to fix.

## License / disclaimer

This repo contains only FTB Quests `.snbt` data files (plain text configuration),
not any mod code or assets. It is not affiliated with the SkyFactory team,
LatvianModder, or FeedTheBeast. Use at your own risk; always back up your world
and config before installing.
