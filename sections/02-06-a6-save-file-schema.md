<!-- from md/02-build-spec-A-formulas-and-systems.md -->

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
