<!-- from md/03-build-spec-B-content-tables.md -->

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
