<!-- from md/01-design.md -->

## 10. Enemy and boss design

Every enemy is defined by the question it asks the defense game (parry it, dodge it, or reposition), and every boss is a scripted sequence of those questions with two to four planned break windows. Enemies are data: a family, a behaviour set, a telegraph profile and stats, so a new enemy is a content entry, not new code.

**Enemy families** (one per world, then recombined)

| Family | Behaviour | Telegraph profile | The question it asks | Counter |
| --- | --- | --- | --- | --- |
| Thornback (W1) | Walks to melee range, one slow swing | White, 800 ms | Can you parry on the flash? | Parry |
| Shellback (W2) | Shielded front, immune from the front until parried | White jab, 700 ms; shield glows when open | Will you parry to open, or walk around? | Parry opens the shell for 3 s |
| Wisp (W3) | Teleports to a marked spot, then attacks | Blue blink marker 600 ms, then white 500 ms | Can you track a target that moves before it attacks? | Dodge the blink, parry the strike |
| Automaton (W4) | Alternates parryable jabs and unparryable slams | White 700 ms / red 900 ms with ground marker | Can you read red from white under pressure? | Parry jabs, dodge slams |
| Stoker (W5) | Stays back, buffs the nearest ally every 6 s | Blue pulse 1 s before the buff | Do you change target priority? | Pin it; Special |
| Sentinel (W6) | Places delayed area rings | Yellow ring fills over 1.2 s; white edge if parryable | Do you leave, or clear it with a parry? | Leave the ring or parry the edge |
| Archer (W7) | Volleys of 3 projectiles from range | White per arrow, 650 ms | Can you reflect, and where does the reflection go? | Parry reflects into the archer |
| Elite variants (all worlds) | Any family with a break bar and one extra trait | Same grammar, larger sprite, distinct outline | Can you keep the grammar going for longer? | Build break, Execute |

**Traits** (stackable on elites and used by stage data): Hasty (telegraphs 15% shorter), Armoured (first parry each room only staggers), Volatile (dies in a yellow ring), Linked (shares damage with another Linked enemy), Vengeful (buffs allies on death). Stages never combine more than two traits on one enemy.

**Rules for every enemy**

- Every attack has a telegraph that is readable on a 9:16 screen from the character's position; off-screen attacks do not exist (edge indicators, section 6).
- The hit frame is the last frame of the telegraph, never during it.
- Each family has one parryable and, from world 4 onward, at most one unparryable attack; red is reserved for the unparryable.
- Enemies approach from the top or bottom; none walk in from the sides.
- Normal enemies die in 2 to 5 seconds of auto-attack at the expected level; elites in 10 to 15 seconds plus one break.
- Maximum 6 active enemies on screen in campaign, 8 in trials. Portrait width does not fit more without stacking telegraphs.

**Boss design.** Each campaign boss is a script of phases, with break windows placed on purpose.

| Beat | What happens | Design intent |
| --- | --- | --- |
| Intro, 1.5 s | Camera pull-out, boss name, no attacks | Read the arena |
| Phase 1 | Two attacks: one parryable, one unparryable, alternating in a fixed order | Teach the boss's grammar |
| Break 1 | 6 parries fill the bar; Execute | Reward reading over DPS |
| Phase 2 | A new attack that combines the world's rule (tide band, conveyor, ring) | New decision |
| Break 2 | Fewer parries needed if the player used the rule (for example, parried from a conveyor) | Reward using the arena |
| Phase 3 (worlds 6 to 8) | Pattern order becomes semi-random from a set of 3; a summon or a split | Mastery check |
| Final break | Execute ends the fight with a cinematic | Memorable close |

Boss attacks are tuned so that a player who parries every parryable attack and dodges every red takes no damage; potions exist for everyone else. Boss arenas are 9 by 16 units with no scrolling. Bosses are re-fightable from the world map after the first clear, with modifiers unlocked at world 6.

**Elites and mini-bosses.** Stage 12 of each world is a mini-boss: an elite with a full script of two phases and one break. Side dungeons end on an elite pair, and trials use elites with stacked traits.
