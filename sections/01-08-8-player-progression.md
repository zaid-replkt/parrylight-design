<!-- from md/01-design.md -->

## 8. Player progression

Progression is five tracks that each change how a fight plays, not only how big the numbers are: class, level, equipment, skills, and mastery. Stats account for about half of the difficulty curve; the other half is the player learning the telegraph grammar. A skilled player 5 levels under the recommended level can clear any campaign stage; an unskilled player 5 levels over it can clear with potions. Nothing in the campaign is gated by level.

**Classes** (three at launch, each changes the defense game)

| Class | Unlock | Parry | Dodge | Special | Playstyle |
| --- | --- | --- | --- | --- | --- |
| Warden | Start | Parry also heals 3% of max health | Standard | Charges 20% faster from parries | Stand and deflect |
| Ranger | Clear world 2 | Standard | Two charges from the start; dodging through an enemy marks it (+15% damage taken) | Charges 20% faster from hits | Kite and punish |
| Mystic | Clear world 4 | A parry applies the weapon's status to the attacker | Standard | Special meter is 50% larger and effects last longer | Build around the Special |

Classes are switched freely at the loadout sheet. Each class has its own skill tree and its own mastery, so a second class is a second progression track, not a cosmetic.

**Level.** Levels 1 to 60 from stage experience. Each level adds health and attack on a gentle curve, and every second level grants one skill point. Experience is awarded for clearing stages and mastery objectives; repeating a cleared stage pays 20% experience, so grinding is possible but never efficient.

**Skills.** Each class has a tree of three branches of five nodes (15 nodes, 30 points available by level 60, so a full tree is possible but ordering matters for 30 hours). Nodes are rules, not percentages: "a perfect parry (first 60 ms of the window) refunds the dodge", "the third riposte hit staggers", "Chill lasts twice as long". Respec costs soft currency and is free the first three times.

**Equipment.** Four slots: weapon, armour, two rings.

| Slot | Source | Rarity | Upgrade path |
| --- | --- | --- | --- |
| Weapon | Guaranteed at campaign milestones (new families at 1-8 and at each world clear through world 3; a higher rarity as worlds 2, 4 and 7 open), plus Forge crafting from world materials (spec A3) | Common, Rare, Epic, Legendary | 8 levels per weapon with world materials; level 3 unlocks the weapon trait, level 6 upgrades the Special |
| Armour | Milestones and Forge | Same four | 8 levels; adds health, defense, and one defensive rule at level 5 ("the first hit in each room is halved") |
| Rings | Side dungeons, trials, bosses | Same four | Rolled affixes from a short, readable list; re-rolling costs a currency earned from dismantling, so a bad roll is never permanent |

There are no duplicate-based upgrades and no equipment gacha. The Forge shows exactly what a craft yields before the player commits.

**Mastery.** Two kinds. Weapon mastery levels 1 to 10 per family, earned by use, each unlocking a small perk for that family (Blade 3: riposte window 1.5 s becomes 1.8 s). Stage mastery: every stage has three objectives (for example: no damage taken in room 2, parry 12 attacks, clear under 4 minutes). Each earns a star; stars unlock side dungeons and trials (section 9) and cosmetic frames. Mastery objectives are the sanctioned reason to replay a stage, and they ask for a different approach, not a repeat.

**Pacing targets** (first-clear path, average skill)

| World | Expected level on entry | Weapon tier | New system introduced |
| --- | --- | --- | --- |
| 1 | 1 | Common Blade | Parry, dodge, Special, boons |
| 2 | 8 | Rare | Rings, Forge, first elite break, side dungeons |
| 3 | 15 | Rare to Epic | Ranger class, second dodge charge, status effects |
| 4 | 22 | Epic | Weapon mastery perks, trials |
| 5 | 30 | Epic | Mystic class, boss arenas with summons |
| 6 | 38 | Epic to Legendary | Boss re-fights with modifiers |
| 7 | 46 | Legendary | Multi-phase bosses with two break cycles |
| 8 | 54 | Legendary | Endgame trials, mastery hunts |

**What the Pixel Blade research changes here.** Pixel Blade's progression leans on duplicate-fed weapon levels, unidentified rings that cannot be rerolled, and a "Wishes" gacha for rare gear, and its guides describe World 4 as a difficulty spike with off-screen ranged attacks. Each of those is designed out above: milestone-guaranteed weapons, rerollable rings, no gacha, and a camera that keeps telegraphs on screen (section 6).
