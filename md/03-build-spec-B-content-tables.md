# Build spec B: content tables

The complete content lists the design tab refers to. Content designers author stages from B4 and B5; everything else here is final launch scope unless a gate cuts it.

## B1. Boons (40)

28 rule boons and 12 stat boons. A stage's pool lists 5 to 8 ids from this table; the offer algorithm (A5) shows two rule boons and one stat boon. All boons expire at stage end. "Max" is the stack cap within one stage.

**Rule boons**

| Id | Name | Effect | Max | Availability |
| --- | --- | --- | --- | --- |
| riposte\_plus | Long Riposte | Riposte window +0.5 s | 2 | all |
| reflect\_all | Mirror Guard | Precise parries reflect projectiles with any weapon; reflected damage 1.5x weapon attack | 1 | world 2+ |
| quick\_feet | Quick Feet | A dodge within 2 s of a previous dodge costs no charge | 1 | all |
| chill\_on\_parry | Frost Guard | Precise parry applies Chill to the attacker | 1 | world 3+ |
| burn\_on\_parry | Ember Guard | Precise parry applies Burn | 1 | world 3+ |
| shock\_on\_parry | Arc Guard | Precise parry Shocks: 50% of weapon attack jumps to the nearest other enemy | 1 | world 3+ |
| bleed\_on\_parry | Razor Guard | Precise parry adds one Bleed stack | 1 | world 2+ |
| second\_wind | Second Wind | Once per stage, at 20% health, heal 25% | 1, pick-once | all; excluded if armour rule is Second Wind |
| heavy\_hands | Heavy Hands | Riposte hits knock the target back 1 unit | 1 | all |
| breaker | Breaker | Parries build 50% more break | 2 | world 2+ |
| overcharge | Overcharge | Special meter can reach 150; at 150 the Special casts at 1.5x | 1 | world 3+ |
| echo | Echo | The Special casts a second time at 50% power, 0.5 s later | 1 | world 4+ |
| soft\_steel | Soft Steel | Soft parries negate all damage (still no riposte or break) | 1 | world 4+; excluded from trials |
| perfect\_refund | Perfect Step | A perfect parry (first 60 ms) refunds a dodge charge | 1 | all |
| hunter | Hunter's Mark | Pinned enemies take +20% damage | 1 | all |
| crowd\_edge | Crowd Edge | +8% damage per enemy within 2 units, up to +32% | 1 | all |
| lone\_edge | Duelist | +25% damage while exactly one enemy is alive | 1 | all |
| thorns | Thorns | An unparried hit deals 50% of its damage back to the attacker | 1 | all |
| potion\_plus | Deep Draught | Potions heal 50% instead of 35% | 1 | all |
| chest\_sense | Forager | Rest rooms hold a second potion; chests give +50% materials | 1 | all |
| stagger\_long | Long Stagger | Stagger lasts 1.5 s (elite 0.9 s) | 1 | all |
| execute\_heal | Reaper's Rest | Execute heals 15% of max health | 1 | world 2+ |
| special\_on\_room | Opening Act | Special meter +30 at the start of each room | 1 | all |
| parry\_chain | Rhythm | Each consecutive precise parry without taking damage adds +5% damage, up to +50%; a hit resets it | 1 | all |
| dash\_strike | Dash Strike | Dodging through an enemy deals 1.0x weapon attack to it | 1 | world 3+ |
| telegraph\_sense | Foresight | Telegraphs last 15% longer | 1 | all; excluded from trials |
| iron\_will | Iron Will | No Hit state: you can parry while taking damage | 1 | world 5+ |
| last\_stand | Last Stand | Under 30% health, +30% damage | 1 | all |

**Stat boons**

| Id | Name | Effect per stack | Max |
| --- | --- | --- | --- |
| attack\_up | Keen Edge | +10% attack | 5 |
| health\_up | Hardy | +10% max health, and heals the added amount | 5 |
| crit\_up | Lucky Edge | +6% crit chance | 4 |
| crit\_dmg | Vicious | Crit multiplier +0.25 (2.0 becomes 2.25, 2.5, 2.75) | 3 |
| haste | Haste | +8% attack cadence | 3 |
| swift | Swift | +8% move speed | 3 |
| tough | Tough | +3 defense, scaled by the square root of M(w) | 3 |
| special\_gain | Attuned | +25% Special charge from all sources | 2 |
| burn\_dmg | Hot Coals | Burn deals 6% per tick instead of 4% | 2 |
| chill\_long | Deep Frost | Chill lasts 5 s instead of 3 | 2 |
| shock\_wide | Fork | Shock jumps to two enemies | 2 |
| bleed\_cap | Open Wounds | Bleed stacks to 5 instead of 3 | 1 |

**Class exclusions.** Warden never sees Thorns (its parry heal covers the niche); Ranger never sees Foresight; Mystic never sees Overcharge (its meter is already larger). Boons that reference a status the equipped weapon or picked boons cannot apply are excluded from the offer (for example Hot Coals without any Burn source).

## B2. Skill trees (45 nodes)

Three classes, three branches each, five nodes per branch, one point per node, nodes taken in order within a branch. Every node is a rule or a threshold change, so the tree reads as a list of play-style decisions. Ids are `w`, `r`, `m` plus branch letter and tier.

