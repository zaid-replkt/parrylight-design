# Build spec D: backlog and build order

What to build first, in what order, and what done means, so the team can start on Monday without a planning meeting.

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

## D2. Tickets for the prototype and the vertical slice

Tickets are sized to one to three days; each has acceptance criteria an engineer or designer can check without asking. Ids are `P-` for prototype and `S-` for slice; the epic number in brackets.

**Prototype (weeks 1 to 6)**

| Id | Ticket | Acceptance criteria |
| --- | --- | --- |
| P-01 (1) | Fixed-step simulation with render interpolation | Simulation runs 60 Hz independent of frame rate; a 30 fps throttle changes nothing in a 60 s input replay (frame hashes equal) |
| P-02 (1) | Seeded RNG and replay buffer | Every random call takes the stage seed; the last 10 s of inputs replay to the same state |
| P-03 (2) | Touch router with OS timestamps | Touch-down event time is logged; a synthetic 50 ms frame stall does not change which window a tap lands in |
| P-04 (2) | Floating joystick | Appears under the thumb in the movement zone; dead zone 8 pt; full at 48 pt; resets on lift; mirrored in left-handed mode |
| P-05 (2) | Gesture classifier | Tap parries on down; a 12 pt move within 60 ms becomes a dodge in that direction; a 350 ms hold on an enemy pins it; unit tests for all three |
| P-06 (3) | Parry resolver | All branches in A2's pseudocode covered by tests: precise, soft, miss, red, buffer, spam 2 and 3, recovery |
| P-07 (3) | Damage formulas | A2 player and enemy formulas with the 40% defense floor; worked example reproduces to the integer |
| P-08 (3) | Riposte, stagger, Special meter | Riposte 1.5 s at 2x (Blade 3x); stagger 1.0 s; meter +16 per parry, +4 per hit, cast at 100 |
| P-09 (3) | Break and Execute | Elite bar 100, decay 10/s, broken 3 s, immune 8 s; Execute 6x ignoring defense; cinematic stub 600 ms |
| P-10 (4) | Enemy record loader | Thornback, Lunger, Seedspitter, Brute load from JSON with A4 fields; a bad field fails the load with a line number |
| P-11 (4) | Enemy state machine | All eight states; family overrides via data flags (shield, blink, projectile) |
| P-12 (4) | Telegraph module | One module owns colour, pose, sound, haptic and duration per attack; lint fails on a telegraph under 450 ms or a colour outside the four |
| P-13 (4) | Projectiles | Seed projectile is a parryable entity; reflection at 1.5x speed hits the first enemy |
| P-14 (5) | Width-locked camera | 9 units visible on 9:16, 9:19.5, 9:21 and 3:4; character at 45% height; lead and damping per A5 |
| P-15 (5) | Threat band and edge indicators | A windup originating under the band draws a chip above the band line; spawn markers 1 s ahead at the edge |
| P-16 (5) | Arena templates | `orchard_short` and `orchard_boss` grey-boxed with decorative margins |
| P-17 (6) | Parry feel pass | Hit stop 80 ms, flash, ring, haptic transient, sound with pitch-up on perfect; A/B build with an "attack button" control for the gate test |
| P-18 (6) | Grey-box stages 1-1 to 1-8 | Loaded from the stage schema; both bots pass (passive bot dies from 1-5 on) |
| P-19 (6) | Prototype HUD | Health, Special meter, room dots, Special button, Action button with Execute and Drink only |
| P-20 (6) | Gate 1 test kit | 20-person protocol: feel checklist, precise parry rate per stage, A/B preference; results sheet template |

**Vertical slice (weeks 7 to 16)**

