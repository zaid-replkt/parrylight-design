<!-- from md/02-build-spec-A-formulas-and-systems.md -->

## A4. Enemy numbers

Every enemy is a family base record scaled by a world multiplier, so authoring a world 5 Thornback is a lookup, not a balancing job. Base values are world 1; the multipliers are derived from the player's expected attack and health at each world's entry level (A1, A3) so that a normal enemy dies in about 3.5 s of auto-attack and an unparried normal hit costs about 12% of health.

**Family base records** (world 1, stage 1)

| Family | Health | Defense | Attack power | Move speed (units/s) | Telegraph (ms) | Attack cooldown (s) | Reach (units) | Attacks |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Thornback | 126 | 0 | 12 | 2.5 | 800 | 2.2 | 1.2 | Swing (white) |
| Shellback | 115 | 2 | 12 | 2.0 | 700 | 2.0 | 1.2 | Jab (white); front shield absorbs all damage until parried, open 3 s |
| Wisp | 76 | 0 | 10 | 3.5 | blink 600 then strike 500 | 2.6 | 1.0 | Blink (blue marker) then Strike (white) |
| Automaton | 176 | 3 | jab 10, slam 22 | 1.8 | jab 700, slam 900 | 2.4 | 1.4 / slam radius 1.6 | Jab (white), Slam (red, ground marker) alternating |
| Stoker | 88 | 0 | bolt 8 | 2.2 | bolt 650, buff pulse 1000 | 3.0 | 5.0 | Bolt (white projectile); Buff: nearest ally +25% attack for 6 s, every 6 s |
| Sentinel | 139 | 2 | ring 18 | 1.6 | ring fill 1200 | 3.2 | ring radius 1.8 at 3 units | Delayed ring (yellow; white edge = parryable edge) |
| Archer | 63 | 0 | arrow 7 x 3 | 2.0 | 650 per arrow, 120 ms apart | 2.8 | 7.0 | Volley (white projectiles, reflectable) |

**World scaling**

```latex
\mathrm{Health}(w,s) = \mathrm{Base} \cdot M(w) \cdot (1 + 0.012\,(s-1)), \quad \mathrm{Attack}(w) = \mathrm{Base} \cdot A(w), \quad \mathrm{Defense}(w) = \mathrm{round}(\mathrm{Base} \cdot (1 + 0.35\,(w-1)))
```

| World | M(w) health | A(w) attack | Thornback health at stage 1 | Normal hit vs entry-level health |
| --- | --- | --- | --- | --- |
| 1 | 1.00 | 1.00 | 126 | 12 of 100 |
| 2 | 2.25 | 1.92 | 284 | 23 of 191 |
| 3 | 3.16 | 3.00 | 398 | 36 of 297 |
| 4 | 5.06 | 4.17 | 638 | 50 of 418 |
| 5 | 6.44 | 5.75 | 812 | 69 of 574 |
| 6 | 7.97 | 7.50 | 1004 | 90 of 749 |
| 7 | 11.05 | 9.42 | 1392 | 113 of 944 |
| 8 | 13.66 | 11.58 | 1721 | 139 of 1157 |

Telegraph times shorten by world, floored: telegraph(w) = max(450, base × (1 − 0.04 (w − 1))). Boss fast attacks are authored directly in their scripts (B6).

**Elite multipliers.** Health 4.0x, attack 1.4x, defense +2, size 1.6x, break bar 100 (A2), one or two traits. Elites are immune to stagger from soft parries and to knockback.

**Boss baselines** (each script in B6 overrides)

| Field | Value |
| --- | --- |
| Health | 18 × Thornback health of the world at stage 25 |
| Attack power | 1.7 × A(w) × 12 (about 20% of entry-level health per hit) |
| Defense | 2 × world defense of a Shellback |
| Break bar | 100, decays 6 per second when not parried, per-parry gain in the script (18 to 25) |
| Stagger | Never; parries build break instead |
| Phase thresholds | Health 100 to 60% phase 1, 60 to 25% phase 2, under 25% phase 3 (worlds 6 to 8 only) |

**Traits as numbers**

| Trait | Effect |
| --- | --- |
| Hasty | Telegraphs 0.85x, move speed 1.15x |
| Armoured | Health 1.3x; only the first precise parry per room staggers it (later parries still riposte and build break) |
| Volatile | On death, a yellow ring of radius 1.5 fills over 0.8 s and deals 1.5x the family attack |
| Linked | Takes 50% of the damage dealt to its Linked partner; both show a tether |
| Vengeful | On death, allies within 3 units gain +25% attack for 6 s (blue flash) |

**Hazards (arena rules) as numbers**

| Rule | Effect | Timing |
| --- | --- | --- |
| Tide band (W2) | Horizontal push 1.5 units/s on the character and enemies inside the band | Band 3 units tall, sweeps top to bottom over 9 s, 2 s warning shimmer |
| Shock pool (W3) | 8% of max health per 0.5 s while standing in it; enemies in a pool are Shocked when hit | Pools are static, 1.5 units across, shown with a rim |
| Conveyor (W4) | Moves anything on it 1.2 units/s in the arrow direction | Reverses every 12 s with a 1 s warning |
| Burn line (W5) | 10% of max health on contact, then 0.5 s immunity | Crosses the arena horizontally over 2 s, every 8 s, 1.5 s warning |
| Chill floor (W6) | Move speed 0.8x, dodge cooldown 1.5x while on it | Static patches, 2 units across |
| Wind band (W7) | Projectiles crossing it bend 30 degrees toward the band's direction | Direction flips every 10 s with a 1 s warning |
| Rotating rules (W8) | One of the above active at a time | Switches every room, announced at room start |

Hazards never deal more than 10% of max health per second in total, and no hazard damages during hit stop or inside a dodge.
