# Build spec A: formulas and systems

Everything an engineer needs to implement the systems in the design tab without inventing a number. Values here are the initial tuning; remote-config keys (A7) override them live.

## A1. Character stats, level curve and XP curve

Health and attack grow on a gentle quadratic so levels 1 to 60 feel steady, and the XP curve is set so that the campaign's stage XP alone lands the player on the entry levels in design section 8 (1, 8, 15, 22, 30, 38, 46, 54). Total XP from level 1 to 60 is 948,200.

**Formulas** (L = level, 1 to 60)

```latex
\mathrm{MaxHealth}(L) = 100 + 12(L-1) + 0.15(L-1)^2
```

```latex
\mathrm{BaseAttack}(L) = 10 + 1.2(L-1) + 0.02(L-1)^2
```

```latex
\mathrm{XPtoNext}(L) = \mathrm{round}(60 \cdot L^{1.6})
```

Other base values at every level: Defense 0 (armour supplies it), move speed 4.5 units per second, dodge charges 1 (2 after the world 3 unlock), potion cap 3 per stage, Special meter 100 points (150 for Mystic).

**Skill points.** One point at every even level: 30 points by level 60. A full class tree is 15 nodes, so two full trees fit by 60 and the third is partial.

**Level table**

| Level | Max health | Base attack | XP to next level | Cumulative XP |
| --- | --- | --- | --- | --- |
| 1 | 100 | 10.0 | 60 | 0 |
| 2 | 112 | 11.2 | 182 | 60 |
| 3 | 125 | 12.5 | 348 | 242 |
| 4 | 137 | 13.8 | 551 | 590 |
| 5 | 150 | 15.1 | 788 | 1141 |
| 6 | 164 | 16.5 | 1055 | 1929 |
| 7 | 177 | 17.9 | 1350 | 2984 |
| 8 | 191 | 19.4 | 1671 | 4334 |
| 9 | 206 | 20.9 | 2018 | 6005 |
| 10 | 220 | 22.4 | 2389 | 8023 |
| 11 | 235 | 24.0 | 2782 | 10412 |
| 12 | 250 | 25.6 | 3198 | 13194 |
| 13 | 266 | 27.3 | 3635 | 16392 |
| 14 | 281 | 29.0 | 4092 | 20027 |
| 15 | 297 | 30.7 | 4570 | 24119 |
| 16 | 314 | 32.5 | 5067 | 28689 |
| 17 | 330 | 34.3 | 5583 | 33756 |
| 18 | 347 | 36.2 | 6118 | 39339 |
| 19 | 365 | 38.1 | 6670 | 45457 |
| 20 | 382 | 40.0 | 7241 | 52127 |
| 21 | 400 | 42.0 | 7829 | 59368 |
| 22 | 418 | 44.0 | 8434 | 67197 |
| 23 | 437 | 46.1 | 9056 | 75631 |
| 24 | 455 | 48.2 | 9694 | 84687 |
| 25 | 474 | 50.3 | 10348 | 94381 |
| 26 | 494 | 52.5 | 11018 | 104729 |
| 27 | 513 | 54.7 | 11704 | 115747 |
| 28 | 533 | 57.0 | 12405 | 127451 |
| 29 | 554 | 59.3 | 13122 | 139856 |
| 30 | 574 | 61.6 | 13853 | 152978 |
| 31 | 595 | 64.0 | 14599 | 166831 |
| 32 | 616 | 66.4 | 15360 | 181430 |
| 33 | 638 | 68.9 | 16135 | 196790 |
| 34 | 659 | 71.4 | 16925 | 212925 |
| 35 | 681 | 73.9 | 17728 | 229850 |
| 36 | 704 | 76.5 | 18545 | 247578 |
| 37 | 726 | 79.1 | 19376 | 266123 |
| 38 | 749 | 81.8 | 20221 | 285499 |
| 39 | 773 | 84.5 | 21079 | 305720 |
| 40 | 796 | 87.2 | 21951 | 326799 |
| 41 | 820 | 90.0 | 22835 | 348750 |
| 42 | 844 | 92.8 | 23733 | 371585 |
| 43 | 869 | 95.7 | 24643 | 395318 |
| 44 | 893 | 98.6 | 25567 | 419961 |
| 45 | 918 | 101.5 | 26503 | 445528 |
| 46 | 944 | 104.5 | 27451 | 472031 |
| 47 | 969 | 107.5 | 28412 | 499482 |
| 48 | 995 | 110.6 | 29386 | 527894 |
| 49 | 1022 | 113.7 | 30371 | 557280 |
| 50 | 1048 | 116.8 | 31369 | 587651 |
| 51 | 1075 | 120.0 | 32379 | 619020 |
| 52 | 1102 | 123.2 | 33401 | 651399 |
| 53 | 1130 | 126.5 | 34434 | 684800 |
| 54 | 1157 | 129.8 | 35480 | 719234 |
| 55 | 1185 | 133.1 | 36537 | 754714 |
| 56 | 1214 | 136.5 | 37606 | 791251 |
| 57 | 1242 | 139.9 | 38686 | 828857 |
| 58 | 1271 | 143.4 | 39777 | 867543 |
| 59 | 1301 | 146.9 | 40880 | 907320 |
| 60 | 1330 | 150.4 | max | 948200 |

