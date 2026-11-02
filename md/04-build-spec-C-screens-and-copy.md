# Build spec C: screens and copy

Screen-by-screen specification for the UI engineer and the artist, with the strings the game ships with.

## C1. Screen inventory

Fourteen screens, five behind the tab bar and nine modal or in-stage. Positions are on the 390 x 844 pt reference phone, measured from the top-left inside the safe area; everything anchors by percentage and scales by width. Every screen lists its elements with ids (for analytics and strings), its states, and where each tap goes.

**Shell: tab bar** (`ui.tabs`): height 56 pt plus bottom inset; five tabs Map, Hero, Forge, Quests, Shop with 24 pt icons and 11 pt labels; a red badge dot on Quests when anything is claimable and on Shop only during a new event. The tab bar is hidden in combat and on full-screen modals.

| Screen | Elements (id: position, size) | States | Taps go to |
| --- | --- | --- | --- |
| Splash (`ui.splash`) | logo centred; `begin` button 0 to 390 x 740 to 796 (full width, 56 pt) on first launch only | first launch; returning (auto-advances after 0.8 s) | Begin: stage 1-1 directly (no Map on first launch) |
| Map (`ui.map`) | vertical scroll of 8 world columns; stage nodes 44 pt, 72 pt apart; current stage centred on open with a pulsing ring; `play_next` button 16 to 374 x 700 to 756; currency strip top (coins, gems, materials of the current world); `continue` replaces `play_next` when a stage is in progress | locked world (greyed, lock icon with the boss name); cleared (filled node, stars 0 to 3 under it); current; in progress | node: Stage preview; play\_next: Stage preview of the next uncleared stage; world header: world summary sheet (families, rule, stars, dungeons, trials) |
| Stage preview (`ui.preview`) | sheet from the bottom, 70% height: stage name and number, enemy family icons, rule icon with one line, rewards row, best time and deaths, 3 mastery rows with checkmarks, `loadout` chip (weapon, armour, rings, class icons) at 16 x 560, `start` button 16 to 374 x 620 to 676 | first visit (rewards show first-clear extra); cleared; in progress (`start` reads Continue, room number shown) | loadout chip: Loadout sheet over the preview; start: Combat |
| Loadout sheet (`ui.loadout`) | class selector (3 cards, 110 pt wide); weapon, armour, ring 1, ring 2 slots 72 pt; tapping a slot opens a vertical list filtered to that slot with stat deltas in green or red; `confirm` 16 to 374 x 740 to 796 | locked class cards show the unlock condition | confirm: back to the preview with the chip updated |
| Combat (`ui.combat`) | C2 | C2 |  |
| Boon pick (`ui.boon`) | dim overlay; 3 cards stacked vertically 16 to 374, each 150 pt tall, 12 pt apart, starting at y 160: icon 44 pt, name 17 pt, effect 15 pt, stack marker right; `skip` text button at bottom (keeps nothing, +20 Special) | first tap enlarges the card to 200 pt and shows the full text; second tap confirms | card: confirm; skip: resume |
| Results (`ui.results`) | title (stage name, Cleared); reward row animates in: coins, XP bar fill, materials, shards; stars earned row with the objectives' text; unlock card full width when an unlock exists; `next_stage` 16 to 374 x 680 to 736 (primary); `replay` and `map` as 44 pt text buttons under it | first clear (extra shown); repeat (20% label on XP); world cleared (boss) adds the world-complete banner and leads to the next world's intro | next\_stage: Stage preview of the next stage with a 1.5 s auto-start countdown that any tap cancels |
| Failure (`ui.failure`) | the last 2 s replayed in a 300 x 170 window at y 120 with the killing attack's telegraph highlighted; attack name; one advice line (C4); `retry` 16 to 374 x 620 to 676 (primary, reads Retry room or Retry stage); `change_loadout` text button; `map` text button | campaign (room retry); dungeon and trial (stage retry); assist suggestion line after 3 deaths in one stage ("Assist options are in Settings", tap opens them) | retry: Combat at the room start |
| Pause (`ui.pause`) | resume (primary), restart room, settings, quit to map (confirm dialog); current boons listed with icons; objectives with progress |  |  |
| Hero (`ui.hero`) | character portrait with equipped skin 0 to 390 x 0 to 260; level and XP bar; stats list (health, attack, defense, crit, Special rate); class tabs; skill tree as three vertical columns of five nodes, 56 pt nodes; `spend` on a node when a point is unspent; respec button with cost | nodes: locked, available, taken | node: confirm dialog with the effect text |
| Forge (`ui.forge`) | inventory grid 4 wide, 80 pt cells, grouped by slot with headers; item detail sheet: name, rarity colour, level, stats, trait or rule, `upgrade` (cost line: coins and materials with have/need), `equip`, `dismantle`, for rings `reroll` per affix and `refine`; craft tab with family cards and a cost line; transmute tab | insufficient funds greys the button and shows the shortfall |  |
| Quests (`ui.quests`) | segments: Daily, Weekly, Achievements, Season, Event; claimable items first with a `claim_all` button at the top; each quest row: icon, text, progress bar, reward chips; calendar strip at the top of Daily (7 day cells, today highlighted) |  | claim: reward animation inline |
| Shop (`ui.shop`) | sections: Season pass (one card), Cosmetics (grid), Gems, Bundles; each item card shows gem or money price and a Cosmetic tag; purchase confirm dialog with the platform sheet | starter bundle appears once, after 1-8, as the first card, and is gone after dismissal plus 24 hours or purchase |  |
| Settings (`ui.settings`) | C5 list |  |  |
| World intro (`ui.world_intro`) | full-screen art, world name, one line, the new family and rule icons with one line each, `continue` | shown once per world | continue: Map centred on stage 1 |

