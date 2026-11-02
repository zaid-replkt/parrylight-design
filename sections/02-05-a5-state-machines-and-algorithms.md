<!-- from md/02-build-spec-A-formulas-and-systems.md -->

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