**Stage XP.** Each world has a base value B(w) chosen so that 24 stages plus the boss sum to the XP between that world's entry level and the next:

```latex
\mathrm{StageXP}(w, s) = \mathrm{round}\big(B(w) \cdot (0.8 + 0.4 \cdot s / 25)\big), \quad \mathrm{BossXP}(w) = 3 \cdot \mathrm{StageXP}(w, 25)
```

| World | Entry level | XP needed to next entry level | B(w) | Stage 1 / stage 24 / boss XP |
| --- | --- | --- | --- | --- |
| 1 | 1 | 4334 | 157 | 128 / 186 / 565 |
| 2 | 8 | 19785 | 717 | 585 / 849 / 2581 |
| 3 | 15 | 43078 | 1561 | 1274 / 1848 / 5619 |
| 4 | 22 | 85781 | 3108 | 2536 / 3680 / 11189 |
| 5 | 30 | 132521 | 4801 | 3918 / 5685 / 17285 |
| 6 | 38 | 186532 | 6758 | 5515 / 8002 / 24330 |
| 7 | 46 | 247203 | 8957 | 7309 / 10605 / 32244 |
| 8 | 54 | 228966 | 8296 | 6769 / 9822 / 29865 |

Other XP sources, all multiples of the world's average stage XP (B(w) × 1.0): side dungeon stage 1.2x, trial 1.5x, each mastery objective 0.3x on first completion, repeat of a cleared stage 0.2x, boss re-fight 0.5x. Daily quests pay coins and materials, never XP, so the pacing above is independent of the engagement layer.

**Coins.** StageCoins(w, s) = round(0.5 × StageXP(w, s)); boss 2x. Side dungeon 1.2x, trial 1.5x, repeat 0.2x. Daily quests pay 1.0x a stage's coins each; weekly quests 5x.

## A2. Combat resolution

One damage formula, one parry resolver, one break rule and four status effects. Everything is integer damage after rounding, and every random roll uses the stage seed so the bots and the death replay are deterministic.

**Damage from the player**

```latex
\mathrm{Damage} = \max\big(1,\ \mathrm{round}((\mathrm{BaseAttack} + \mathrm{WeaponAttack}) \cdot m_{skill} \cdot m_{riposte} \cdot m_{broken} \cdot m_{crit} \cdot m_{boon}) - \mathrm{EnemyDefense}\big)
```

