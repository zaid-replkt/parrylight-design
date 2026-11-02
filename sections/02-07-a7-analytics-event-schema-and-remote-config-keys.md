<!-- from md/02-build-spec-A-formulas-and-systems.md -->

## A7. Analytics event schema and remote-config keys

Thirteen events with typed fields and a common envelope, and 38 remote-config keys that cover every number a live balance change might need. Events are batched and sent on stage end and app background; nothing is sent per frame.

**Envelope on every event**: `event` (string), `ts` (ISO 8601 UTC), `player_id` (uuid), `session_id` (uuid), `build` (string, e.g. 1.0.3+412), `platform` (ios | android), `device_class` (low | mid | high, from a benchmark at first launch), `world` (int), `stage` (string id), `class` (string), `weapon_family` (string), `weapon_rarity` (string), `level` (int), `assist_flags` (string list).

| Event | Fields | Type |
| --- | --- | --- |
| app\_open | cold (bool), seconds\_since\_last\_open (int), return\_reward\_shown (bool) | per launch |
| tutorial\_step | step (string), seconds\_from\_app\_open (int) | FTUE funnel |
| stage\_start | mode (campaign, dungeon, trial, refight, challenge), attempt\_n (int), potions (int), loadout (object) |  |
| stage\_end | result (win, fail, quit), duration\_s (int), rooms\_cleared (int), deaths (int), potions\_used (int), boons (string list), damage\_taken (int), parries\_precise (int), parries\_soft (int), parries\_missed (int), dodges\_ok (int), executes (int), stars\_earned (int list), xp (int), coins (int), materials (int) | the core event |
| parry | result (precise, soft, miss, spam\_blocked), enemy\_family (string), attack\_id (string), delta\_ms (int, signed: tap time minus hit frame), room (int) | sampled 100% in soft launch, 20% after |
| dodge | absorbed\_hit (bool), direction (string), trigger (swipe, button) | sampled as above |
| death | attack\_id (string), enemy\_family (string), room (int), health\_history (int list, 10 s at 10 Hz), seed (int) |  |
| boon\_pick | offered (string list), chosen (string), room (int) |  |
| equip\_change | slot (string), from\_item (string), to\_item (string), context (preview, hub) |  |
| economy | action (upgrade, craft, reroll, refine, dismantle, respec, potion\_buy), item (string), coins\_delta (int), materials\_delta (int), shards\_delta (int), balances (object) |  |
| engagement | action (calendar\_claim, streak\_day, quest\_complete, quest\_claim, first\_win, challenge\_play, return\_claim, season\_tier, event\_stage), id (string), value (int) |  |
| monetization | action (offer\_shown, offer\_dismissed, purchase, ad\_offered, ad\_completed, ad\_skipped), offer\_id (string), price\_usd (float), context (string) |  |
| perf | fps\_p50 (float), fps\_p05 (float), slow\_frames\_pct (float), memory\_mb (int), thermal (string), load\_s (float), scene (string) | per stage end |

Settings changes send `engagement` with action `setting_change` and id = the setting key.

**Remote-config keys** (type, default; read at app open and on stage start, never mid-stage)

| Group | Key | Default |
| --- | --- | --- |
| Parry | parry.precise\_ms | 200 |
|  | parry.soft\_ms | 450 |
|  | parry.recovery\_ms | 300 |
|  | parry.input\_buffer\_ms | 100 |
|  | parry.spam\_window\_ms | 400 |
|  | parry.spam\_precise\_ms | 120 |
|  | parry.assist\_precise\_ms | 280 |
|  | parry.assist\_soft\_ms | 550 |
|  | parry.perfect\_ms | 60 |
|  | parry.riposte\_s | 1.5 |
|  | parry.special\_gain | 16 |
| Dodge | dodge.duration\_ms | 250 |
|  | dodge.iframes\_ms | 180 |
|  | dodge.cooldown\_ms | 800 |
| Telegraph | telegraph.floor\_ms | 450 |
|  | telegraph.world\_shrink | 0.04 |
|  | telegraph.assist\_mult | 1.2 |
| Enemy | enemy.M (list of 8) | 1.00, 2.25, 3.16, 5.06, 6.44, 7.97, 11.05, 13.66 |
|  | enemy.A (list of 8) | 1.00, 1.92, 3.00, 4.17, 5.75, 7.50, 9.42, 11.58 |
|  | enemy.stage\_growth | 0.012 |
|  | enemy.elite\_health\_mult | 4.0 |
|  | enemy.cap\_campaign | 6 |
|  | enemy.cap\_trial | 8 |
| Break | break.elite\_decay\_per\_s | 10 |
|  | break.boss\_decay\_per\_s | 6 |
|  | break.broken\_s | 3.0 |
|  | break.execute\_mult | 6 |
| Economy | econ.stage\_xp\_B (list of 8) | 157, 717, 1561, 3108, 4801, 6758, 8957, 8296 |
|  | econ.coin\_ratio | 0.5 |
|  | econ.repeat\_mult | 0.2 |
|  | econ.materials\_per\_stage | 3 |
|  | econ.materials\_per\_boss | 12 |
|  | econ.potion\_cost | 60 |
|  | econ.reroll\_shards | 3 |
| Engagement | eng.calendar\_values (object by world) | B8 |
|  | eng.streak\_forgiveness\_per\_week | 1 |
|  | eng.return\_days | 3 |
|  | eng.notification\_min\_days\_played | 3 |
| Monetization | mon.starter\_bundle\_after\_stage | w1-s08 |
|  | mon.rewarded\_double\_per\_day | 5 |

A remote-config change is logged as an `engagement` event with action `config_applied` and the changed keys, so cohorts can be split by config version.
