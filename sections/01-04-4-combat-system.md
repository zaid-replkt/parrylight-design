<!-- from md/01-design.md -->

## 4. Combat system

Combat is a defense game: the character attacks by itself, and every point of skill expression is in the parry, the dodge, where you stand, and when you spend the Special. The rule that keeps this honest is that the auto-attack alone must never clear a stage above world 1; enemy damage is tuned so that an unparried stage ends in death.

**Auto-attack.** The character attacks the current target continuously, including while moving. There is no stop-to-shoot. Target priority: the enemy currently winding up an attack on the player, then the nearest, then the lowest health. The player can tap an enemy to pin it as priority for 5 seconds. Weapon families define the attack: range, cadence, hit shape and parry bonus.

| Weapon family | Hit shape | Cadence | Parry bonus | Role |
| --- | --- | --- | --- | --- |
| Blade | Short arc in front | Fast | Riposte deals 3x instead of 2x | Default, balanced |
| Spear | Line, mid range | Medium | Parry also pushes enemies back | Crowd control |
| Chakram | Thrown, returns, ranged | Medium | Parry reflects projectiles | Ranged, kiting |
| Hammer | Slow arc, area | Slow | Parry builds double break | Boss breaker |
| Wand | Homing bolt, ranged | Fast, low damage | Parry refunds 25% Special | Caster, ability focused |

**Parry.** Tap anywhere in the right-hand combat zone. The parry is active instantly for a short precise window, followed by a longer soft tier that halves damage without the reward, then a recovery during which a second tap does nothing. If an enemy's parryable hit lands inside the window: damage is negated, the enemy is staggered, the character's next attacks for 1.5 seconds are riposte attacks at double damage, and the Special meter gains charge. The parry is the only way to build meaningful break on bosses, so it is never optional against them.

**Dodge.** Swipe in the combat zone in any direction. A short dash with invulnerability frames in the first part of it. Dodge is for unparryable attacks (red telegraphs) and for repositioning out of area attacks. One charge at the start; a second charge is an unlock in world 3.

**Special.** One fixed button. Its effect comes from the equipped weapon, modified by class. It is charged by parries and hits, not by a timer, so a player who parries well casts more often. Full charge is roughly 6 parries or 25 hits. Examples: Blade Crescent (wide 180 degree slash), Hammer Quake (area stagger around the character), Wand Nova (ring of bolts that each apply the wand's status).

**Break and Execute.** Elites and bosses carry a break meter under their health bar. Parries fill it fast, hits fill it slowly. At full, the enemy is broken for 3 seconds, takes 1.5x damage, and the contextual Action button offers Execute: a cinematic high-damage strike that also clears the enemy's current attack pattern. Bosses break two to four times per fight by design, and each break is a planned beat in the fight script (section 10).

**Telegraph language.** Every enemy attack is announced before it lands, in one consistent visual grammar. Players learn the grammar in world 1 and never have to relearn it.

| Cue | Meaning | Correct answer |
| --- | --- | --- |
| White flash and wind-up pose, white outline on the enemy | Parryable melee or projectile | Parry on the flash |
| Red flash, red outline, red ground marker | Unparryable (grab, slam, barrage) | Dodge or leave the marker |
| Yellow ground ring that fills | Area attack with a delay; fills over the telegraph time | Leave the ring, or parry if it has a white edge |
| Blue pulse on an enemy | Enemy is about to buff or heal another | Target it (tap to pin) or Special |
| Enemy outline shakes, break bar flashes | Break imminent | Keep parrying, prepare Execute |

Colour never carries meaning alone: each cue also has a distinct shape and sound, and a colour-blind mode swaps the palette (section 14).

**Health, damage and status.** Damage is attack times a skill multiplier minus flat defense, never below 1. There are four status effects and no more: Burn (damage over time), Chill (slow), Shock (chains to a nearby enemy), Bleed (increased damage taken). Health does not regenerate. Healing comes from boons, from a potion offered through the Action button when health is below 40% and nothing else is in context, and from the stage reward screen.

**Failure.** In campaign stages, death restarts the current room with full health and the boons kept; boons picked so far are not re-rolled. In trials and side dungeons, death restarts the stage. Death never costs currency, experience or items. The failure screen names the attack that killed the player and shows its telegraph, with one sentence of advice ("Red flashes cannot be parried. Swipe to dodge.").

**Initial tuning values.** These are starting points for the prototype gate (section 17), not final.

| Parameter | Initial value | Note |
| --- | --- | --- |
| Precise parry window | 200 ms from touch-down | Full parry: no damage, stagger, riposte, Special charge. Console games sit at 130 to 200 ms; touch latency earns the extra. |
| Soft parry tier | 200 to 450 ms | Late parry: half damage, no riposte, no stagger. Keeps a near miss from feeling like nothing happened. |
| Spam penalty | Second tap within 400 ms shrinks the precise window to 120 ms; a third removes it until 600 ms of no taps | Borrowed from Nine Sols; makes mashing strictly worse than reading |
| Parry recovery after a whiff | 300 ms | No second parry during recovery |
| Enemy telegraph, normal enemies | 600 to 800 ms before the hit frame | Shorter in later worlds, never under 450 ms |
| Enemy telegraph, boss fast attacks | 450 to 550 ms | Always paired with a distinct sound |
| Input buffer | 100 ms | A tap slightly before the window still counts |
| Dodge duration / invulnerable | 250 ms / 180 ms | Starts on the first frame |
| Dodge cooldown | 800 ms | Second charge unlocked in world 3 |
| Riposte window after a parry | 1.5 s | Auto-attacks deal 2x (Blade 3x) |
| Stagger on parried normal enemy | 1.0 s | Elites 0.6 s, bosses build break instead |
| Broken state duration | 3.0 s | Execute available throughout |
| Hit stop on parry | 80 ms | Plus haptic pulse and screen flash |
| Assist: wider windows | Precise 280 ms, soft to 550 ms | Mirrors Clair Obscur's 40% story-mode widening |

The numbers above are anchored to the research in section 2 where it gives measured values from shipped games, and otherwise to the prototype's first playtest.