**Transitions**: screens slide vertically (sheets up, full screens cross-fade 200 ms); Combat loads behind the Stage preview so Start is instant; Results fades in over the frozen last frame of combat. No screen shows a spinner; loading states keep the previous screen visible with a thin progress line under the HUD strip.

**Dialogs**: `confirm_quit` ("Leave the stage? Progress in this room is lost." Stay primary, Leave muted), `confirm_respec`, `confirm_dismantle` (lists what comes back), `confirm_purchase`, `cloud_conflict` (two cards with dates and playtime, choose one), `notifications_prompt` (shown once, after the third day played, from the Quests tab, never on launch).

## C2. Combat HUD and Action button states

**HUD elements** (`ui.combat.*`; positions on the reference phone, y measured from the top safe-area inset)

| Id | Element | Position and size | States |
| --- | --- | --- | --- |
| hud.health | Health bar | x 16 to 196, y 16, 10 pt tall, rounded | full; damaged (white flash 120 ms on hit); low (under 40%: amber, slow pulse); healing (green fill animation) |
| hud.special | Special meter | x 16 to 136, y 32, 5 pt tall | filling; full (gold pulse, the Special button glows); Overcharge (extends to 150 with a second colour) |
| hud.rooms | Room dots | centred, y 24; 8 pt dots 12 pt apart; boss room a diamond | pending; current (ring); cleared (filled); boon room (small plus) |
| hud.pause | Pause button | right, 44 x 44 at x 330, y 8 | enabled; disabled during Execute cinematic |
| hud.target | Target bar | floats 12 pt above an elite or boss, 120 pt wide: health bar with break bar under it | hidden; shown; break filling; broken (bar flashes, timer ring 3 s) |
| hud.edge\_top | Spawn and threat indicators | 8 pt under the HUD strip | arrow for a spawn 1 s before; telegraph colour chip for an off-screen windup |
| hud.edge\_band | Threat band indicators | 16 pt above the band line at 78% height | same chips for telegraphs originating under the thumbs |
| hud.banner | Boon banner | slides down to y 56, 1.2 s | one at a time, queued |
| hud.callout | Combat callouts | centred at 45% height, 24 pt, 400 ms | Perfect, Reflected, Break, Execute, Last Stand; one at a time; off in reduced-motion mode except Break and Execute |
| hud.joystick | Floating joystick | appears under the left thumb: 68 pt ring, 28 pt knob | hidden; active |
| hud.special\_btn | Special button | 72 pt circle, centre at x 342, y 780 | charging (ring fills); ready (glow); locked (trial) |
| hud.action\_btn | Action button | 60 pt circle, centre at x 342, y 700 | below |
| hud.dodge\_btn | Dodge button (setting) | 56 pt circle, centre at x 342, y 630 | ready; cooldown (ring) |

