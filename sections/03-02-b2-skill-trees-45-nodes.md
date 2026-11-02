<!-- from md/03-build-spec-B-content-tables.md -->

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
