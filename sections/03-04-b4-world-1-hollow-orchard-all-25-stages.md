<!-- from md/03-build-spec-B-content-tables.md -->

## B4. World 1, Hollow Orchard: all 25 stages

World 1 uses four enemy records and no arena rule, so every stage is about the grammar: white means tap, red means swipe, a projectile can be sent back. XP and coins follow A1 (B(1) = 157; coins are half of XP). Arena templates: `orchard_short` (16 tall) for stages with up to 3 rooms, `orchard_long` (24) for 4 or more, `orchard_boss` (16) for stage 25.

**World 1 enemy records** (base values in A4 scale; all are Thornback-family sprites with distinct silhouettes)

| Code | Record | Difference from Thornback |
| --- | --- | --- |
| T | Thornback | the base record |
| L | Lunger | Health 0.8x; one attack: Lunge, red, 900 ms, power 18, dashes 2.5 units; cooldown 2.8 s |
| S | Seedspitter | Health 0.5x; holds at 5 units; Seed: white projectile, 650 ms, power 9, speed 6 units/s, reflectable; cooldown 2.6 s |
| U | Burrower | Health 1.0x; Burrow: vanishes, yellow marker at the player's position fills 1,200 ms, red emergence hit power 16 radius 1.2; then behaves as T for 6 s |
| B | Brute | Elite Thornback (A4 elite multipliers); Sweep: white, 800 ms, 150 degree arc, power 15; traits per stage |

Spawn notation: `2T top` = two Thornbacks from the top edge; `bot` = bottom edge; `+6s` = spawns 6 s after the room starts; `rest` = a rest room with a chest and one potion; `boon` after a room = a boon pick follows it.

