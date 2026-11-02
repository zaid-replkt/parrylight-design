<!-- from md/01-design.md -->

## 11. Encounter and level design

A stage is a data file: an arena, an ordered list of rooms, each room a list of timed spawn groups, a hazard rule, a boon pool and three mastery objectives. 293 stages are feasible only because designers author data against reusable templates and two bots validate every stage automatically before a human plays it.

**Stage definition** (illustrative schema; the real file is JSON validated against a schema in the repo)

```json
{
  "id": "w2-s07",
  "world": 2,
  "arena": { "template": "saltflats_long", "height": 24, "rule": "tide_band", "rule_params": { "period_s": 9, "push": 1.5 } },
  "recommended_level": 11,
  "rooms": [
    { "type": "wave", "spawns": [ { "t": 0, "edge": "top", "family": "thornback", "n": 2 }, { "t": 6, "edge": "bottom", "family": "shellback", "n": 1 } ] },
    { "type": "wave", "spawns": [ { "t": 0, "edge": "top", "family": "shellback", "n": 2, "traits": ["hasty"] } ], "boon_after": true },
    { "type": "gauntlet", "waves": 3, "spawns_per_wave": [ { "edge": "both", "family": "mixed_w1_w2", "n": 3 } ] },
    { "type": "elite", "family": "shellback", "traits": ["armoured"], "adds": { "family": "thornback", "n": 2, "every_s": 12 } }
  ],
  "boon_pool": ["riposte_plus", "chill_on_parry", "second_wind", "heavy_hands", "quick_feet"],
  "mastery": [ { "type": "no_damage_room", "room": 2 }, { "type": "parries", "n": 15 }, { "type": "time_under_s", "s": 240 } ],
  "rewards": { "xp": 420, "coins": 180, "materials": { "salt_shard": 3 }, "first_clear": { "ring": "rolled_rare" } }
}
```

**Room types**

| Type | Shape | Used for |
| --- | --- | --- |
| Wave | One spawn list, ends when all are dead | The default room |
| Gauntlet | Several waves with no pause, spawns from both edges | Pressure; late-stage rooms |
| Elite | One elite plus periodic adds | Mid-stage and dungeon finales |
| Rule room | A wave where the arena rule is at maximum strength | Teaching rooms early in a world |
| Rest | No enemies; a chest, a shrine or the merchant via the Action button | Pacing; one per stage at most, never in the last two rooms |
| Boss | Scripted (section 10) | Stage 25 |

**Boons** (in-stage, expire at stage end). A pool of about 40 across the game, five to eight per stage pool, three offered after rooms flagged "boon\_after". Each boon changes a rule rather than a number where possible ("parries also reflect projectiles", "your second dodge in 2 s is free"); pure stat boons exist but are never more than one of the three offered. The boon pick is where a stage gets replay variety without random stage layouts.

**Arena templates.** Each world has three arena templates (short 16, long 24, boss 16) with fixed decoration slots. Hazards attach to templates by rule name. Designers do not place individual tiles; they choose a template and parameters, which keeps every arena within the portrait rules in section 6 by construction.

**Spawn rules for portrait**

- Spawn edges are top and bottom only; a spawn marker shows on the edge 1 s before the enemy enters.
- No more than two spawn groups within 2 s of each other, and never from both edges within 1 s, so the player can turn to face one side at a time.
- Ranged families spawn at the top only, where the camera lead keeps them in frame.
- Active enemy cap per room is in the stage data and validated against the section 10 maximums.

**Validation before a human plays**

1. Schema validation: the file matches the schema; families, traits and boons exist; caps respected.
2. Perfect bot: an automated player that parries every parryable attack on its hit frame and dodges every red. It must clear the stage with zero damage taken. If it cannot, the stage has an unreadable or impossible overlap and is rejected.
3. Passive bot: an automated player that moves but never parries or dodges. It must die before the final room in every stage from world 2 onward. If it survives, the stage can be won by standing there, which violates pillar 1.
4. Timing report: the expected first-clear time from both bots brackets the design target in section 9; stages outside the bracket are flagged.
5. Human pass: a designer plays the stage once and names the new decision it asks (section 9). The name is stored in the file.

**Difficulty curve.** Three measured dials per stage, logged by the bots and by live analytics: telegraph density (attacks per 10 s that require a response), red share (fraction of attacks that are unparryable), and simultaneous threats (peak attacks overlapping within 500 ms). Each world raises one dial at a time; a stage that raises two at once must be stage 20 or the boss.