- m\_skill: 1.0 for an auto-attack; the Special's own multiplier (A3).
- m\_riposte: 2.0 during the riposte window (3.0 with Blade), else 1.0.
- m\_broken: 1.5 while the target is broken, else 1.0.
- m\_crit: 2.0 on a critical hit, else 1.0. Base crit chance 5%, raised by rings and skills; capped at 40%.
- m\_boon: product of active boon multipliers (B1), capped at 2.5.
- EnemyDefense: a flat value per family and world (A4), applied last, never reducing below 1.

**Damage to the player**

```latex
\mathrm{Damage} = \max\big(1,\ \mathrm{round}(\mathrm{AttackPower} \cdot m_{parry} \cdot m_{assist}) - \mathrm{Defense}\big)
```

- m\_parry: 0 on a precise parry, 0.5 on a soft parry, 1.0 otherwise. Red attacks ignore the parry entirely (m\_parry stays 1.0).
- m\_assist: 1.0 by default; the "hold to guard" assist applies 0.5 while held (no riposte, no break).
- Defense comes from armour (A3) and the Warden tree; capped so it never exceeds 40% of the incoming attack power (check after subtraction: if Damage < 0.6 × AttackPower × m\_parry × m\_assist, raise it to that).

**Parry resolver** (runs on the simulation thread at 60 Hz; times in ms; constants are remote-config keys in A7)

```
on TouchDown(zone == DEFENSE, t_touch):
  if parry.recoveryUntil > t_touch: return            // whiffed recently, ignore
  if parry.spamCount >= 2 and t_touch < parry.spamResetAt: return   // third rapid tap: no parry
  window = PRECISE_MS (200)                           // widened by assist to 280
  if parry.spamCount == 1 and t_touch < parry.spamResetAt: window = PRECISE_SPAM_MS (120)
  parry.activeFrom = t_touch - INPUT_BUFFER_MS (100)
  parry.preciseUntil = t_touch + window
  parry.softUntil   = t_touch + SOFT_MS (450)         // 550 with assist
  parry.spamCount   = (t_touch < parry.spamResetAt) ? parry.spamCount + 1 : 1
  parry.spamResetAt = t_touch + SPAM_WINDOW_MS (400)  // extended to 600 after a third tap
  play(parryStartAnim)

on EnemyHitFrame(attack, t_hit):                      // the last frame of the telegraph
  if attack.red: applyDamage(player, attack.power, m_parry=1.0); return
  if parry.activeFrom <= t_hit <= parry.preciseUntil:
      precise(attack)                                 // damage 0, stagger, riposte, break, Special charge
  elif t_hit <= parry.softUntil:
      soft(attack)                                    // damage x0.5, no stagger, no riposte, no break
  else:
      applyDamage(player, attack.power, m_parry=1.0)
      parry.recoveryUntil = max(parry.recoveryUntil, t_hit)

on ParryWhiff():                                      // precise window expired with no hit resolved
  parry.recoveryUntil = now + RECOVERY_MS (300)
```

A precise parry also consumes the attack: the attack cannot hit twice, and a multi-hit attack (volley) resolves each projectile separately against the same window, so one tap can reflect up to three arrows if they arrive inside 200 ms.

**Precise parry effects** (in this order)

1. Damage set to 0; hit stop 80 ms; haptic transient; parry sound with pitch-up if the tap was within the first 60 ms of the window ("perfect", used by skills).
2. Attacker staggered: 1.0 s normal, 0.6 s elite; bosses are not staggered.
3. Riposte window: 1.5 s (1.8 s at Blade mastery 3).
4. Break added: normal 0 (no bar), elite +25, boss +Break\_per\_parry from its script (B6), Hammer doubles it.
5. Special meter +16 (so 6 parries fill 100; Warden +20).
6. Projectiles are reflected back along their path at 1.5x speed and deal the weapon's current attack to the first enemy hit.

**Hits on enemies**: Special meter +4 per auto-attack hit (25 hits fill 100; Ranger +5). Break +2 per hit on elites and bosses.