**Warden** (parry and endurance)

| Branch | Tier | Id | Name | Effect |
| --- | --- | --- | --- | --- |
| Bastion | 1 | wa1 | Firm Guard | Soft parry tier extends from 450 to 500 ms |
| Bastion | 2 | wa2 | Steady Hands | Spam penalty resets after 300 ms instead of 400 |
| Bastion | 3 | wa3 | Shield Mind | Precise parry heal 3% becomes 5% |
| Bastion | 4 | wa4 | Unbroken | A precise parry during the riposte window extends it by 0.5 s (max 3 s) |
| Bastion | 5 | wa5 | Bulwark Stance | Holding the defense zone for 400 ms raises a guard: 50% damage reduction, parries still work; moves at 0.5x |
| Vitality | 1 | wv1 | Thick Skin | +5% max health |
| Vitality | 2 | wv2 | Potion Lore | Potions heal 45% |
| Vitality | 3 | wv3 | Resolve | Second Wind triggers at 30% health and heals 30% (stacks with armour rule as a second trigger) |
| Vitality | 4 | wv4 | Stone Feet | Immune to push from hazards (tide, conveyor, wind) |
| Vitality | 5 | wv5 | Last Wall | Under 25% health, defense doubles |
| Retaliation | 1 | wr1 | Counter Edge | Riposte multiplier 2.0 becomes 2.3 (Blade 3.0 becomes 3.3) |
| Retaliation | 2 | wr2 | Heavy Counter | The first riposte hit after each parry staggers elites for 0.4 s |
| Retaliation | 3 | wr3 | Breakwater | Parries on bosses build +4 break |
| Retaliation | 4 | wr4 | Executioner | Execute multiplier 6 becomes 8 |
| Retaliation | 5 | wr5 | Retribution | Every third consecutive precise parry fires a free Special at 50% power |

**Ranger** (dodge and targeting)

