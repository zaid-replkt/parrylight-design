# Parrylight: Game Design Document

Portrait-only, single-player 2D mobile action RPG with auto-attack and tap-to-parry. Working title Parrylight (placeholder). As of 2 November 2026.

Start with `md/01-design.md` (the design, 18 sections), then the four build-spec files: A (formulas, state machines, schemas), B (every boon, skill, affix, stage, boss, quest, achievement), C (every screen and string), D (epics, tickets, definition of done). `GDD-Parrylight-complete.md` is all five in one file. `data/` holds the same numbers in CSV and JSON for tooling. `manifest.json` lists every file.

| File | What it is |
| --- | --- |
| [md/01-design.md](md/01-design.md) | Design (sections 1 to 18) |
| [md/02-build-spec-A-formulas-and-systems.md](md/02-build-spec-A-formulas-and-systems.md) | Build spec A: formulas and systems |
| [md/03-build-spec-B-content-tables.md](md/03-build-spec-B-content-tables.md) | Build spec B: content tables |
| [md/04-build-spec-C-screens-and-copy.md](md/04-build-spec-C-screens-and-copy.md) | Build spec C: screens and copy |
| [md/05-build-spec-D-backlog.md](md/05-build-spec-D-backlog.md) | Build spec D: backlog and build order |
| [GDD-Parrylight-complete.md](GDD-Parrylight-complete.md) | All five tabs in one Markdown file |
| [data/level_table.csv](data/level_table.csv) | Level 1 to 60: health, attack, XP |
| [data/stage_xp.csv](data/stage_xp.csv) | XP, coins and materials per stage, all 200 campaign stages |
| [data/weapons.csv](data/weapons.csv) | Weapon attack by family, rarity and level |
| [data/enemies.json](data/enemies.json) | Enemy family base records, scaling, traits |
| [data/remote_config_defaults.json](data/remote_config_defaults.json) | Remote-config keys and defaults |
| [data/stage_example_w2-s07.json](data/stage_example_w2-s07.json) | Stage file example matching the schema in design section 11 |
| [images/03-stage-loop.png](images/03-stage-loop.png) | Stage loop diagram |
| [images/06-portrait-layout.png](images/06-portrait-layout.png) | Portrait screen layout |
| [images/09-hours-by-world.png](images/09-hours-by-world.png) | Hours by world chart |
| [images/17-production-timeline.png](images/17-production-timeline.png) | Production timeline |

Images referenced by `md/01-design.md` live in `images/`, each with a text version (`.md`) beside the PNG.

**If your reader truncates long files:** use `sections/` (one file per section, 42 files, each under 25 KB; `sections/README.md` is the reading order) instead of `md/`, or `git clone` the repo.
