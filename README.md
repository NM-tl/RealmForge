# RealmForge

A chat-based 4X strategy game engine, defined entirely as JSON rule files. One player message = one game turn. The AI (ChatGPT, Claude, or any capable chat model) acts as the game engine, narrator, and rules arbiter.

## How it works

`PROMPT.md` is the text you paste into a new chat. It points the AI at the rule files below and tells it how to run the game. The AI reads the JSON as its rulebook — buildings, research, combat, world generation, diplomacy, event system, and the exact turn-report format — and then starts the game.

## Repository structure

```
RealmForge/
├── engine/
│   ├── Part01_core.json          # design principles, new game setup, turn structure, terrain/resources
│   ├── Part02_buildings.json     # city & tile buildings
│   ├── Part03_research.json      # technology tree (Stone → Copper → Bronze → Iron)
│   ├── Part04_army.json          # army, experience, equipment, combat
│   ├── Part05_world.json         # map generation, AI kingdoms, rulers, titles, diplomacy, chronicle
│   ├── Part06_population.json    # citizen professions & economy
│   ├── Part07_events.json        # random event system
│   ├── Part08_turn_report.json   # mandatory per-turn output format
│   ├── Part09_victory.json       # victory / defeat / endless mode
│   ├── manifest.json             # ordered index of all parts, for AI clients with web access
│   └── RealmForge_Full_v1.json   # all parts merged into one file (fallback, no web access needed)
├── PROMPT.md                     # paste this into a new chat to start the game
└── README.md
```

## Starting a game

**Option A — AI with web/browsing access** (Claude with web fetch, a Custom GPT with Actions/browsing, etc.)
Paste `PROMPT.md`. It contains the raw URLs to `manifest.json` and each part; the AI fetches them itself and starts the game.

**Option B — AI without web access** (plain ChatGPT chat, no browsing)
Upload or paste `RealmForge_Full_v1.json` directly into the chat, then paste `PROMPT.md`. Nothing needs to be fetched — it's all in one file.

## Versioning

Each part is independently versioned in `manifest.json`. Add new parts (e.g. trade, espionage, naval combat) by dropping a new file into `engine/`, adding it to `manifest.json`, and re-running the merge script to update `RealmForge_Full_v1.json`.

## Contributing

Keep the JSON format consistent with existing parts: a single top-level key per file, a `rules` array for AI-facing instructions in plain English, and structured objects (`id`, `cost`, `effect`, `requires`, `unlocks`) for anything mechanical. Avoid top-level key collisions with existing parts.
