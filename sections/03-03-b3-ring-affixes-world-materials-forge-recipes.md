<!-- from md/03-build-spec-B-content-tables.md -->

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
