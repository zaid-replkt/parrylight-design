<!-- from md/02-build-spec-A-formulas-and-systems.md -->

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
