<!-- from md/03-build-spec-B-content-tables.md -->

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