| Id | Ticket | Acceptance criteria |
| --- | --- | --- |
| S-01 (7) | Stage schema and CI validation | JSON schema from design 11; CI fails on an invalid file; all B4 stages committed |
| S-02 (8) | Perfect bot | Parries on the hit frame, dodges reds, leaves rings; clears every world 1 stage with 0 damage in CI |
| S-03 (8) | Passive bot | Moves toward enemies, never defends; must die before the final room from 1-5 on; CI asserts it |
| S-04 (8) | Timing and dial report | Per stage: expected first-clear minutes, telegraph density, red share, simultaneous threats; written to a CSV in CI |
| S-05 (9) | Stage editor v1 | Desktop tool: edit rooms and spawns, 9:16 preview, run both bots, show the report |
| S-06 (10) | Level and XP | A1 table loaded from data; level-up at the exact thresholds; +1 skill point on even levels |
| S-07 (10) | Weapons and armour | A3 attack formula, cadence, hit shapes for Blade and Hammer; armour rules Bulwark and Quickstep; upgrade costs |
| S-08 (10) | Warden tree | 15 nodes from B2 with effects wired; respec |
| S-09 (10) | Boons | 19 world 1 boons from B1; offer algorithm with the seed; stack caps; expiry at stage end |
| S-10 (11) | Full HUD | All C2 elements and states; damage numbers setting; callouts |
| S-11 (11) | Action resolver | A5 priority, 200 ms arm, hold-lock, pulse; all C2 states |
| S-12 (12) | Map and Stage preview | C1 layouts; current stage centred; stars; loadout chip |
| S-13 (12) | Results and Failure | Reward animation, stars, unlock card; replay window with highlighted telegraph; advice lines from C4 |
| S-14 (12) | Hero, Forge (basic), Pause, Settings | Equip, upgrade, dismantle; settings in C5 with persistence |
| S-15 (13) | Save and resume | A6 schema; atomic writes; two rotating copies; resume at room start; migration harness with fixtures |
| S-16 (14) | Tutorial system | C3 steps as data; slow-motion on the simulation clock only; each step once |
| S-17 (15) | Analytics SDK and events | A7 envelope and 13 events; batching on stage end and background; dashboard shows the FTUE funnel |
| S-18 (16) | World 1 final art | Thornback family silhouettes, four variants, Brute; orchard templates; telegraph palette check against the world palette |
| S-19 (16) | Rootmaw | B6 script; intro pull-out; two breaks; finisher at 15% |
| S-20 (16) | World 1 audio | Telegraph sounds for 5 attack types, parry set, music loops at a shared tempo |
| S-21 (16) | Stages 1-9 to 1-25 authored | From B4; both bots pass; times within 20% of targets |
| S-22 (12) | Cold-start path | Splash to first parry under 30 s on a mid device with no account prompt |
| S-23 (15) | Perf budget check | 60 fps on the mid device class, 30 on low; slow frames under 5%; memory under 350 MB in world 1 |
| S-24 (16) | Gate 2 closed test | 300-install cohort; D1, funnel, first-clear times, parry curves reported against section 16 targets |

**Production tickets** are generated per world from the same shapes: one content ticket per block (five per world), one art ticket per family record, one boss ticket, three dungeon tickets, one trial-set ticket, plus the system epics 17 to 21 broken down the same way. The pattern above is the template; the production backlog is produced from B5 by the design lead at the start of week 17.

## D3. Definition of done and the content pipeline

**Definition of done per content type**

| Content | Done means |
| --- | --- |
| Enemy record | Fields complete per A4; silhouette distinct from every other family at 1 unit; two wind-up poses (parryable raised, unparryable lowered); telegraph lint passes; sounds for every attack; appears in the enemy encyclopedia with its one-line counter |
| Campaign stage | File validates; perfect bot clears with 0 damage; passive bot dies by the final room (world 2 onward: by room 3); dials within the block target (B5); first-clear estimate within 20% of the block target; three mastery objectives of different types; the "new decision" field filled and approved by a second designer; played once by a human on a 9:16 device and once on a 3:4 device |
| Boss | Script per B6; every attack rehearsed by a stage in 21 to 24; a no-damage clear is possible for the perfect bot; break count and finisher verified; intro and victory beats; unique Execute animation |
| Side dungeon | Three stages as above; the remix rule is visible in the first room; elite pair script; reward entry in the loot table |
| Trial | Type rule enforced by data flags; assists disabled; pass condition tested by both bots (perfect passes, passive fails) |
| Boon | Effect implemented as a rule hook, not a special case; stack cap; class exclusion; shows correctly on the pick card and the pause list; one automated test per boon |
| Skill node | Effect hook; tooltip string; respec returns it; one test |
| Ring affix | Value range by quality; cap across both rings enforced; re-roll excludes duplicates on the same ring |
| Quest or achievement | Progress hook fires from the right event; claim flow; string; a test that completes it in a scripted run |
| Screen | Matches C1 positions within 4 pt; all states reachable; back gesture and close control; safe-area insets on the device matrix; strings from the table, none hard-coded; analytics events on open and primary action |
| Cosmetic | Readability check against the telegraph palette and colour-blind modes; no silhouette change |

**Content pipeline** (one stage, start to ship)

1. Designer picks the block in B5 and writes the stage file in the editor (spawns, timings, rule parameters, boon pool, mastery, rewards from A1).
2. Editor runs schema validation and both bots locally; the designer adjusts until the dials and the time estimate are inside the targets.
3. Designer fills `new_decision` in the file; a second designer approves it in review or sends it back.
4. CI runs validation and both bots on the merge; failures block the merge.
5. Art attaches the arena template decoration and any new record's assets; the telegraph palette check runs on the world's palette.
6. QA plays the stage on the device matrix (one 9:16, one 9:19.5, one 3:4, one low-end Android) and checks the portrait readability list in design section 6.
7. The stage ships behind the world's unlock; analytics watch its first-attempt clear rate and deaths per clear for the thresholds in section 16; a stage outside them goes back to step 1 with the data attached.

**Weekly content cadence in production**: 10 stages across two designers, which with 268 remaining stages is 27 weeks; the schedule in section 17 allows 28. Bosses, dungeons and trials are inside that count (a boss counts as 4 stages of effort, a dungeon as 3, a trial as 1).

**Cuts in order, if the schedule slips**: third side dungeon per world (saves 21 stages), trials in worlds 4 and 5 (12), world 8's side dungeons (9). Campaign stages and bosses are never cut; the 30-hour target drops to about 26 hours after the first cut and is restored by the first content update.