**Action button states** (one at a time; icon plus one-word label under it)

| State | Icon and label | Colour | Enabled when | Tap |
| --- | --- | --- | --- | --- |
| hidden | none (position reserved) |  |  | nothing |
| execute | blade over a cracked ring, "Execute" | accent gold, distinct pulse and sound | 200 ms after shown, while a broken enemy is within 1.5 units | Execute (A2) |
| open | chest, "Open" | neutral | chest within 1.5 units | opens; rewards fly to the HUD |
| pull | lever, "Pull" | neutral | lever within 1.5 units | triggers the room object |
| pray | shrine, "Pray" | neutral | shrine within 1.5 units | heals 20% and ends the shrine |
| pick | relic, "Take" | neutral | relic within 1.5 units | collects |
| trade | merchant, "Trade" | neutral | merchant within 1.5 units | opens the merchant sheet (potions for coins, one ring re-roll) |
| drink | potion, "Drink" with the count | neutral, amber ring | health under 40%, potions above 0, no other context | Drink (0.6 s) |
| arming | the new state's icon at 60% opacity |  | the 200 ms arm delay | nothing |

The button never shows two options; when two contexts apply the resolver in A5 picks one, and the dropped context reappears when the first one ends. In trials where potions are disabled, the drink state never appears.

## C3. Tutorial scripts

Tutorial steps are data (`tutorial.steps[]`): a trigger, an optional slow-motion, a callout string, a highlight target, and a completion condition. Each step runs once, records into `save.tutorial.steps_done`, and never repeats. All copy below is final launch copy; one line each, under 60 characters, no exclamation marks.

| Step id | Stage and trigger | Slow-mo | Highlight | Copy (string id) | Completes when |
| --- | --- | --- | --- | --- | --- |
| move | 1-1 R1 start | no | left half shimmer | `tut.move`: Drag on the left to move | joystick held 1 s |
| parry | 1-1 R2, first white flash | 30% for up to 2 s | the enemy's outline, a tap ripple on the right half | `tut.parry`: White flash. Tap the right side now | first precise or soft parry |
| parry\_ok | after the first precise parry | no | none | `tut.parry_ok`: Parried. Your next hits strike harder | 1.5 s |
| riposte | 1-1 R3, first riposte hit lands | no | damage pop shown once | `tut.riposte`: Riposte. Parry first, then let the blade work | 1.5 s |
| dodge | 1-2 R1, first red flash | 30% for up to 2 s | the enemy's red outline, a swipe arrow on the right half | `tut.dodge`: Red cannot be parried. Swipe to dodge | first dodge during a red |
| dodge\_ok | after the first successful dodge | no | none | `tut.dodge_ok`: Dodged. Red means swipe | 1.5 s |
| special | 1-3 R1, meter reaches 100 | no | Special button pulse | `tut.special`: The Special is ready. Tap it | Special cast |
| boon | 1-3 after R1, boon pick opens | paused | the three cards | `tut.boon`: Pick one. It lasts until the stage ends | a card confirmed |
| action\_open | 1-4 R2, chest in range | paused 1.5 s | Action button | `tut.action`: This button changes with what is near you | chest opened |
| potion | 1-4 R3, health drops under 40% (scripted hit if needed) | paused 1.5 s | Action button (Drink) | `tut.potion`: Low health. The button offers a potion | potion drunk or room cleared |
| results | 1-1 Results screen | no | Next stage button | `tut.results`: Rewards are yours. Next stage is one tap | tap |
| home | after 1-4, first Map visit | no | calendar and quest badge | `tut.home`: Daily rewards and quests live here | tap anywhere |
| edges | 1-5 R1, first bottom spawn marker | no | the bottom edge marker | `tut.edges`: Enemies also come from below. Watch the edge | 1.5 s |
| reflect | 1-9 R1, first seed in flight | 30% for up to 1.5 s | the seed, tap ripple | `tut.reflect`: Parry the seed to send it back | first reflection |
| pin | 1-10 R1 start | no | the Seedspitters | `tut.pin`: Hold on an enemy to make it the target | first pin or room cleared |
| elite | 1-12 R3, Brute appears | no | the break bar | `tut.break`: Parries fill the break bar. Full means Execute | first break |
| execute | first broken enemy | paused 1.5 s | Action button (Execute) | `tut.execute`: Execute now | Execute |
| burrow | 1-19 R3, first yellow marker | 30% for up to 1.5 s | the marker | `tut.burrow`: A yellow marker on you means move | marker resolves |
| forge | after 1-6 (first armour), Map visit | no | Forge tab | `tut.forge`: Equip the armour you found in the Forge | Forge opened |
| hero | first skill point (level 2) | no | Hero tab | `tut.hero`: A skill point is waiting | Hero opened |

