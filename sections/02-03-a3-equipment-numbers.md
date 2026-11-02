<!-- from md/02-build-spec-A-formulas-and-systems.md -->

## A3. Equipment numbers

Weapon attack is set by rarity and level, families trade attack for cadence so their auto-attack DPS sits within 25% of each other (the ranged families are lower on purpose), and upgrade costs are cheap in coins and gated by world materials.

**Weapon attack**

```latex
\mathrm{WeaponAttack} = \mathrm{RarityBase} \cdot f_{family} \cdot (1 + 0.09\,(n-1)), \quad n = \text{weapon level } 1..8
```

RarityBase: Common 8, Rare 18, Epic 40, Legendary 80. Family factor and cadence:

| Family | f\_family | Cadence (attacks/s) | Range (units) | Hit shape | Common L1 / L8 | Rare L1 / L8 | Epic L1 / L8 | Legendary L1 / L8 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Blade | 1.0 | 2.0 | 1.4 | 90 degree arc, 1 target plus 50% to a second | 8.0 / 13.0 | 18.0 / 29.3 | 40.0 / 65.2 | 80.0 / 130.4 |
| Spear | 1.25 | 1.6 | 2.6 | Line 0.6 wide, all targets | 10.0 / 16.3 | 22.5 / 36.7 | 50.0 / 81.5 | 100.0 / 163.0 |
| Chakram | 0.9 | 1.8 | 5.0 | Projectile out and back, hits on both passes | 7.2 / 11.7 | 16.2 / 26.4 | 36.0 / 58.7 | 72.0 / 117.4 |
| Hammer | 2.0 | 1.0 | 1.6 | 150 degree arc, all targets | 16.0 / 26.1 | 36.0 / 58.7 | 80.0 / 130.4 | 160.0 / 260.8 |
| Wand | 0.6 | 2.6 | 6.0 | Homing bolt, 1 target | 4.8 / 7.8 | 10.8 / 17.6 | 24.0 / 39.1 | 48.0 / 78.2 |

**Weapon trait (unlocked at level 3)** and **Special** (upgraded at level 6)

| Family | Trait at level 3 | Special (meter 100) | Special at level 6 |
| --- | --- | --- | --- |
| Blade | Riposte hits apply Bleed | Crescent: 180 degree arc, 3.0x attack, 0.4 s | 4.0x and applies 2 Bleed stacks |
| Spear | Every third consecutive hit on one target applies Shock | Thrust: 6-unit line, 2.5x to all, knockback 2 units | 3.5x and Shock on all hit |
| Chakram | Return-pass hits apply Chill | Orbit: 3 chakrams orbit 2.5 units for 4 s, 0.8x per hit, 2 hits/s each | 6 s and 1.0x |
| Hammer | +30% damage to broken enemies | Quake: radius 3, 2.5x, +40 break (boss: 3x its per-parry break) | Radius 4, 3.5x |
| Wand | Every fourth bolt applies Burn | Nova: 8 bolts outward, 1.2x each, Burn | 12 bolts |

**Upgrade costs** (to reach level n; coins times a rarity factor of Common 1, Rare 2, Epic 4, Legendary 8; materials are the item's tier-world materials)

| Level n | 2 | 3 | 4 | 5 | 6 | 7 | 8 | Total to 7 | Total to 8 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Coins (Common) | 57 | 104 | 160 | 224 | 294 | 370 | 453 | 1209 | 1662 |
| Materials | 2 | 4 | 6 | 8 | 10 | 12 | 14 | 42 | 56 |

Material drops: 3 per campaign stage, 12 per boss (84 per world), 5 per side-dungeon stage, 8 per trial. So the campaign path funds weapon and armour to level 7 (84 materials) and side dungeons fund level 8, which is the design target in section 12. Coins are tight only in world 1 (about 2,060 from the campaign against 1,209 for the weapon and 846 for armour), by design.

**Forge crafting.** A weapon of the current world's rarity in any unlocked family: 10 materials and 500 coins times the rarity factor. Armour: same. Unlock order of families: Blade (start), Hammer (clear 1-8), Spear (clear world 1), Chakram (clear world 2), Wand (clear world 3).

**Armour** (one slot; adds health and defense, plus one rule from level 5)

| Rarity | Health bonus L1 / L8 | Defense L1 / L8 | Rules available (one per item, fixed at craft) |
| --- | --- | --- | --- |
| Common | 20 / 33 | 2 / 3 | Bulwark: the first hit taken in each room is halved |
| Rare | 45 / 73 | 4 / 7 | Bulwark; Quickstep: dodge cooldown 800 becomes 600 ms |
| Epic | 100 / 163 | 8 / 13 | Bulwark; Quickstep; Second Wind: once per stage at 20% health, heal 25% |
| Legendary | 200 / 326 | 14 / 23 | All above; Stonecoat: a soft parry also staggers for 0.4 s |

Health bonus and defense scale by (1 + 0.09(n − 1)). Defense is capped in the damage formula (A2) so it can never remove more than 40% of a hit.

**Rings** (two slots; affixes in B3)

| Rarity | Affixes | Quality tiers (value multiplier) | Source |
| --- | --- | --- | --- |
| Rare | 2 | Dull 0.6, Plain 0.8, Fine 1.0, Shiny 1.2, Heirloom 1.5 | Side dungeons, calendar day 7, return rewards |
| Epic | 3 | Same | Side dungeon finales, trials |
| Legendary | 3 plus one named rule | Same | Boss first clears in worlds 6 to 8, trial sets |

Re-roll: 3 shards re-draws one chosen affix (type and value) from the ring's rarity pool; quality tier is fixed at drop. Refine: 5 shards raise quality one tier, up to Shiny; Heirloom only drops. Dismantle yields 1 shard (Rare), 2 (Epic), 4 (Legendary).

**Potions.** Heal 35% of max health over 0.6 s (interrupted by a dodge, which keeps the potion). Cost 60 coins at the Forge. Carry cap 3 per stage; rest rooms hold one free potion.