| Stage | Rooms | Mastery objectives | XP / coins | First-clear extra | New decision |
| --- | --- | --- | --- | --- | --- |
| 1-1 | R1: 1T top (never attacks) · R2: 1T top, telegraph 1,000 ms, game slows on first flash · R3: 2T top | parry 3 · no damage in R3 · under 1:30 | 128 / 64 | none | tap on the white flash |
| 1-2 | R1: 1L top, game slows on first red · R2: 1T + 1L top · R3: 2T top, 1L bot +4s | dodge 3 lunges · no damage in R1 · under 2:00 | 131 / 66 | 1 potion | red means swipe, not tap |
| 1-3 | R1: 2T top, boon · R2: 2T top + 1L bot · R3: 3T top | cast the Special twice · no damage in R1 · under 2:30 | 133 / 67 | 2 potions | spend the Special or hold it |
| 1-4 | R1: 2T top · R2: rest (chest: 3 Orchard Sap) · R3: 2T top + 1L bot +5s; scripted hit to 35% if above it, Drink prompt | open the chest · parry 8 · no damage in R3 | 136 / 68 | 60 coins | the Action button changes with context |
| 1-5 | R1: 1T top + 1T bot · R2: 2T top + 1T bot +3s · R3: 2T top + 2T bot | parry 10 · no damage in R2 · under 2:30 | 138 / 69 | none | threats from both edges; turn, do not run |
| 1-6 | R1: 2L top · R2: 2T top + 1L bot, boon · R3: gauntlet 2 waves (2T top; 2T top + 1L bot) | dodge 5 · no potion · under 3:00 | 141 / 70 | Common armour, Bulwark | waves with no pause between them |
| 1-7 | R1: 3T top, boon · R2: 2T top + 2L bot · R3: 3T top + 1L bot +6s | parry 15 · no damage in R1 · perfect parry 3 | 143 / 71 | none | parry rhythm against three |
| 1-8 | R1: 2T top · R2: 3T top + 1L bot, boon · R3: 3T top + 2L bot +4s | no damage in R2 · parry 12 · under 3:00 | 146 / 73 | Hammer family unlocked, Common Hammer | choose a weapon for the stage |
| 1-9 | R1: 1S top (seed is slow: 4 units/s this stage) · R2: 1S top + 2T top, boon · R3: 2S top + 1L bot | reflect 4 seeds · no damage in R1 · under 3:00 | 148 / 74 | 1 potion | a projectile is a parry, and it goes back |
| 1-10 | R1: 2S top · R2: 2T top + 1S top, boon · R3: 3T top + 1S top + 1L bot +5s | kill both Seedspitters first in R1 · reflect 6 · no damage in R3 | 151 / 75 | none | kill order: ranged first |
| 1-11 | R1: 2T top + 1L bot · R2: rest · R3: gauntlet 3 waves (3T top; 2T top + 2L bot; 2S top + 2T top) | no potion · parry 20 · under 3:30 | 153 / 76 | none | manage health across a long gauntlet |
| 1-12 | R1: 2T top · R2: 2T top + 1S top, boon · R3: B (Armoured) top, adds 2T top every 12 s | break the Brute twice · no potion · under 4:00 | 156 / 78 | 150 coins, 10 Orchard Sap | elites: parries build break, Execute ends it |
| 1-13 | R1: 3T top · R2: 2S top + 2T bot, boon · R3: 2L bot + 2T top + 1S top +4s | reflect 5 · dodge 4 · no damage in R2 | 158 / 79 | none | ranged behind melee |
| 1-14 | R1: 2L (Hasty) top + 1S top · R2: 4T top, boon · R3: 2S top + 2L bot · R4: 3T top + 1L bot +3s | dodge 6 · no damage in R4 · under 4:00 | 161 / 80 | none | faster reds |
| 1-15 | R1: 3T top · R2: B (Hasty) top · R3: boon after; 2S top + 2T bot · R4: 3T top + 2L bot +5s | break the Brute · parry 20 · no potion | 163 / 81 | none | a faster elite before the stage is over |
| 1-16 | R1: 2T top, boon · R2: gauntlet 3 waves (3T top; 2T top + 2L bot; 3T top + 1S top + 1L bot) · R3: rest · R4: 4T top + 1S top | no damage in R2 · reflect 3 · under 4:30 | 166 / 83 | second loadout slot | save potions for the long room |
| 1-17 | R1: 2S top + 1T top · R2: 2S top + 2L bot, boon · R3: rest · R4: 3T top + 2S top +6s | reflect 8 · no damage in R2 · kill both Seedspitters in R4 within 20 s | 168 / 84 | none | reflect while something is in your face |
| 1-18 | R1: B top + 1S top · R2: boon after; 3L bot + 1T top · R3: 2T top + 2L bot + 2S top +4s (cap 6) | break the Brute · dodge 6 · no potion | 171 / 85 | 1 potion | the elite is not the priority |
| 1-19 | R1: 4T top · R2: 3L bot, boon · R3: 2U top (Burrower introduced; marker 1,500 ms this stage) · R4: B (Hasty) top + 2T bot +8s | dodge both emergences · parry 20 · under 4:30 | 173 / 86 | none | yellow marker on you: move |
| 1-20 | R1: 3T top + 1L bot, boon · R2: 2T top + 2L bot, boon · R3: 2S top + 2T bot, boon · R4: 3L bot + 1S top · R5: B (Volatile) top + 2T bot +6s | no potion · no damage in R4 · under 5:30 | 176 / 88 | 100 coins, 8 Orchard Sap | five rooms, no boon late; leave the Volatile ring |
| 1-21 | R1: B top (Sweep only) · R2: 2T top + 1U bot, boon · R3: B top + 1S top | parry 6 Sweeps · no damage in R1 · under 3:30 | 178 / 89 | none | boss rehearsal: the wide white sweep |
| 1-22 | R1: 3L bot · R2: 2L top + 2L bot, boon · R3: 2U top + 2T bot | dodge 8 · no potion · under 3:30 | 181 / 90 | none | boss rehearsal: reds from both sides |
| 1-23 | R1: 3S top · R2: 2S top + 2T top, boon · R3: 3S top + 1L bot | reflect 10 · reflect 3 seeds inside 1 s · no damage in R1 | 183 / 91 | none | boss rehearsal: the volley |
| 1-24 | R1: 2U top + 1T bot · R2: rest · R3: B (Hasty) top + 2U bot, boon · R4: 3T top + 2L bot + 1S top | dodge 4 emergences · break the Brute · under 4:30 | 186 / 93 | 2 potions | boss rehearsal: the burrow |
| 1-25 | Boss: Rootmaw (B6) | no damage in phase 1 · Execute twice · under 6:00 | 565 / 282 | Spear family unlocked, Common Spear, 300 coins, 20 Orchard Sap, title Orchard Keeper, world 2 opens | the boss script |

**Boon pools** for world 1 (five ids per stage, rotating; all from the "all" availability set): riposte\_plus, quick\_feet, heavy\_hands, second\_wind, potion\_plus, chest\_sense, stagger\_long, special\_on\_room, parry\_chain, perfect\_refund, lone\_edge, crowd\_edge, last\_stand, attack\_up, health\_up, crit\_up, haste, swift, tough. Each stage lists 5 to 8 of these in its file; no world 1 stage offers a status boon because world 1 weapons have no status trait until level 3.

**Validation expectations** (A5 bots): the passive bot must die by R3 in every stage from 1-5 onward; the perfect bot must clear every stage with zero damage; expected first-clear times 1-1 at 2 minutes rising to 1-24 at 6 minutes; 1-25 at 9 minutes.