Slow-motion applies to the simulation clock, not to input timestamps, so the parry window is judged in real time and the tutorial parry is easier only because the telegraph is longer. After `parry` and `dodge` complete, no tutorial step ever pauses combat again except `action_open`, `potion` and `execute`, each once.

**Hints after failures** (not tutorial steps; shown on the Failure screen, C4) are selected by the killing attack's type, and after three deaths in one stage the line `tut.assist`: Assist options are in Settings. They never cost rewards. is appended.

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

## C5. Settings

| Group | Setting (key) | Options | Default |
| --- | --- | --- | --- |
| Controls | Left-handed (`left_handed`) | off, on | off |
| Controls | Dodge button (`dodge_button`) | off, on | off |
| Controls | Joystick size (`joystick_size`) | small, medium, large | medium |
| Controls | Tap to pin (`pin_enabled`) | off, on | on |
| Assist | Wider parry window (`assist_parry`) | off, on | off |
| Assist | Slower telegraphs (`assist_telegraph`) | off, on | off |
| Assist | Hold to guard (`hold_guard`) | off, on | off |
| Assist | Damage resistance (`assist_resist`) | off, 20%, 40% | off |
| Display | Colour mode (`colour_mode`) | default, deuteranopia, protanopia, tritanopia | default |
| Display | Damage numbers (`damage_numbers`) | off, on | off |
| Display | Reduced motion (`reduced_motion`) | off, on | off (follows the OS setting on first launch) |
| Display | Screen shake (`shake`) | off, on | on |
| Display | Frame rate (`fps_target`) | 30, 60, auto | auto |
| Display | Text size (`text_scale`) | 100%, 115%, 130% | follows the OS |
| Audio | Music (`music`) | 0 to 100 | 80 |
| Audio | Effects (`sfx`) | 0 to 100 | 100 |
| Audio | Haptics (`haptics`) | off, on | on where supported |
| Audio | Telegraph sounds (`telegraph_audio`) | off, on | on |
| Notifications | Daily reward (`push_calendar`) | off, on | off |
| Notifications | Weekly and events (`push_events`) | off, on | off |
| Account | Cloud save (`cloud_save`) | off, on | on |
| Account | Link account | button |  |
| Account | Restore purchases | button |  |
| Account | Delete local data | button, double confirm |  |
| About | Version, licences, privacy policy, support link |  |  |

Assist settings show one line: "Assists never cost rewards. Trials run without them." The `assist_resist` option follows the Hades God Mode shape in design section 2 without the per-death escalation: a fixed 20% or 40%, chosen by the player.
