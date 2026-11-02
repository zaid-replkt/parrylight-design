<!-- from md/05-build-spec-D-backlog.md -->

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
