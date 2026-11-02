<!-- from md/01-design.md -->

## 13. Retention and LiveOps

The engagement layer ships at launch in full: an in-play tutorial, a seven-day reward calendar with a streak that forgives a missed day, three daily and three weekly quests, achievements, mastery stars, a free season track, a rotating weekly challenge stage, and return rewards. Its job is to give a reason to open the app; the campaign's job is to make the session worth it. Nothing in this section counts toward the 30 hours.

**First-time experience** (stages 1-1 to 1-4, no separate tutorial mode)

| Stage | Teaches | How |
| --- | --- | --- |
| 1-1 room 1 | Move | One Thornback that never attacks; the joystick hint fades after the first drag |
| 1-1 room 2 | Parry | One Thornback with a 1,000 ms telegraph; the game slows to 30% on its first flash with a "tap now" marker; the first successful parry triggers the full hit-stop, flash, haptic and a one-word callout |
| 1-1 room 3 | Auto-attack and riposte | Two enemies; the riposte damage is shown once with a callout |
| 1-2 | Dodge | An Automaton-style red slam from a Thornback variant; the game slows on the first red and shows a swipe hint |
| 1-3 | Special and boons | The meter fills visibly; the first boon pick pauses with a one-line explanation of expiry |
| 1-4 | Action button and potions | A rest room with a chest; a scripted hit to 35% health, then the Drink prompt |
| After 1-4 | Daily reward and quests | The home screen shows the calendar and the first daily quest, once, with a two-line overlay |

Targets: first parry within 30 seconds of app open; first stage won within 2 minutes; 95% of installs reach 1-2; 90% clear 1-1 on the first attempt.

**Daily and weekly**

| System | Spec |
| --- | --- |
| Seven-day calendar | Day 1 coins; 2 potions; 3 materials; 4 shards; 5 coins; 6 a cosmetic frame; 7 gems and a Rare ring. Values scale with the player's current world. Resets after day 7. |
| Streak | Counts consecutive days; one missed day is forgiven per week; a streak at 14 and 30 days awards gems and a title. No reset to zero on one miss. |
| Daily quests (3) | Drawn from a pool tied to play: "parry 20 attacks", "clear any stage without a potion", "win with a Spear", "Execute twice". Each finishable in one session. Rewards: coins and materials for the current world. |
| Weekly quests (3) | "Earn 6 mastery stars", "clear a side dungeon", "defeat a boss re-fight". Rewards: gems and shards. |
| First win of the day | Double coins on the first stage cleared each day. |
| Weekly challenge stage | A rotating authored stage with a modifier (Hasty enemies, parry-only, mirrored colours). Leaderboard is personal best only at launch. Rewards gems. |
| Return rewards | Away 3 days or more: a catch-up crate of the current world's materials and a one-screen "what's new". Away 14 days or more: also a free respec and a Rare ring. |

**Achievements.** About 80 at launch in four groups: progression (worlds, bosses), mastery (stars, perfect parries, no-damage bosses), collection (weapons, rings, cosmetics), and style ("reflect 100 arrows", "win a boss using only soft parries"). Each pays gems; the style group exists to teach techniques.

**Seasons and events.** Five-week seasons with a free reward track of 30 tiers driven by season quests (three categories: campaign, mastery, challenge), one week of rest between seasons as Roblox's guidance suggests. Each season adds one event: a themed dungeon with three stages, a modifier set and cosmetics, available for the season and returning later. New campaign content ships between seasons: a new world or a trial set every 8 to 10 weeks after launch.

**Notifications.** Off by default until the player has opened the game on three separate days. Then at most one per day, only for a claimable reward or a new event, with a one-tap opt-out in the notification itself.

**What is deliberately not copied from the Roblox and survivor-like playbooks**

- No streak reset to zero on one missed day.
- No time-played rewards that reward leaving the app open; playtime milestones count active stage time only.
- No daily chores needed to progress; a player who ignores every quest clears the campaign on schedule.
- No energy, no AFK rewards, no paid skips.
- No more than one popup per session on the home screen.

**Measured by** D1, D7, D30 cohorts; calendar claim rate; quest completion rate per quest (quests under 20% completion are rewritten); streak length distribution; return-reward claim rate; event participation (section 16).
