<!-- from md/05-build-spec-D-backlog.md -->

## D1. Epics in build order

22 epics across the four phases in design section 17. The prototype is epics 1 to 6 only; nothing else starts until gate 1 passes. Each epic names the spec it implements, so a ticket is "implement A5 player state machine", not a paragraph.

| # | Epic | Phase | Owner | Depends on | Implements | Exit criteria |
| --- | --- | --- | --- | --- | --- | --- |
| 1 | Simulation core | Prototype | Gameplay eng | none | A5 (fixed step, determinism, replay buffer) | 60 Hz step, same inputs replay to the same frame hashes on two devices |
| 2 | Input and gestures | Prototype | Gameplay eng | 1 | A5 gesture classifier, design 5 zones | Touch-down timestamps from the OS; parry fires on down; swipe within 60 ms converts to dodge |
| 3 | Combat resolution | Prototype | Gameplay eng | 1, 2 | A2 (damage, parry resolver, break, status) | Resolver unit tests for precise, soft, miss, spam, red, buffer; worked example in A2 reproduces |
| 4 | Enemy framework | Prototype | Gameplay eng | 3 | A4 records, A5 enemy state machine, telegraph module | Thornback, Lunger, Seedspitter, Brute from data; telegraph lint runs |
| 5 | Camera and portrait frame | Prototype | UI eng | 1 | A5 camera, design 6 | Width-locked 9 units; aspect matrix 9:16 to 1:1 letterboxed; threat-band indicators |
| 6 | Prototype feel | Prototype | Animator, audio | 3, 4 | design 14 parry feel, haptics | Feel checklist passed in a 20-person test; gate 1 |
| 7 | Stage data and loader | Slice | Tools eng | 4 | design 11 schema, B4 | All 25 world 1 files load; schema validation in CI |
| 8 | Bots and validation | Slice | Tools eng | 7 | A5, design 11 steps 2 to 4 | Perfect and passive bots run headless on all world 1 stages in CI under 10 minutes |
| 9 | Stage editor | Slice | Tools eng | 7, 8 | design 15 tooling | Edit a stage, preview on 9:16, run both bots, see the dials |
| 10 | Player progression | Slice | Gameplay eng | 3 | A1, A3, B2 (Warden tree only) | Level 1 to 15 reachable in world 1 with the XP table exactly |
| 11 | Combat HUD and Action button | Slice | UI eng | 2, 5 | C2 | All HUD states; Action resolver with the 200 ms arm; no two options |
| 12 | Shell screens | Slice | UI eng | 10 | C1 (Map, Preview, Loadout, Results, Failure, Pause, Hero, Forge basic, Settings) | Cold start to first parry under 30 s on a mid device |
| 13 | Save and resume | Slice | Tools eng | 10 | A6 | Kill the app mid-room; relaunch resumes at the room start with boons; migration test harness |
| 14 | Tutorial system | Slice | UI eng, designer | 11, 12 | C3 | All 20 steps data-driven; each fires once |
| 15 | Analytics | Slice | Tools eng | 12 | A7 events | Every event in A7 visible in the dashboard from a device build |
| 16 | World 1 content | Slice | Content designers, artists | 7 to 9 | B4, B6 Rootmaw, design 14 art | 25 stages pass both bots; first-clear times within 20% of targets; gate 2 |
| 17 | Worlds 2 to 8 content | Production | Content designers, artists | 16 | B5, B6, B7, A4 families | 268 stages pass validation; dials within block targets |
| 18 | Classes, trees, Forge full | Production | Gameplay eng | 10 | B2 all, A3, B3 | Ranger and Mystic; rings, re-roll, refine, transmute, craft |
| 19 | Engagement layer | Production | Gameplay eng, UI eng | 12, 13, 15 | design 13, B8, C4 | Calendar, streak, dailies, weeklies, achievements, season track, return rewards, weekly challenge |
| 20 | Monetization and stores | Production | Tools eng | 13, 19 | design 12, B9 | Receipts validated; pass, cosmetics, bundles, rewarded ads, ad-free; odds disclosure not needed (no random purchases) |
| 21 | Cloud save, accounts, localization hooks | Production | Tools eng | 13 | A6 cloud rules, design 15 | Conflict prompt works; strings externalised; Arabic RTL menus verified |
| 22 | Soft launch tooling | Soft launch | Tools eng | 15, 20 | A7 remote config | Config keys live; cohorts split by config version |

**Parallel lanes in the slice**: tools (7, 8, 9, 13, 15) run beside gameplay (10, 11) and UI (12, 14); content (16) starts the day the loader (7) accepts a file and does not wait for the editor (9). **Critical path**: 1, 3, 4, 7, 8, 16.
