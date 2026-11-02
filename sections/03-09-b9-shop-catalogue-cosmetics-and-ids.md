<!-- from md/03-build-spec-B-content-tables.md -->

## B9. Shop catalogue, cosmetics and ids

**Launch catalogue** (prices are USD placeholders for store tiers; gem prices in the gem column)

| Id | Item | Money | Gems | Notes |
| --- | --- | --- | --- | --- |
| pass\_s1 | Season pass, season 1 | 7.99 | not for gems | 5-week season |
| bundle\_starter | Starter bundle: Orchard Keeper cape, 10 potions, 2,000 coins | 2.99 |  | once, after 1-8 |
| pack\_supporter | Supporter pack: Gilded set (weapon, armour, parry effect) and the Patron badge | 19.99 |  |  |
| adfree | Ad-free: rewarded-ad rewards granted directly | 4.99 |  | one-time |
| gems\_s / gems\_m / gems\_l | 120 / 650 / 1,400 gems | 1.99 / 9.99 / 19.99 |  |  |
| skin\_w\_\* (12) | Weapon skins: 2 per family, plus 2 seasonal |  | 180 | no stats |
| skin\_a\_\* (6) | Armour skins: Orchard, Salt, Lantern, Clockwork, Ember, Frost |  | 220 |  |
| fx\_parry\_\* (6) | Parry effects: Spark, Frost, Ember, Arc, Petal, Ink |  | 150 |  |
| fx\_exec\_\* (4) | Execute cinematics: Guillotine, Overhead, Pierce, Shatter |  | 300 |  |
| frame\_\* (10) | Profile frames |  | 80 | plus 12 calendar frames, not sold |
| title\_\* | Titles |  | 60 | most are earned, 6 are sold |
| slot\_loadout\_3 | Third loadout slot |  | 200 | second slot is earned at 1-16 |

Gem earn rate check: the campaign's achievements, stars and season track pay about 2,400 gems over the 30-hour path, enough for two skins, a parry effect and an Execute cinematic without spending.

**Cosmetic rules**: no cosmetic changes a silhouette's readability (weapon skins keep the family's outline; armour skins keep the character's outline); parry effects are tested against the telegraph palette and the colour-blind modes; Execute cinematics keep the 600 ms duration.

**String and id conventions** (used by every table in this doc and by the analytics in A7)

| Thing | Pattern | Example |
| --- | --- | --- |
| Stage | `w<world>-s<stage, 2 digits>` | w3-s07 |
| Side dungeon stage | `w<world>-d<n>-s<n>` | w4-d2-s3 |
| Trial | `w<world>-t<type>` | w6-tmirror |
| Boss and re-fight | `w<world>-boss`, `w<world>-boss-m<modifier set>` | w2-boss-m1 |
| Enemy record | `<family>[_<variant>]`, elites `<family>_elite_<name>` | wisp\_flicker, shellback\_elite\_warden |
| Attack | `<record>.<attack>` | rootmaw.sweep |
| Boon | ids in B1 | parry\_chain |
| Skill node | ids in B2 | wa3 |
| Item instance | `inv_<4 hex>` | inv\_0f3a |
| Affix | ids in B3 | crit\_chance |
| Quest | `dq_*`, `wq_*`, season `sq_*` | dq\_parry\_20 |
| Achievement | `ach_<group>_<slug>` | ach\_parry\_chain50 |
| Offer | ids in the catalogue | bundle\_starter |
| UI string | `ui.<screen>.<element>`; combat callouts `cb.<event>` | ui.results.next\_stage, cb.perfect |

All player-facing strings live in one string table keyed by these ids (C3 and C4 list the launch copy); no string is hard-coded in a scene.