| Branch | Tier | Id | Name | Effect |
| --- | --- | --- | --- | --- |
| Fleet | 1 | rf1 | Light Step | Dodge cooldown 800 becomes 650 ms |
| Fleet | 2 | rf2 | Long Step | Dodge distance +30% |
| Fleet | 3 | rf3 | Phase Step | i-frames 180 becomes 220 ms |
| Fleet | 4 | rf4 | Third Charge | Three dodge charges |
| Fleet | 5 | rf5 | Afterimage | Dodging through an enemy's windup cancels that attack |
| Marksman | 1 | rm1 | Sharp Eye | Crit chance +5% |
| Marksman | 2 | rm2 | Pin Master | Pin lasts 10 s and marks for +15% damage taken (replaces the base +15% mark, stacks with Hunter's Mark boon) |
| Marksman | 3 | rm3 | Ricochet | Reflected projectiles hit a second enemy |
| Marksman | 4 | rm4 | Deadeye | Ranged families (Chakram, Wand) +20% attack |
| Marksman | 5 | rm5 | Headshot | Crits on marked enemies deal 3.0x |
| Hunter | 1 | rh1 | Tracker | Enemies below 20% health are outlined; auto-attack prefers them |
| Hunter | 2 | rh2 | Opportunist | Hits on staggered or Chilled enemies +15% |
| Hunter | 3 | rh3 | Quick Draw | Special meter +6 per hit instead of +5 |
| Hunter | 4 | rh4 | Trapper | Dash Strike boon effect is always on at 0.6x |
| Hunter | 5 | rh5 | Apex | Each kill grants +4% attack for the room, up to +40% |

**Mystic** (Special and status)

| Branch | Tier | Id | Name | Effect |
| --- | --- | --- | --- | --- |
| Resonance | 1 | ms1 | Attunement | Special charge from parries +25% |
| Resonance | 2 | ms2 | Reservoir | Meter 150 becomes 200; casts still cost 100 |
| Resonance | 3 | ms3 | Aftershock | Special effects last +50% |
| Resonance | 4 | ms4 | Twin Cast | Casting at 200 fires twice |
| Resonance | 5 | ms5 | Cadence | Each precise parry during a Special's effect adds +0.5 s to it |
| Elements | 1 | me1 | Kindling | Burn ticks every 0.4 s |
| Elements | 2 | me2 | Rime | Chill also reduces enemy attack 15% |
| Elements | 3 | me3 | Conduit | Shock jumps twice |
| Elements | 4 | me4 | Haemorrhage | Bleed stacks to 5 |
| Elements | 5 | me5 | Confluence | An enemy with two statuses takes +20% damage; three statuses +40% |
| Tempo | 1 | mt1 | Slow Read | Telegraphs +8% longer |
| Tempo | 2 | mt2 | Counter Status | Precise parries apply the weapon's status |
| Tempo | 3 | mt3 | Still Mind | Parry recovery 300 becomes 200 ms |
| Tempo | 4 | mt4 | Borrowed Time | A perfect parry slows all enemies 50% for 0.8 s |
| Tempo | 5 | mt5 | Eclipse | Execute applies every status the weapon can apply and resets the Special meter to 50 |

**Respec** is free three times, then 500 coins; class switch keeps each class's spent points.

## B3. Ring affixes, world materials, Forge recipes

**Ring affixes** (values at Fine quality; multiply by the quality tier in A3; a ring never carries the same affix twice; two rings may stack the same affix)

| Id | Affix | Fine value range | Cap across both rings |
| --- | --- | --- | --- |
| crit\_chance | Crit chance | +4% to +8% | +16% |
| crit\_damage | Crit damage | +0.15 to +0.30 multiplier | +0.6 |
| attack\_pct | Attack | +4% to +8% | +16% |
| health\_pct | Max health | +5% to +10% | +20% |
| defense\_flat | Defense | +2 to +4, scaled by the square root of M(w) at drop | none |
| riposte\_duration | Riposte window | +0.2 to +0.4 s | +0.8 s |
| special\_gain | Special charge | +10% to +20% | +40% |
| dodge\_cooldown | Dodge cooldown | −100 to −200 ms | −300 ms |
| parry\_window | Precise window | +10 to +20 ms | +30 ms |
| status\_duration | Status duration | +20% to +40% | +80% |
| coin\_find | Coins from stages | +5% to +15% | +30% |
| material\_find | Materials from dungeons and trials | +5% to +15% | +30% |
| potion\_power | Potion heal | +5% to +10% | +20% |
| break\_gain | Break from parries | +10% to +20% | +40% |
| move\_speed | Move speed | +3% to +6% | +12% |
| execute\_damage | Execute damage | +20% to +40% | +80% |

**Legendary named rules** (one per Legendary ring, fixed; six exist at launch)

| Id | Name | Rule | Drops from |
| --- | --- | --- | --- |
| lr\_mirror | Mirror | Reflected projectiles deal 3x weapon attack | World 7 boss first clear |
| lr\_pulse | Pulse | Every fifth precise parry casts a 1.0x Quake around you | World 6 boss first clear |
| lr\_anchor | Anchor | Immune to push from hazards | World 6 trial set complete |
| lr\_wick | Wick | Burn spreads to enemies within 1.5 units when its target dies | World 7 trial set complete |
| lr\_lull | Lull | Chilled enemies telegraph 25% longer | World 8 boss first clear |
| lr\_echoing | Echoing Steel | The riposte window does not end while you keep landing precise parries | World 8 trial set complete |

**World materials**

| World | Material | Used for |
| --- | --- | --- |
| 1 | Orchard Sap | Common tier upgrades and crafts |
| 2 | Salt Shard | Rare tier |
| 3 | Lantern Oil | Rare tier (second source) and Epic crafts' secondary cost |
| 4 | Cog Iron | Epic tier |
| 5 | Ember Glass | Epic tier |
| 6 | Rime Crystal | Epic tier and Legendary crafts' secondary cost |
| 7 | Sky Feather | Legendary tier |
| 8 | Crown Dust | Legendary tier |

An item's tier world is the world whose rarity it belongs to: Common items use world 1 material; Rare items use world 2 or 3; Epic items use world 4, 5 or 6; Legendary items use world 7 or 8. Upgrades accept any material of the tier's worlds.

**Forge recipes**

| Recipe | Cost | Result |
| --- | --- | --- |
| Craft weapon (unlocked family, current rarity) | 10 tier materials, 500 coins x rarity factor | Level 1 weapon, no roll |
| Craft armour (choose rule from the rarity's list) | 10 tier materials, 500 coins x rarity factor | Level 1 armour |
| Upgrade weapon or armour | A3 table | +1 level |
| Transmute | 10 materials of world w | 3 materials of world w+1 (never above world 8) |
| Re-roll ring affix | 3 shards | Chosen affix redrawn |
| Refine ring | 5 shards | Quality +1 tier, up to Shiny |
| Dismantle | the item | Shards 1, 2, 4 by rarity; weapons also return 30% of materials spent |
| Potion | 60 coins | 1 potion, up to the carry cap |
| Respec | free x3, then 500 coins | All points refunded for one class |

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

## B5. Worlds 2 to 8: the authoring matrix

Each world's 24 stages are authored from the same five-block pattern as world 1, with the block's family mix, rule strength and difficulty dials fixed here. A content designer fills a stage file by choosing spawn counts and timings that hit the dials; the bots confirm them. Dials are measured per stage: telegraph density (attacks requiring a response per 10 s), red share (fraction of attacks that are unparryable), simultaneous threats (peak attacks overlapping within 500 ms).

**Dial targets by world and block**

| World | Stages 1 to 4 | Stages 5 to 12 | Stages 13 to 20 | Stages 21 to 24 | Enemy cap |
| --- | --- | --- | --- | --- | --- |
| 2 | 4 / 0.10 / 1.2 | 5 / 0.15 / 1.4 | 6 / 0.15 / 1.6 | 6 / 0.20 / 1.6 | 5 |
| 3 | 5 / 0.10 / 1.4 | 6 / 0.15 / 1.6 | 7 / 0.20 / 1.8 | 7 / 0.20 / 1.8 | 5 |
| 4 | 5 / 0.25 / 1.4 | 6 / 0.30 / 1.6 | 7 / 0.30 / 2.0 | 7 / 0.30 / 2.0 | 6 |
| 5 | 6 / 0.20 / 1.6 | 7 / 0.25 / 1.8 | 8 / 0.25 / 2.0 | 8 / 0.30 / 2.2 | 6 |
| 6 | 6 / 0.20 / 1.8 | 7 / 0.25 / 2.0 | 8 / 0.30 / 2.2 | 8 / 0.30 / 2.2 | 6 |
| 7 | 7 / 0.20 / 1.8 | 8 / 0.25 / 2.0 | 9 / 0.30 / 2.4 | 9 / 0.30 / 2.4 | 6 |
| 8 | 7 / 0.30 / 2.0 | 8 / 0.30 / 2.2 | 9 / 0.35 / 2.5 | 9 / 0.35 / 2.5 | 6 |

Values are density / red share / simultaneous threats. World 1 for reference: 3 / 0.10 / 1.0 rising to 5 / 0.20 / 1.4. A stage may exceed its block's density by 1 only if it is stage 12 or 20.

**Family mix per world**

| World | New records (variants of the family in A4) | Earlier families used in stages 5 to 12 (one per stage, in this order) | Pairs used in stages 13 to 20 (two earlier families plus the new one) | Rule strength by block |
| --- | --- | --- | --- | --- |
| 2 Salt Flats | Shellback; Shellback Charger (shield plus a red charge, 900 ms, 2 units); Shellback Warden elite (shield re-closes after 2 s) | T, L, S, T, U, S, L, T | T+S, L+S, T+U, L+T, S+U, T+L, S+T, U+L | 1 to 4: tide band period 12 s, push 1.0 · 5 to 12: period 9 s, push 1.5 · 13 to 20: period 9 s, push 1.5, band 4 tall · 21 to 24: period 7 s |
| 3 Lantern Marsh | Wisp; Wisp Flicker (two blinks before striking); Wisp Lantern elite (blink leaves a Shock pool) | Shellback, T, S, Shellback, L, Charger, S, U | Shellback+S, T+L, Charger+S, Shellback+U, L+S, T+Shellback, Charger+L, S+U | pools: 2 per room · 4 · 6, placed near spawn edges · 6 with one at the centre |
| 4 Clockwork Quarry | Automaton; Automaton Piston (slam only, red, 800 ms); Automaton Foreman elite (jab, slam, and a 3-jab chain) | Wisp, Shellback, S, Wisp, Charger, T, Flicker, L | Wisp+Shellback, S+Charger, Wisp+S, Shellback+L, Flicker+S, T+Charger, Wisp+Charger, Flicker+Shellback | conveyor: one band 1.0 units/s · one band 1.2 · two bands opposing · two bands, reversal every 10 s |
| 5 Ember Vaults | Stoker; Stoker Bellows (buff hits two allies); Stoker Furnace elite (buff pulse also Burns the player within 2 units) | Automaton, Wisp, Shellback, Piston, S, Charger, Flicker, Archer-free: U | Automaton+Wisp, Piston+Shellback, Wisp+S, Automaton+Charger, Flicker+Piston, Shellback+S, Automaton+Shellback, Wisp+U | burn line every 10 s · every 8 s · every 8 s, two lines offset 4 s · every 7 s |
| 6 Frost Reliquary | Sentinel; Sentinel Twin (two rings, the second 0.6 s later); Sentinel Warden elite (rings leave Chill floor) | Stoker, Automaton, Wisp, Shellback, Piston, Bellows, Charger, Flicker | Stoker+Automaton, Wisp+Piston, Shellback+Stoker, Bellows+Automaton, Flicker+Charger, Stoker+Wisp, Piston+Bellows, Automaton+Charger | chill patches: 2 · 3 · 4 · 4 plus one under each spawn edge |
| 7 Sky Bastion | Archer; Archer Volleyer (5 arrows); Archer Captain elite (volleys alternate with a red dive) | Sentinel, Stoker, Automaton, Twin, Wisp, Bellows, Piston, Shellback | Sentinel+Stoker, Twin+Automaton, Wisp+Bellows, Sentinel+Piston, Stoker+Shellback, Twin+Wisp, Automaton+Bellows, Sentinel+Charger | wind band flips every 12 s · 10 s · 10 s, bend 40 degrees · 8 s |
| 8 The Undercrown | No new family; Crowned variants of each elite (health 1.2x, one extra trait) | Archer, Sentinel, Stoker, Automaton, Wisp, Shellback, Archer, Sentinel | Archer+Sentinel, Stoker+Automaton, Wisp+Shellback, Volleyer+Twin, Bellows+Piston, Flicker+Charger, Captain-free: Archer+Stoker, Sentinel+Automaton | rotating rule: one rule per room, announced; blocks 13 to 24 may run two rules in gauntlet rooms |

**Block rules shared by every world**

- Stages 1 to 4: stage 1 new family alone; stage 2 the rule alone with world 1 families; stage 3 both; stage 4 the new family's variant. Telegraphs on the new family are 15% longer in stage 1 and 2.
- Stages 5 to 12: one earlier family per stage as listed; stage 12 is the mini-boss: the world's elite with its listed trait plus adds every 12 s.
- Stages 13 to 20: pairs as listed; one elite appears in stages 15 and 18; stage 20 is five rooms with no boon after rooms 4 and 5 and an elite with Volatile or Vengeful in room 5.
- Stages 21 to 24: each stage rehearses one boss mechanic (B6 names them) using the record that shares the animation.
- Traits: Hasty from stage 9, Armoured on elites from stage 12, Volatile from stage 14, Linked from world 4 stage 13, Vengeful from world 5 stage 16. Never more than two traits on one record.
- Rest rooms: one in stages 4, 11, 16, 17 and 24 of every world (same positions as world 1), none in 20 or 25.
- Boon pools: 6 ids in stages 1 to 12, 8 ids from stage 13, drawn from the ids whose availability allows the world; each world's pool must include at least two status boons that match the world's new weapon trait.
- Side-dungeon stars: stage mastery stars in a world unlock that world's dungeons at 15, 35 and 55 stars (of 75).

**Expected first-clear minutes** by block (used in the section 9 budget and checked by the bots): stages 1 to 4 about 4.5, 5 to 12 about 5, 13 to 20 about 6, 21 to 24 about 6, boss 12 including retries.

## B6. Boss scripts (8)

Every boss follows the beat structure in design section 10 and the baselines in A4: health 18x the world's stage-25 Thornback, attack baseline P = 1.7 × A(w) × 12, break bar 100 that decays 6 per second, finisher at 15% health (the next break's Execute ends the fight with the cinematic). Attack power is given as a multiple of P; telegraphs in ms; phase thresholds are health percentages.

**Rootmaw, world 1** (break per parry 18; rehearsed in 1-21 to 1-24)

| Phase | Attack order (loops) | Attack | Colour, telegraph, power, shape |
| --- | --- | --- | --- |
| 1 (100 to 60%) | Sweep, Sweep, Slam | Sweep | white, 800, 1.0P, 150 degree arc reach 2.0 |
|  |  | Slam | red, 900, 1.3P, ground marker radius 1.6 |
| Break 1 | about 6 parries | Execute | opens phase 2 |
| 2 (60 to 15%) | Sweep, Volley, Slam, Burrow | Volley | 3 white seeds, 650, 0.5P each, 120 ms apart, reflectable |
|  |  | Burrow | yellow marker on the player 1,200, red emergence 1.2P radius 1.2; the boss is untargetable while burrowed (1.5 s) |
| Break 2 | about 6 parries | Execute | at or under 15%: finisher |

**Saltcrown, world 2** (break per parry 18; shield mechanic)

| Phase | Behaviour | Attacks |
| --- | --- | --- |
| 1 (100 to 60%) | Shield up: frontal damage 0 until 4 precise parries open it for 6 s | Jab (white, 700, 1.0P); Charge (red, 900, 1.3P, crosses the arena vertically, 2 units wide) |
| Break 1 | Parries made while standing in a tide band count double | Execute |
| 2 (60 to 15%) | Shield re-closes every 10 s; Tide Call every 15 s sets the tide period to 5 s for 8 s | adds Shell Slam (red, 800, 1.2P, radius 1.8, fires when the shield closes) |
| Break 2 |  | Execute, finisher at 15% |

**The Lanternkeeper, world 3** (break per parry 20; split mechanic)

| Phase | Behaviour | Attacks |
| --- | --- | --- |
| 1 (100 to 60%) | Blink twice (blue, 600 each) then Strike | Strike (white, 500, 1.1P); Lantern Toss (yellow ring 1,200, 0.9P, leaves a Shock pool for 8 s) |
| Break 1 | After Execute the boss splits into 3 Wisps (0.15x boss health each, white Strike only); killing 2 re-forms the boss at phase 2 |  |
| 2 (60 to 15%) | Blink three times; pools chain: standing in any pool when any enemy is hit Shocks the player for 0.3P | adds Lantern Sweep (white, 650, 1.0P, 180 degrees) |
| Break 2 | Split again; re-form at the finisher threshold if under 15% | Execute, finisher |

**The Foreman, world 4** (break per parry 18, the third jab in a chain gives 30)

| Phase | Behaviour | Attacks |
| --- | --- | --- |
| 1 (100 to 60%) | Jab chain of three (white 700, 600, 500; 0.8P, 0.9P, 1.0P) then Piston Slam | Piston Slam (red, 900, 1.4P, radius 2.0) |
| Break 1 | Both conveyor bands reverse after Execute |  |
| 2 (60 to 15%) | Double Slam: two markers 1.0 s apart; jab chain becomes four | adds Steam Vent (yellow line across the arena, 1,000, 0.6P, parryable white edge) |
| Break 2 | Conveyors stop for 6 s | Execute, finisher |

**The Furnace, world 5** (break per parry 22; kill-order mechanic)

| Phase | Behaviour | Attacks |
| --- | --- | --- |
| 1 (100 to 60%) | Summons 2 Stokers at the top edge every 20 s; while any Stoker's buff is on the boss, parries build 0 break | Bolt Fan (5 whites, 650, 0.4P each, 15 degrees apart, reflectable); Flame Line (burn line every 6 s) |
| Break 1 | Execute also kills all live Stokers |  |
| 2 (60 to 15%) | Summons 3 Stokers (one Bellows); Furnace Pulse: blue 1,000 then a red ring radius 2.5, 1.2P | adds Ember Slam (red, 850, 1.3P, radius 1.6) |
| Break 2 |  | Execute, finisher |

**The Reliquary Warden, world 6** (break per parry 20; three phases)

| Phase | Behaviour | Attacks |
| --- | --- | --- |
| 1 (100 to 60%) | Ring Lattice: three rings 0.4 s apart (yellow, 1,200, 0.8P each, white edges parryable: a precise parry on an edge clears that ring) | Frost Slam (red, 900, 1.3P, radius 1.8, leaves chill floor radius 2 for 10 s) |
| Break 1 | Chill floor cleared | Execute |
| 2 (60 to 25%) | Lattice of four rings; chill patches spawn under each slam | adds Shard Volley (3 whites, 600, 0.5P, reflectable) |
| Break 2 |  | Execute |
| 3 (25 to 15%) | Rings overlap on purpose; a parried edge clears all overlapping rings | Pattern order random from a set of 3 |
| Break 3 |  | Execute, finisher |

**The Bastion Captain, world 7** (break per parry 20; reflection phase)

| Phase | Behaviour | Attacks |
| --- | --- | --- |
| 1 (100 to 60%) | Alternates Volley and Dive | Volley (5 whites, 650, 0.45P each, bends in wind bands, reflectable); Dive (red, 900, 1.4P, line 1.5 wide) |
| Break 1 | Wind flips | Execute |
| 2 (60 to 25%) | Rampart: the boss is immune to non-reflected damage for 10 s every 25 s; reflected arrows deal 3x weapon attack | adds Arrow Rain (yellow ring radius 2.5 with a white edge, 1,100, 0.9P) |
| Break 2 |  | Execute |
| 3 (25 to 15%) | Volleys of 7; Dive from both edges in sequence | random order from a set of 3 |
| Break 3 |  | Execute, finisher |

**The Undercrown, world 8** (break per parry 22; six breaks)

| Phase | Rule active | Attack set | Breaks |
| --- | --- | --- | --- |
| 1 (100 to 65%) | tide band | Rootmaw's Sweep and Slam at 1.2P, Saltcrown's shield (3 parries to open) | 2 |
| 2 (65 to 30%) | conveyor | Lanternkeeper's double blink Strike, the Foreman's four-jab chain, Furnace Bolt Fan | 2 |
| 3 (30 to 15%) | wind band | Reliquary Lattice (four rings), Captain's Volley of 7 and Dive; order random from a set of 4 | 2, the last is the finisher |

All eight bosses: intro 1.5 s with the camera pull-out; arena 9 by 16, boss anchored in the top half; no adds beyond those listed; the boss never attacks during the player's Execute; after the fight, a 4 s victory beat before the Results screen.

## B7. Side dungeons (21) and trials (30)

Side dungeons remix a world's rule across three stages and end on an elite pair; trials are fixed-loadout or modifier fights with one room each. Both restart from the stage start on death (design section 4) and pay the XP multiples in A1.

**Side dungeons** (three per world, worlds 2 to 8; unlock at 15, 35 and 55 mastery stars in that world; each stage 3 rooms, the third stage's last room is the elite pair)

| Id | World | Name | Remix | Stage 1 / 2 / 3 | Elite pair | First-clear reward |
| --- | --- | --- | --- | --- | --- | --- |
| w2-d1 | 2 | Shallows | Every enemy is a Shellback; boons are parry-only | 3 Shellbacks / Chargers join / tide period 6 s | Warden + Charger (Linked) | Rare ring |
| w2-d2 | 2 | Undertow | Tide band always on, 2.0 push | mixed W1 and W2 / bottom spawns only / both edges | Warden (Armoured) + Brute | Rare ring, 5 shards |
| w2-d3 | 2 | Brine Court | No potions; rest rooms give Second Wind instead | W1 families at W2 scale / Shellbacks / gauntlet 4 waves | Warden + Warden (Linked) | Epic ring (quality Fine or better) |
| w3-d1 | 3 | Marshlight | Wisps only; pools under every spawn | 3 Wisps / Flickers / Lantern elite early | Lantern + Flicker (Hasty) | Rare ring |
| w3-d2 | 3 | Still Water | Pools cover 50% of the arena; Chill floor absent | Shellbacks in pools / Wisps / mixed | Lantern + Warden | Rare ring, 5 shards |
| w3-d3 | 3 | Lantern Walk | Dodge disabled; parry only (Soft Steel always on) | Seedspitters / Wisps / Flickers | Lantern + Lantern (Linked) | Epic ring |
| w4-d1 | 4 | Gear Pit | Three conveyors | Automata / Pistons / Foreman early | Foreman + Piston (Armoured) | Rare ring |
| w4-d2 | 4 | Press Line | Conveyors reverse every 5 s | Shellbacks on conveyors / Wisps / mixed | Foreman + Lantern | Rare ring, 5 shards |
| w4-d3 | 4 | Scrapyard | Every enemy Volatile | Thornbacks / Automata / gauntlet | Foreman + Foreman (Linked) | Epic ring |
| w5-d1 | 5 | Stokehold | Stokers buff every 3 s | Stokers + Thornbacks / Bellows / Furnace elite | Furnace + Bellows | Rare ring |
| w5-d2 | 5 | Cinder Run | Burn lines every 4 s, no rest rooms | Automata / Wisps / mixed | Furnace + Foreman | Rare ring, 5 shards |
| w5-d3 | 5 | Kiln | Vengeful on everything | Shellbacks / Stokers / gauntlet | Furnace + Furnace (Linked) | Epic ring |
| w6-d1 | 6 | Rime Hall | Chill floor everywhere | Sentinels / Twins / Warden elite early | Sentinel Warden + Twin | Rare ring |
| w6-d2 | 6 | Lattice | Rings overlap by design | Sentinels + Stokers / Twins / mixed | Sentinel Warden + Furnace | Rare ring, 5 shards |
| w6-d3 | 6 | Reliquary Vault | Special disabled | Automata / Sentinels / gauntlet | Sentinel Warden x2 (Linked) | Epic ring |
| w7-d1 | 7 | Rampart | Archers only; wind flips every 5 s | Archers / Volleyers / Captain early | Captain + Volleyer | Rare ring |
| w7-d2 | 7 | Gale Stair | Reflection deals 2x; melee deals 0.5x | mixed / Sentinels + Archers / Volleyers | Captain + Sentinel Warden | Rare ring, 5 shards |
| w7-d3 | 7 | Eyrie | Enemy cap 8; Hasty on everything | Wisps + Archers / Stokers + Archers / gauntlet | Captain x2 (Linked) | Epic ring |
| w8-d1 | 8 | Crown Steps | Rule changes every 30 s | all families / elites mixed / gauntlet | Crowned Foreman + Crowned Captain | Epic ring |
| w8-d2 | 8 | Deep Court | Two rules at once | all families / all elites / gauntlet | Crowned Lantern + Crowned Furnace | Epic ring, 10 shards |
| w8-d3 | 8 | The Throne Road | No boons; every room an elite | 3 elites / 3 Crowned elites / final pair | Crowned Sentinel Warden + Crowned Captain | Legendary ring (random named rule) |

**Trials** (six per world, worlds 4 to 8; unlocked by clearing that world's boss; one room each, fixed by the type; completing all six in a world is a "trial set")

| Type | Rule | World twist (4 / 5 / 6 / 7 / 8) | Target to pass |
| --- | --- | --- | --- |
| Boss rush | The world's boss at 60% health, then the previous world's boss at 60% | Foreman then Lanternkeeper / Furnace then Foreman / Warden then Furnace / Captain then Warden / Undercrown phases 1 and 2 only | clear |
| No damage | Any damage fails the trial; 3 rooms of the world's stage 15 | same spawns as stage 15 | clear |
| Silent Special | Special disabled; meter shows locked | elite with Armoured at room end | clear |
| Parry only | Dodge disabled; red attacks are replaced by white versions at 1.5P | the world's elite plus two adds | clear |
| Speed clear | Clear stage 10's spawns under a time limit | 2:30 / 2:30 / 2:45 / 2:45 / 3:00 | under the limit |
| Mirror | Telegraph colours swapped (white becomes red and the reverse); shapes and sounds unchanged | stage 8 spawns | clear |

Trial rewards: 8 materials of the world each, plus per set: world 4 Epic armour (Quickstep), world 5 Epic weapon of choice, world 6 Anchor ring, world 7 Wick ring, world 8 Echoing Steel ring and the title Trialborne. Trials pay no XP after the first clear and cannot be used with assist options (the assist toggle is greyed with the line "Trials run without assists").

## B8. Engagement content

**Daily quest pool** (three drawn per day, never two of the same group; progress counts in any mode; reward = one stage's coins at the player's current world, plus the listed extra)

| Id | Group | Objective | Extra |
| --- | --- | --- | --- |
| dq\_parry\_20 | parry | Land 20 precise parries | 3 materials |
| dq\_perfect\_5 | parry | Land 5 perfect parries | 3 materials |
| dq\_reflect\_6 | parry | Reflect 6 projectiles | 3 materials |
| dq\_soft\_0 | parry | Clear a stage with no soft parries | 1 shard |
| dq\_dodge\_10 | dodge | Dodge through 10 red attacks | 3 materials |
| dq\_nodamage\_room | dodge | Clear 3 rooms without taking damage | 1 shard |
| dq\_special\_4 | special | Cast the Special 4 times | 3 materials |
| dq\_execute\_2 | special | Execute 2 enemies | 3 materials |
| dq\_weapon\_spear | loadout | Win a stage with a Spear | 2 materials |
| dq\_weapon\_hammer | loadout | Win a stage with a Hammer | 2 materials |
| dq\_weapon\_chakram | loadout | Win a stage with a Chakram | 2 materials |
| dq\_weapon\_wand | loadout | Win a stage with a Wand | 2 materials |
| dq\_class\_other | loadout | Win a stage with a class you did not use yesterday | 1 shard |
| dq\_stage\_any | progress | Clear any campaign stage | 1 potion |
| dq\_stage\_new | progress | Clear a stage for the first time | 2 materials |
| dq\_star\_2 | progress | Earn 2 mastery stars | 1 shard |
| dq\_dungeon | progress | Clear a side dungeon stage | 3 materials |
| dq\_nopotion | challenge | Clear a stage without drinking | 1 shard |
| dq\_boon\_rule | challenge | Win a stage having picked only rule boons | 2 materials |
| dq\_time | challenge | Clear a stage under its mastery time | 2 materials |

Loadout quests only draw from families the player has unlocked; a quest the player cannot progress (for example dq\_dungeon before world 2) is never drawn.

**Weekly quest pool** (three per week; reward 5x a stage's coins plus the extra)

| Id | Objective | Extra |
| --- | --- | --- |
| wq\_stars\_6 | Earn 6 mastery stars | 20 gems |
| wq\_dungeon\_clear | Clear a side dungeon | 10 shards |
| wq\_refight | Win a boss re-fight | 20 gems |
| wq\_trial | Clear a trial | 15 gems, 5 shards |
| wq\_parry\_150 | Land 150 precise parries | 15 gems |
| wq\_families\_3 | Win stages with 3 different weapon families | 15 gems |
| wq\_challenge | Clear the weekly challenge stage | 25 gems |
| wq\_nodamage\_boss | Beat any boss re-fight without taking damage | 30 gems |
| wq\_stages\_12 | Clear 12 stages (any mode) | 10 shards |
| wq\_execute\_10 | Execute 10 enemies | 15 gems |

**Seven-day calendar** (values scale by the player's highest world w; the day-6 frame and day-7 ring are fixed)

| Day | Reward |
| --- | --- |
| 1 | Coins: 2 × StageCoins(w, 12) |
| 2 | 2 potions |
| 3 | Materials: 6 of world w |
| 4 | 3 shards |
| 5 | Coins: 3 × StageCoins(w, 12) |
| 6 | Cosmetic frame from the calendar set (12 frames, one per cycle, then gems 20) |
| 7 | 30 gems and a Rare ring (Epic from world 5; quality Plain to Shiny) |

Streak milestones: day 7 title Regular, day 14 60 gems, day 30 150 gems and the title Devoted, day 60 a cosmetic parry effect. One missed day per calendar week is forgiven; a second miss resets the streak count to 0 but not the calendar day index.

**Season track** (30 tiers; season points from season quests: campaign 100 per stage first clear, mastery 60 per star, challenge 300 per weekly challenge clear; 60,000 points to tier 30; free track shown, premium adds the cosmetics column)

| Tier | Points | Free | Premium adds |
| --- | --- | --- | --- |
| 1 | 1,000 | 2 potions | seasonal frame |
| 2 | 2,500 | 6 materials |  |
| 3 | 4,000 | 3 shards | parry effect colour |
| 4 | 5,500 | 20 gems |  |
| 5 | 7,000 | Rare ring | title |
| 6 to 9 | 8,500 to 13,000 | alternating 6 materials, 3 shards, coins, 2 potions | tier 8 weapon skin part 1 |
| 10 | 15,000 | 40 gems | Execute cinematic |
| 11 to 14 | 17,000 to 23,000 | alternating as above | tier 12 weapon skin part 2 |
| 15 | 25,000 | Epic ring | seasonal armour skin |
| 16 to 19 | 27,500 to 35,000 | alternating as above |  |
| 20 | 37,500 | 60 gems | title |
| 21 to 24 | 40,000 to 49,000 | alternating as above | tier 24 weapon skin part 3 (complete) |
| 25 | 52,000 | 10 shards |  |
| 26 to 29 | 54,000 to 58,000 | alternating as above |  |
| 30 | 60,000 | 100 gems and the season's Legendary ring (one of the six named rules, rotating) | seasonal Execute cinematic and the season title |

Premium refunds 60% of the pass price in gems across tiers 5, 10, 15, 20 (section 12). The Legendary ring at tier 30 is on the free track on purpose: power is never behind the pass.

**Achievements (80; gems in brackets)**

| Group | Achievements |
| --- | --- |
| Progression (16) | Clear world 1 to 8 (20 each: ach\_w1 to ach\_w8); beat each boss without a potion (15 each: ach\_b1np to ach\_b8np) |
| Mastery (24) | 25, 50, 75 stars in each of worlds 1 to 8 (10, 15, 25) |
| Parry (12) | 100, 1,000, 10,000 precise parries (10, 25, 50); 50, 500 perfect parries (15, 40); 100, 1,000 reflections (10, 30); parry chain of 10, 25, 50 (10, 20, 40); clear a boss with only precise parries (50); 1,000 soft parries (10, named Close Enough) |
| Dodge (6) | 100, 1,000 dodges through reds (10, 25); 100 Dash Strikes (15); a stage with 0 damage in world 4+ (20); a boss with 0 damage (50); Afterimage cancel 50 windups (20) |
| Combat (10) | 100, 1,000 Executes (10, 30); 50 breaks on elites (15); kill 3 enemies with one Special (15); 10,000 enemies (30); 100 kills with each status (4 × 10); Execute heal 1,000 total (10) |
| Collection (8) | Unlock all 5 families (20); all 3 classes (20); a Legendary of each slot (30); all six named rings (60); all 40 boons picked at least once (25); 10 cosmetics (10); all calendar frames (30); level 60 (50) |
| Style (4) | Win a boss using only soft parries (60, named Grace Under Pressure); clear a world 6+ stage with the Wand and no Special (30); clear 1-20 with a Hammer under 5:00 (25); clear a mirror trial first try (40) |

Achievement ids follow `ach_<group>_<slug>`; each is claimed from the Quests tab and shows a one-line hint for progress-type achievements ("312 of 1,000 reflections").

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
