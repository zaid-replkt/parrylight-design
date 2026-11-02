<!-- from md/04-build-spec-C-screens-and-copy.md -->

## C4. System strings

**Failure advice** (`adv.<attack_type>`; one line, chosen by the attack that killed the player; the replay highlights the same attack)

| Attack type | Copy |
| --- | --- |
| white\_melee | White flash means tap. Try parrying a beat earlier. |
| white\_melee\_late (killing hit landed inside the soft tier) | Close. Tap a little earlier for a full parry. |
| red | Red cannot be parried. Swipe to dodge, or step away. |
| projectile | Projectiles can be parried. Tap as they arrive. |
| ring | Leave the ring before it fills, or parry its white edge. |
| blink\_strike | It blinks first, then strikes. Parry the strike, not the blink. |
| burrow | A yellow marker on you means move. |
| hazard\_tide | The tide pushes. Face the band and parry from inside it. |
| hazard\_pool | Standing in a pool hurts. Fight beside it. |
| hazard\_conveyor | The floor moves you. Walk against it before you parry. |
| hazard\_burn | The burn line crosses on a timer. Cross it after it passes. |
| hazard\_chill | Chill floor slows your dodge. Parry here, dodge elsewhere. |
| hazard\_wind | Wind bends arrows. Reflect them with the wind, not against it. |
| buffed (killed by a buffed enemy) | Blue pulse means a buff. Target the one pulsing. |
| volatile | It explodes on death. Step back before the last hit. |
| boss\_phase | New phase, new pattern. Watch two attacks before you commit. |

**Reward and progress copy** (`ui.*`)

| Id | Copy |
| --- | --- |
| ui.results.cleared | Stage cleared |
| ui.results.first\_clear | First clear |
| ui.results.repeat | Repeat clear: 20% rewards |
| ui.results.star | Mastery star earned |
| ui.results.unlock\_family | New weapon family: {family} |
| ui.results.unlock\_class | New class: {class} |
| ui.results.world\_cleared | {world} cleared. {next\_world} is open. |
| ui.results.next\_stage | Next stage |
| ui.map.continue | Continue, room {n} |
| ui.quests.claim\_all | Claim all |
| ui.quests.daily\_reset | New quests in {h}h {m}m |
| ui.calendar.claim | Claim day {n} |
| ui.streak.forgiven | A missed day was forgiven. Streak kept. |
| ui.streak.reset | The streak reset. Day 1 again. |
| ui.return.title | Welcome back |
| ui.return.body | Here is what changed while you were away, and a crate to catch up. |
| ui.season.tier | Tier {n} reached |
| ui.forge.short | Need {n} more {material} |
| ui.forge.reroll\_confirm | Re-roll {affix} for 3 shards? The other affixes stay. |
| ui.hero.respec\_cost | Respec: {cost} |
| ui.trial.no\_assist | Trials run without assists |
| ui.pause.quit\_body | Leave the stage? Progress in this room is lost. |
| ui.cloud.conflict | Two saves found. Which one do you want to keep? |

**Combat callouts** (`cb.*`; 400 ms, 24 pt): cb.perfect Perfect · cb.reflect Reflected · cb.break Break · cb.execute Execute · cb.last\_stand Last Stand · cb.second\_wind Second Wind · cb.phase Phase {n} · cb.boon {boon name} (banner, not callout).

**Notifications** (`push.*`; at most one per day; only after three days played and opt-in)

| Id | Copy | Sent when |
| --- | --- | --- |
| push.calendar | Day {n} reward is ready. | the daily claim is available and the player has not opened the app by 18:00 local |
| push.weekly | A new weekly challenge stage is up: {name}. | weekly rotation, Monday 10:00 local |
| push.event | {event} has started. New stages and rewards until {date}. | event start |
| push.return | Your catch-up crate is waiting. | day 3 of absence, once |

Every notification deep-links to the screen it names and carries a "Stop these" action that turns the category off.