**Break.** Elites: bar of 100, decays 10 per second when not hit, breaks at 100 for 3.0 s, then resets to 0 and the elite is immune to break for 8 s. Bosses: bar size and decay from the script (B6); on break, the current attack is cancelled, the boss is broken for 3.0 s, Execute becomes available. Execute damage = 6 × (BaseAttack + WeaponAttack), ignores defense, ends the broken state.

**Status effects** (applied by weapon trait, boons or skills; one stack each except Bleed)

| Status | Effect | Duration | Stacks | Applied by |
| --- | --- | --- | --- | --- |
| Burn | 4% of the applier's attack per 0.5 s | 4 s, refreshed | 1 | Wand trait, boons |
| Chill | Move and attack speed 0.7x; telegraphs 15% longer | 3 s | 1 | Chakram trait, boons |
| Shock | On application, 50% of the hit's damage jumps to the nearest enemy within 2 units | instant | n/a | Spear trait, boons |
| Bleed | Target takes +10% damage per stack | 5 s | up to 3 | Blade trait, boons |

Status effects never apply to the player; enemy hazards use their own rules (A4).

**Worked example** (world 2, stage 7, level 11, Rare Blade level 3)

- Player attack = 24.0 + 21.2 = 45.2. Thornback (world 2) HP 284, defense 4. Auto-attack: round(45.2) − 4 = 41 per hit, 2.0 per second: dead in 7 hits, 3.5 s.
- The Thornback swings (white, 800 ms). Tap at 150 ms before the hit frame: precise. Damage 0, stagger 1.0 s, riposte: next hits deal round(45.2 × 3.0) − 4 = 132, so two hits in the riposte window kill it: 1.0 s.
- Same swing, tap 320 ms before the hit frame: soft. Attack power 23 × 0.5 = 11.5, round 12, minus armour defense 3 = 9 damage; floor check: 0.6 × 23 × 0.5 = 6.9, so 9 stands. Player health 235 to 226.
- A Shellback jab unparried: 23 − 3 = 20 damage, about 8.5% of health; eight unparried hits kill, as designed (12% at the world's entry level, less once levelled).

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

## A5. State machines and algorithms

The player has nine states and auto-attack is a layer that runs on top of three of them; enemies share one eight-state machine with per-family overrides; four small algorithms (targeting, Action resolver, camera, gesture classifier) are specified as pseudocode so two engineers would implement them the same way.

**Player state machine**

| State | Enter on | Exit to | Auto-attack layer runs | Notes |
| --- | --- | --- | --- | --- |
| Idle | no input | Move, Parry, Dodge, Special, Action states | yes |  |
| Move | joystick magnitude > dead zone | Idle on release | yes | speed 4.5 units/s times magnitude |
| Parry | defense tap | Idle or Move after 200 ms window plus recovery if whiffed | no (attack animation is interrupted, cadence timer keeps running) | movement continues at 0.5x during the window |
| Dodge | defense swipe with a charge available | Idle or Move after 250 ms | no | i-frames 0 to 180 ms; cannot be cancelled |
| Special | Special button with meter 100 | Idle or Move after the Special's duration | no | movement locked for Blade and Hammer, free for others |
| Drink | Action = Potion | Idle after 600 ms; Dodge cancels and refunds the potion | yes |  |
| Interact | Action = Open, Pull, Pray, Pick up | Idle after 400 ms | no | enemies cannot spawn during the first 400 ms of a rest room |
| Execute | Action = Execute | Idle after the 600 ms cinematic | no | invulnerable throughout |
| Hit | damage taken and not parried | previous state after 120 ms | no | no knockback except from red slams (1.0 unit) |
| Dead | health 0 | Failure screen | no | replay buffer frozen |

Auto-attack layer: every 1/cadence seconds, if a target is in reach and the state allows it, play the attack and resolve the hit at the animation's hit frame (40% through the swing). If the state does not allow it, the timer keeps running so the next attack fires as soon as the state returns.

**Targeting** (runs every step)

```
candidates = enemies within weapon.range * 1.25 (so the character steps toward a target just out of reach)
if pinned and pinned in candidates: return pinned
winding = candidates with state == Windup and attack targets player
if winding: return nearest(winding)
if candidates: return nearest(candidates) tie-break lowest health
return nearest(enemies)    // out of reach: face it, do not attack
```

**Enemy state machine**

| State | Behaviour | Transitions |
| --- | --- | --- |
| Spawn | Edge marker shown 1.0 s, then enter at 1.5x speed for 0.5 s; untargetable until fully inside | Approach |
| Approach | Move toward the player along the vertical axis first, then horizontal; keep 0.3 units from allies | Windup when in reach and cooldown elapsed; family override: Stoker and Archer hold at range, Wisp blinks |
| Windup | Telegraph pose, flash on first frame, sound; duration from the family record | Hit at the end; Stagger if parried precisely; Broken if the bar fills |
| Hit | One frame; resolve damage against the parry window (A2) | Recover |
| Recover | 300 ms idle; cooldown timer starts | Approach |
| Stagger | 1.0 s (elite 0.6 s): no movement, takes riposte damage | Approach |
| Broken | 3.0 s: takes 1.5x damage, Execute available; cancels any windup | Approach; immune to break 8 s |
| Dead | Death animation under 300 ms; drops, trait on-death effects, spirit of the room counter | removed |

Family overrides are data: Shellback adds a shield flag that routes frontal damage to zero until a precise parry sets shieldOpen for 3 s; Wisp inserts Blink (600 ms marker, teleport, then Windup); Automaton alternates attack ids; Stoker adds a Buff state every 6 s; Sentinel's Windup places the ring, and its Hit resolves against everyone inside; Archer's Hit spawns three projectiles 120 ms apart, each a parryable entity of its own.

**Contextual Action resolver** (every step; emits one action or none)

```
action = none
broken = nearest enemy with state Broken within 1.5 units
if broken: action = EXECUTE(broken)
else:
  interactables = objects within 1.5 units with a prompt (chest, lever, shrine, relic, merchant)
  if interactables: action = INTERACT(nearest)
  elif player.health < 0.40 * max and player.potions > 0 and not inCombatPause: action = POTION
if action != shown.action:
  shown = action; shown.armedAt = now + 200 ms; pulseOnce()
if touch is held on the button: keep shown unchanged until release
button.enabled = shown.action != none and now >= shown.armedAt
```

**Camera** (every render frame; world units; portrait)

```
visibleW = 9; visibleH = 9 * screenH / screenW
anchorY = 0.45 * visibleH                       // character's target distance from the top edge
threatCentroid = mean position of enemies in Windup, or player position if none
lead = clamp(threatCentroid - player, -1.5, +1.5) per axis
targetCenter = player + lead; targetCenter.y -= (visibleH/2 - anchorY)
targetCenter.x = clamp(targetCenter.x, arena.left + visibleW/2, arena.right - visibleW/2)   // arena is 9 wide, so x is fixed
targetCenter.y = clamp(targetCenter.y, arena.bottom + visibleH/2, arena.top - visibleH/2)
if hitStopActive: do not move
else camera.center = damp(camera.center, targetCenter, 150 ms)
threatBandTop = screenH * 0.78 (in screen space)
for each enemy in Windup whose attack origin projects below threatBandTop: draw edge indicator at (x, threatBandTop - 16 pt)
for each spawn marker off the top edge: draw at (x, hudBottom + 8 pt)
```

**Gesture classifier** (touch events with OS timestamps; zones from design section 5)

```
on down(t0, p0):
  if p0 in button: route to button; return
  if p0 in MOVE zone: joystick.origin = p0; joystick.active = true; return
  // DEFENSE zone
  parryResolver.touchDown(t0)          // fires immediately (A2)
  gesture = {t0, p0, decided: false}
on move(t, p):
  if joystick.active: joystick.vector = clamp((p - origin) / 48 pt, 1.0); dead zone 8 pt; return
  if gesture and not decided and |p - p0| >= 12 pt and t - t0 <= 60 ms:
      decided = true; dodge(direction = normalize(p - p0))      // parry frames already active stay active
on up(t, p):
  if joystick.active: joystick.active = false; joystick.vector = 0; return
  if gesture and not decided and t - t0 >= 350 ms and enemyUnder(p): pin(enemyUnder(p), 5 s)
  gesture = none
```

Left-handed mode mirrors the zones and buttons; the dedicated dodge button setting adds a 56 pt button above the Action button and disables swipe-to-dodge.

**Boon offer** (after rooms flagged boon\_after; seeded by stage seed and room index)

```
pool = stage.boon_pool minus boons at max stacks minus boons excluded by class
statBoons = pool where kind == stat; ruleBoons = pool where kind == rule
offer = 2 random from ruleBoons + 1 random from statBoons (if either runs short, fill from the other, never two of the same id)
if the player has a pick-once boon already, it is excluded
```

**Spawn director.** Reads the room's spawn list in order; a group spawns at its time t unless the active-enemy cap would be exceeded, in which case it waits and all later times shift by the wait. Both-edge groups alternate top, bottom. The room ends when the list is exhausted and no enemy is alive. A gauntlet room starts the next wave 1.0 s after the previous wave's last death.

## A6. Save file schema

One versioned JSON document, written atomically (write to a temp file, then rename), kept locally as the source of truth and mirrored to the platform cloud save. Everything the player owns or has done is in it; nothing about the current room is, because a stage resumes at the start of the current room, not mid-fight.

```json
{
  "schema": 3,
  "player_id": "uuid",
  "created_at": "2027-12-07T10:00:00Z",
  "updated_at": "2027-12-09T18:21:04Z",
  "playtime_active_s": 61420,
  "character": {
    "level": 23, "xp": 70212, "class": "warden", "skill_points_unspent": 1,
    "skills": { "warden": ["w1","w2","w4","w7"], "ranger": ["r1"], "mystic": [] },
    "loadout": { "weapon": "inv_0f3a", "armour": "inv_9c21", "ring_1": "inv_1b77", "ring_2": null },
    "unlocks": { "classes": ["warden","ranger"], "families": ["blade","hammer","spear"], "dodge_charges": 2 }
  },
  "inventory": [
    { "id": "inv_0f3a", "kind": "weapon", "family": "blade", "rarity": "epic", "level": 3, "mastery_xp": 1200 },
    { "id": "inv_9c21", "kind": "armour", "rarity": "epic", "level": 2, "rule": "bulwark" },
    { "id": "inv_1b77", "kind": "ring", "rarity": "rare", "quality": "fine", "affixes": [ { "id": "crit_chance", "value": 0.06 }, { "id": "riposte_duration", "value": 0.3 } ] }
  ],
  "currencies": { "coins": 4120, "gems": 85, "shards": 7, "potions": 2, "materials": { "w1": 3, "w2": 0, "w3": 14, "w4": 22 } },
  "progress": {
    "stages": { "w1-s01": { "cleared": true, "best_time_s": 142, "deaths": 0, "stars": [true,true,false] } },
    "current": { "stage": "w4-s09", "room": 2, "boons": ["riposte_plus","quick_feet"], "potions_at_start": 3, "seed": 918273 },
    "worlds_unlocked": 4, "dungeons_cleared": ["w2-d1","w2-d2"], "trials_cleared": [], "bosses_refought": {}
  },
  "mastery": { "weapons": { "blade": { "level": 4, "xp": 3100 } }, "stars_total": 41 },
  "engagement": {
    "calendar": { "day_index": 4, "last_claim_date": "2027-12-09" },
    "streak": { "days": 9, "last_play_date": "2027-12-09", "forgiveness_used_week": "2027-W49" },
    "daily": { "date": "2027-12-09", "quests": [ { "id": "dq_parry_20", "progress": 14, "done": false, "claimed": false } ], "first_win_claimed": true },
    "weekly": { "week": "2027-W49", "quests": [] },
    "achievements": { "ach_w1_clear": "2027-12-07T12:00:00Z" },
    "season": { "id": "s1", "tier": 6, "points": 1340, "premium": false, "claimed_tiers": [1,2,3,4,5,6] },
    "events": { "ev_frost_01": { "stages_cleared": 1 } },
    "last_seen_at": "2027-12-09T18:21:04Z", "return_reward_claimed_at": null
  },
  "settings": { "left_handed": false, "dodge_button": false, "assist_parry": false, "assist_telegraph": false, "hold_guard": false, "colour_mode": "default", "haptics": true, "reduced_motion": false, "damage_numbers": false, "music": 0.8, "sfx": 1.0, "notifications": "off" },
  "purchases": { "ad_free": false, "starter_bundle_offered_at": "2027-12-07T12:40:00Z", "receipts": [] },
  "tutorial": { "steps_done": ["move","parry","riposte","dodge","special","boon","action","potion","home"] }
}
```

**Rules**

- Save triggers: room clear, stage end (win or fail), any purchase, any equipment or skill change, any claim, app background. A save takes under 20 ms on the main thread or runs on a worker.
- Resume: on launch, if `progress.current.stage` is set, the Map centres on it and offers Continue, which starts at `room` with the listed boons and `potions_at_start` minus potions used in earlier rooms (tracked by a `potions_used` field added on room clear).
- Migration: `schema` increments on any breaking change; each version has a migration function run in order; migrations are tested against saved fixtures from every shipped version.
- Cloud: upload after each local save, debounced to 30 s; on launch, if the cloud copy's `updated_at` is newer and its `playtime_active_s` is greater, prompt once ("Use cloud progress from 9 Dec, 17:02?"); otherwise keep local.
- Dates are UTC; the day boundary for calendar, streak and dailies is 04:00 in the device's local time zone, stored as the date string shown above.
- Corruption: if the file fails to parse, restore the previous write (two rotating copies) and log `save_recovered`.

## A7. Analytics event schema and remote-config keys

Thirteen events with typed fields and a common envelope, and 38 remote-config keys that cover every number a live balance change might need. Events are batched and sent on stage end and app background; nothing is sent per frame.

**Envelope on every event**: `event` (string), `ts` (ISO 8601 UTC), `player_id` (uuid), `session_id` (uuid), `build` (string, e.g. 1.0.3+412), `platform` (ios | android), `device_class` (low | mid | high, from a benchmark at first launch), `world` (int), `stage` (string id), `class` (string), `weapon_family` (string), `weapon_rarity` (string), `level` (int), `assist_flags` (string list).

| Event | Fields | Type |
| --- | --- | --- |
| app\_open | cold (bool), seconds\_since\_last\_open (int), return\_reward\_shown (bool) | per launch |
| tutorial\_step | step (string), seconds\_from\_app\_open (int) | FTUE funnel |
| stage\_start | mode (campaign, dungeon, trial, refight, challenge), attempt\_n (int), potions (int), loadout (object) |  |
| stage\_end | result (win, fail, quit), duration\_s (int), rooms\_cleared (int), deaths (int), potions\_used (int), boons (string list), damage\_taken (int), parries\_precise (int), parries\_soft (int), parries\_missed (int), dodges\_ok (int), executes (int), stars\_earned (int list), xp (int), coins (int), materials (int) | the core event |
| parry | result (precise, soft, miss, spam\_blocked), enemy\_family (string), attack\_id (string), delta\_ms (int, signed: tap time minus hit frame), room (int) | sampled 100% in soft launch, 20% after |
| dodge | absorbed\_hit (bool), direction (string), trigger (swipe, button) | sampled as above |
| death | attack\_id (string), enemy\_family (string), room (int), health\_history (int list, 10 s at 10 Hz), seed (int) |  |
| boon\_pick | offered (string list), chosen (string), room (int) |  |
| equip\_change | slot (string), from\_item (string), to\_item (string), context (preview, hub) |  |
| economy | action (upgrade, craft, reroll, refine, dismantle, respec, potion\_buy), item (string), coins\_delta (int), materials\_delta (int), shards\_delta (int), balances (object) |  |
| engagement | action (calendar\_claim, streak\_day, quest\_complete, quest\_claim, first\_win, challenge\_play, return\_claim, season\_tier, event\_stage), id (string), value (int) |  |
| monetization | action (offer\_shown, offer\_dismissed, purchase, ad\_offered, ad\_completed, ad\_skipped), offer\_id (string), price\_usd (float), context (string) |  |
| perf | fps\_p50 (float), fps\_p05 (float), slow\_frames\_pct (float), memory\_mb (int), thermal (string), load\_s (float), scene (string) | per stage end |

Settings changes send `engagement` with action `setting_change` and id = the setting key.

**Remote-config keys** (type, default; read at app open and on stage start, never mid-stage)

| Group | Key | Default |
| --- | --- | --- |
| Parry | parry.precise\_ms | 200 |
|  | parry.soft\_ms | 450 |
|  | parry.recovery\_ms | 300 |
|  | parry.input\_buffer\_ms | 100 |
|  | parry.spam\_window\_ms | 400 |
|  | parry.spam\_precise\_ms | 120 |
|  | parry.assist\_precise\_ms | 280 |
|  | parry.assist\_soft\_ms | 550 |
|  | parry.perfect\_ms | 60 |
|  | parry.riposte\_s | 1.5 |
|  | parry.special\_gain | 16 |
| Dodge | dodge.duration\_ms | 250 |
|  | dodge.iframes\_ms | 180 |
|  | dodge.cooldown\_ms | 800 |
| Telegraph | telegraph.floor\_ms | 450 |
|  | telegraph.world\_shrink | 0.04 |
|  | telegraph.assist\_mult | 1.2 |
| Enemy | enemy.M (list of 8) | 1.00, 2.25, 3.16, 5.06, 6.44, 7.97, 11.05, 13.66 |
|  | enemy.A (list of 8) | 1.00, 1.92, 3.00, 4.17, 5.75, 7.50, 9.42, 11.58 |
|  | enemy.stage\_growth | 0.012 |
|  | enemy.elite\_health\_mult | 4.0 |
|  | enemy.cap\_campaign | 6 |
|  | enemy.cap\_trial | 8 |
| Break | break.elite\_decay\_per\_s | 10 |
|  | break.boss\_decay\_per\_s | 6 |
|  | break.broken\_s | 3.0 |
|  | break.execute\_mult | 6 |
| Economy | econ.stage\_xp\_B (list of 8) | 157, 717, 1561, 3108, 4801, 6758, 8957, 8296 |
|  | econ.coin\_ratio | 0.5 |
|  | econ.repeat\_mult | 0.2 |
|  | econ.materials\_per\_stage | 3 |
|  | econ.materials\_per\_boss | 12 |
|  | econ.potion\_cost | 60 |
|  | econ.reroll\_shards | 3 |
| Engagement | eng.calendar\_values (object by world) | B8 |
|  | eng.streak\_forgiveness\_per\_week | 1 |
|  | eng.return\_days | 3 |
|  | eng.notification\_min\_days\_played | 3 |
| Monetization | mon.starter\_bundle\_after\_stage | w1-s08 |
|  | mon.rewarded\_double\_per\_day | 5 |

A remote-config change is logged as an `engagement` event with action `config_applied` and the changed keys, so cohorts can be split by config version.
