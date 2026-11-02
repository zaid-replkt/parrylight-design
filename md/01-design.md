# Game Design Document: Portrait 2D Action RPG (working title: Parrylight)

As of 2 November 2026 · author Zaid

## 1. Overview

Parrylight is a portrait-only, single-player 2D action RPG for phones where your character attacks on its own and you win by moving, parrying, dodging and choosing when to fire abilities, across 8 worlds of hand-authored stages that take about 30 hours to clear the first time. "Parrylight" is a placeholder name; everything else in this document is a build spec.

This tab is the design. The build-level detail lives in four spec tabs: Build spec A: formulas and systems (formulas, state machines, schemas), Build spec B: content tables (every boon, skill, affix, stage, boss, quest and achievement), Build spec C: screens and copy (every screen and string) and Build spec D: backlog (epics, tickets, definition of done).

**One-page summary**

| Field | Decision |
| --- | --- |
| Genre | Stage-based action RPG with roguelite-style in-run upgrades (not a roguelike: progress is never lost) |
| Platform | iOS and Android phones; tablets supported in portrait with letterboxing |
| Orientation | Portrait only, locked. No landscape mode exists. |
| Players | One. No multiplayer, no co-op, no synchronous social features at launch. |
| Core fantasy | A lone fighter who wins through timing and positioning, not through stat inflation |
| Session shape | One stage is 3 to 6 minutes; a boss stage 6 to 10 minutes; a satisfying session is 10 to 20 minutes |
| Structure | World map, 8 worlds, each world 24 stages plus a boss, plus side dungeons and trials (section 9) |
| Content target | 30 hours of first-clear content without repeating stages for resources |
| Inputs | Auto-attack; left-thumb floating joystick for movement; right-zone tap to parry, swipe to dodge; one Special button; one contextual Action button (section 5) |
| Business model | Free to download, fair monetization (section 12). Every unit of power is earnable in play. |
| Reference games | Pixel Blade (structure and progression), Brotato (auto-attack with real decisions), Archero 2 and Survivor.io (portrait presentation), The Battle Bricks (campaign pacing and reward cadence) |

**Design pillars**

1. **Automatic offense, skillful defense.** Basic attacks are automated. Parry, dodge, positioning and ability timing are the whole game. If a stage can be won by standing still, the stage is wrong.
2. **Every stage is a new problem.** Each stage introduces or recombines an enemy behaviour, a hazard or a rule. Difficulty comes from new decisions, never only from larger health bars.
3. **Depth you can feel in ten seconds.** A parry must look, sound and feel decisive on first contact. Progression systems can be deep, but the combat read is instant.
4. **Portrait is the design, not a port.** Arenas are taller than wide, enemies approach along the vertical axis, HUD lives in the thumb zones, and the camera never asks the player to look where a thumb is.

**Hard constraints (from the brief)**

- Portrait only. No landscape layout, no rotation.
- Fully playable solo. No content is balanced for or gated behind other players.
- Minimum 30 hours of meaningful first-clear content. Grinding, daily chores and repeated stages do not count toward this.
- Level, wave and world based. No open world, no sandbox, no creativity-driven loop.
- No pop-culture IP, no meme characters, no borrowed brands. Original name, art, characters, audio and level content.
- The Roblox-style engagement layer (tutorial, daily rewards, streaks, quests, achievements, events, return rewards) ships at launch, as specified in section 13.
- Auto-attack with a small set of skill buttons; contextual, situation-aware UI.

**Non-goals**

- PvP, guilds, chat, leaderboards that require live opponents (asynchronous score boards are allowed later).
- Procedurally generated campaign stages. Stages are authored from data templates; randomness lives only in optional challenge modes.
- Gacha for units or power. Cosmetics only.
- Landscape, controller, or desktop support at launch.

## 2. Research and analysis

The research supports the concept but changes three things from the earlier discussion: the parry window must be wider than console values because of touch latency, Pixel Blade's progression should be borrowed for its structure and not its economy, and the portrait survivor-likes prove the control scheme but not the retention we want (their D30 is low and carried by gacha and energy, both of which this design excludes). Findings below are as of 2 November 2026; figures from third-party guides are marked.

**Reference games: what we take and what we leave**

| Game | What it proves | What we take | What we leave out |
| --- | --- | --- | --- |
| [Pixel Blade](https://rotrends.com/game/6161049307) (Roblox, 266M visits, 96.8% positive, 6.5 min average session) | Wave and room runs with one boss, per-world difficulty tiers, pick-1-of-3 upgrade cards between waves, rings as a rolled accessory slot, campaign solo-viable | World and difficulty structure, between-wave boon cards, the ring slot, campfire merchant as a rest beat | Duplicate-fed weapon levels, rings that cannot be rerolled, the Wishes gacha, raids that cannot be played alone, a World 4 spike with off-screen ranged attacks (guide reports, [roonby](https://roonby.com/2025/12/17/pixel-blade-world-4-guide-tips-and-tricks-to-clear-faster-and-farm-safely/)) |
| [Archero 2](https://www.levelwinner.com/archero-2-beginners-guide/) (Habby, $32.8M in 30 days per [PocketGamer.biz](https://www.pocketgamer.biz/archero-2-makes-328m-in-first-30-days-from-player-spending)) | Portrait room combat with a floating joystick works at scale; 50 waves per chapter, boss every 10 waves | Floating joystick, room-sized arenas, boss cadence, wave timer that pauses during bosses | Stop-to-shoot (ours attacks while moving), energy cap with ad refills, gear and character gacha, pay-to-win artifacts |
| [Survivor.io](https://naavik.co/deep-dives/survivorio-archeros-footsteps/) (Habby, D1 44%, D7 15%, D30 4% per data.ai via [mobilegamer.biz](https://mobilegamer.biz/two-months-in-survivor-io-passes-75m-from-37m-downloads/)) | One-finger auto-attack, confined boss arenas that guarantee telegraph visibility, pre-boss notifications | Confined boss arenas, boss warnings, a top-strip HUD with the timer and progress | 15-minute rounds (too long for our stage loop), gacha equipment, energy |
| [Brotato](https://brotato.wiki.spellsandguns.com/Waves) | Auto-aim and auto-fire with movement-only input still carries real decisions, because the decisions live between waves | Decision density between rooms, a small number of options at any moment, i-frames scaled by hit size (0.2 to 0.4 s) | 20-wave 17-minute runs; run-level permadeath |
| The Counter of Death, One Finger Death Punch 2 ([Gamesradar](https://www.gamesradar.com/a-delightfully-retro-deflectathon-you-should-be-playing-the-counter-of-death), [PocketGamer](https://www.pocketgamer.com/one-finger-death-punch-2/app-army-assemble-one-finger-death-punch-2-does-this-arcade-fighter-maintain-its)) | Tap-to-counter is a proven mobile core input; both use oversized hit zones and punish spamming | Oversized defense zone, spam penalty, rhythm-paced telegraphs | No published timing windows exist for any mobile parry game, so ours are set by prototype |
| [The Battle Bricks](https://www.roblox.com/) (from the earlier analysis) | Chapter, stage and daily-reward cadence that a solo player follows for weeks | Seven-day reward calendar, chapter milestones, challenge stages | Horizontal battlefield (wrong for portrait) |

**Parry timing anchors.** Shipped action games cluster their precise window at 130 to 200 ms with a lenient tier around 500 ms and a penalty for spamming: Nine Sols uses 133 ms precise, 133 to 500 ms imprecise, and shrinks the window on rapid repeat presses ([wiki](https://ninesols.wiki.gg/wiki/Parry)); Sekiro's deflect is about 30 frames and shrinks after repeated guards ([Fextralife](https://sekiroshadowsdietwice.wiki.fextralife.com/Deflection)); Dead Cells auto-parries hits in the first 0.2 s of a shield hold and locks blocking for 0.6 s after a failure ([wiki](https://deadcells.wiki.gg/wiki/Shield)); Hollow Knight's parry grants 0.25 s of invulnerability ([Fextralife](https://hollowknight.wiki.fextralife.com/Combat)). Clair Obscur's story mode widened parry and dodge windows by 40% as its accessibility lever ([Automaton](https://automaton-media.com/en/news/clair-obscur-expedition-33-makes-parrying-and-dodging-easier-in-story-mode-allowing-for-a-more-traditional-turn-based-rpg-experience/)). Touch adds latency a controller does not, so section 4 starts at 200 ms precise, a 450 ms soft tier, telegraphs of 600 to 800 ms, and a spam penalty.

**Platform rules that shape the layout.** Apple's game-control guidance: frequently used controls at least 44 x 44 pt, movement on the left and a floating thumbstick where the thumb lands, press state plus sound plus haptics, hide controls that are not relevant ([HIG](https://developer.apple.com/design/human-interface-guidelines/game-controls)). Android: 30 fps minimum for the core loop, 60 recommended, a slow frame is 50 ms, a slow session is over 25% slow frames, and Play steers users away from games under 20 fps ([Android quality](https://developer.android.com/quality/technical), [slow sessions](https://developer.android.com/google/play/vitals/slow-session)); bad-behaviour thresholds are 1.09% crash rate and 0.47% ANR rate overall ([Play vitals](https://developer.android.com/google/play/vitals)). On screens of 600 dp or wider, Android 16 ignores orientation locks, so the tablet layout in section 6 is required, not optional ([form factors](https://developer.android.com/games/develop/multiplatform/make-your-game-compatible-with-all-form-factors)).

**Retention benchmarks** (what "good" means for section 16)

| Metric | Median, all mobile | Top 25% | Top 10% | RPG reference |
| --- | --- | --- | --- | --- |
| D1 | about 22% | just over 30% | about 40% | 30.5% |
| D7 | 3.4 to 3.9% | 6 to 8% | 11 to 12% | 9.9% |
| D30 | 0.7 to 0.8% | 1.6 to 1.8% |  | 3.5% |
| Session length | 3.1 to 3.5 min | about 5.2 min |  | action genre has the longest sessions |

Sources: GameAnalytics 2026 benchmarks, 16,262 mobile games ([summary](https://gamedevreports.substack.com/p/gameanalytics-mobile-and-pc-game), [PDF](https://investgame.net/wp-content/uploads/2026/01/2026-01-27-2026-mobile-pc-benchmarks_compressed.pdf)); RPG column from Mistplay via [Segwise](https://segwise.ai/blog/mobile-gaming-app-user-retention-strategies.md), year not stated; Adjust 2026 for the action-session note ([summary](https://gamedevreports.substack.com/p/adjust-gaming-app-insights-report)). Archero 1 reached D1 49%, D7 23%, D30 11% in 2022 (data.ai). No 2026 source publishes an action-roguelite split, so the targets in section 16 use the top-quartile row with an RPG uplift.

**Engagement design guidance.** Roblox's creator docs are the most explicit public source on the systems this brief asks for: get players to the fun in five minutes or less and ship smaller updates every two to four weeks ([retention](https://create.roblox.com/docs/production/analytics/retention)); dailies should be finishable in one session with modest rewards ([quest design](https://create.roblox.com/docs/production/game-design/introduction-to-quest-design)); seasons of about one month with a week of rest, about ten tiers to start, never requiring hard currency ([season pass](https://create.roblox.com/docs/production/game-design/season-pass-design)); login-streak and time-played rewards with thresholds near 10, 30 and 60 minutes ([engagement rewards](https://create.roblox.com/docs/resources/feature-packages/engagement-rewards)). Mistplay and AppsFlyer's 2025 loyalty report found engagement bonuses are the top stated reason players return (64%), events second (50%) ([summary](https://gamedevreports.substack.com/p/mistplay-and-appsflyer-player-loyalty)). AppMagic counted midcore login-calendar usage up 93% year over year in 2025 ([summary](https://gamedevreports.substack.com/p/appmagic-mobile-live-ops-in-2025)).

**Monetization evidence.** Apple (guideline 3.1.1) and Google Play both require disclosing odds before purchase for any paid randomized item ([Apple](https://www.fenwick.com/insights/publications/apple-now-requires-disclosure-of-loot-box-odds), [Google](https://fenwick.com/insights/publications/google-play-now-requires-disclosure-of-loot-box-odds)); this design has none. Brawl Stars removed loot boxes in late 2022, lost about 14% of revenue over five months, then rebuilt around earned drops and an IAP-only pass and reported 8.8x revenue by February 2024 ([Deconstructor of Fun](https://www.deconstructoroffun.com/blog/why-removing-loot-boxes-in-brawlstars-failed), [mobilegamer.biz](https://mobilegamer.biz/supercell-explains-brawl-stars-big-comeback-from-an-all-time-low-to-8-8x-revenue/)). Battle passes in the market sit at roughly $5 to $15 per 4-to-8-week season (aggregator figures, directional only, [source](https://www.shanethegamer.com/research/battle-pass-statistics/)).

**Accessibility precedent.** Hades' God Mode adds 20% damage resistance, rising 2% per death to a cap of 80%, and can be toggled at any time ([Supergiant via Can I Play That](https://caniplaythat.com/2021/08/11/hades-god-mode-explained-by-supergiant-games)); Celeste's assist mode includes a game-speed slider down to half ([New Normative](https://newnormative.com/2018/01/25/celestes-assist-mode-brings-welcome-accessibility-options)); Xbox guideline 103 requires that cues never rely on colour alone ([XAG 103](https://learn.microsoft.com/en-gb/gaming/accessibility/xbox-accessibility-guidelines/103)). Section 5's assist options follow these.

**Engines.** Unity 6 is free below $200k revenue and Pro is $2,310 per seat per year from January 2026 ([Unity](https://unity.com/pricing-updates)); Godot 4.5 and 4.6 now ship foundation-maintained Google Play Billing, Play Games and StoreKit 2 plugins ([Godot mobile update](https://godotengine.org/article/godot-mobile-update-apr-2026/)) with larger Android builds reported by users; Defold is free with sub-2 MB bundles and an official IAP extension but fragmented haptics ([extension-iap](https://github.com/defold/extension-iap)). The choice is made in section 15 and depends on one open question: whether this ships as a standalone app or inside Playabl's own runtime.

## 3. Core loops

The game is four nested loops, and the inner two are where the skill lives. Everything in the outer loops exists to send the player back into the inner ones with a new reason.

**Moment to moment (1 to 3 seconds).** Read a telegraph, decide: parry it, dodge it, or ignore it and reposition. A successful parry opens a punish window; the auto-attack fills it. Failure costs health, never progress.

**Room (20 to 60 seconds).** A room is one wave or a small set of waves with a fixed enemy mix and a hazard rule. Rooms end when the last enemy dies. Between rooms the player picks one of three boons (temporary in-stage upgrades that expire when the stage ends).

**Stage (3 to 6 minutes, bosses 6 to 10).** Three to five rooms, then a final wave or a boss. Stages are authored; the order of rooms is fixed, so the player can learn and plan. Clearing a stage pays experience, currency, and at milestones an equipment or skill unlock.

![stage loop · 6 steps, one permanent return](images/03-stage-loop.png)

Each stage ends in rewards and a permanent upgrade step, so the next stage is entered stronger and with a new problem.

**Session (10 to 20 minutes).** The home screen shows the next stage, any claimable reward and any quest that is one stage from completion, in that order. A session is two to four stages. Everything saves on stage completion and on room completion, so a phone call costs at most the current room.

**Meta (hours to weeks).** Worlds unlock in order, each with a new enemy family, a new mechanic, a boss, and side dungeons and trials that remix the world's rules. Character progression (section 8) and the engagement layer (section 13) sit on top of this and are never a substitute for it.

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

## 5. Controls and input

The phone is held in one or two hands in portrait, and the whole control scheme fits under two thumbs: the left thumb moves, the right thumb defends, and two fixed buttons in the bottom-right corner carry the Special and the one contextual Action. Nothing else is ever on screen during combat.

**Zones** (measured on a 390 x 844 pt phone; everything scales by percentage, section 6)

| Zone | Where | Input | Result |
| --- | --- | --- | --- |
| Movement | Left half of the screen, lower 65% | Touch and drag | Floating joystick appears under the thumb; direction and magnitude set movement. Lifting the thumb stops. |
| Defense | Everything not in the movement zone and not a button, including the whole upper play area | Tap | Parry (fires on touch-down for lowest latency) |
| Defense | Same | Swipe (12 pt of movement within 60 ms) | Dodge in the swipe direction; the parry started on touch-down is cancelled, except its first frames, which stay active |
| Defense | Same | Long press (350 ms) on an enemy | Pins that enemy as the auto-attack target for 5 s |
| Special | Fixed button, bottom-right corner, 72 pt | Tap | Fires the weapon Special when the meter is full; otherwise shows the charge |
| Action | Fixed button above Special, 60 pt | Tap | Performs the current contextual action (below); hidden content keeps its position |
| Pause | Top-right, inside the safe area, 44 pt | Tap | Pause menu; game pauses instantly, also on app background |

The left-handed setting mirrors all zones and buttons. A "dedicated dodge button" setting adds a third fixed button for players who dislike swiping; it is off by default to keep the screen clean.

**Why not "tap anywhere parries".** The left thumb is on the joystick for most of every fight, and a joystick touch-down must not parry. Splitting the screen gives the right thumb the entire remaining surface, which is as close to "anywhere" as the design allows without false parries.

**The contextual Action button.** One slot, one fixed position, one action at a time, chosen by priority:

1. Execute: a broken elite or boss is within reach.
2. Interact: a chest, lever, shrine or relic is within 1.5 character widths. The nearest wins.
3. Potion: health is below 40% and the player holds at least one potion.
4. Empty: the button is hidden, the position is reserved.

Rules that keep it trustworthy:

- The action and its icon never change while a touch is held on the button.
- A newly shown or changed action is not tappable for 200 ms and pulses once, so the player cannot tap an old action and get a new one.
- Execute uses a distinct colour, shape and sound; nothing else on the button looks like it.
- The label is written under the icon in one word (Execute, Open, Pull, Drink, Pray).
- In the tutorial, the first appearance of each action pauses the game for 1.5 s with a callout.

**Latency budget.** Touch-down to visible parry frame under 50 ms on the game thread, under 80 ms input-to-photon on a 60 Hz device. The parry fires on touch-down, not touch-up, which halves the perceived delay compared with tap-gesture recognition. Haptics fire in the same frame as the visual.

**Out-of-combat input.** Menus use standard taps and vertical scrolling only; no horizontal carousels (hard to reach one-handed and easy to mistake for a swipe). Minimum tap target 44 x 44 pt everywhere, with primary buttons at 56 pt or larger and placed in the lower half of the screen.

**Assist options** (settings, no gameplay penalty, no achievement lockout)

- Wider parry window: precise 200 ms becomes 280 ms, soft tier extends to 550 ms.
- Slower telegraphs: all telegraph times plus 20%.
- Hold to parry: holding the defense zone keeps a weaker guard up (50% damage reduction, no riposte) for players who cannot time taps.
- Colour-blind telegraph palettes (section 14).
- Reduced screen shake and flash.

## 6. Camera and portrait presentation

The camera is width-locked at 9 world units, follows the character vertically with a lead toward the enemies, and arenas are tall rectangles, so a narrow screen shows a full fight without zooming out. Taller phones see more of the arena above and below; nothing is ever cropped horizontally.

![portrait screen layout · 390 x 844 pt reference phone](images/06-portrait-layout.png)

The thumbs own the lower third, the HUD sits in the top safe area, and the character is held above the thumb band so the fight is never under a hand.

**Camera rules**

| Rule | Specification |
| --- | --- |
| Projection | 2D orthographic, width-locked: exactly 9 world units are visible horizontally on every phone |
| Visible height | 16 units at 9:16, about 19.5 units at 9:19.5, 21 at 9:21. Arenas are authored for 16 and decorated beyond it. |
| Tablets and foldables (3:4, near 1:1) | Width grows to 12 units with the arena's decorative margin visible; UI stays at phone proportions, centred, with themed side panels. No landscape. |
| Follow | Damped follow, 150 ms smoothing. Vertical follow is free; horizontal follow is clamped to the arena so the walls never show gaps. |
| Character anchor | The character is held at 45% of screen height (measured from the top), above the control band, and drifts up to 15% toward the enemy centroid. |
| Lead | Camera leads 1.5 units toward the centroid of enemies that are winding up an attack, so telegraphs are on screen before the hit. |
| Threat band | The lower 22% of the screen sits under the thumbs. Any telegraph that originates there is mirrored as an edge indicator drawn just above the band. Arenas are designed so most threats come from above. |
| Hit stop | On parry the camera freezes for 80 ms with the world. No shake during hit stop. |
| Shake | Capped at 0.2 units, 120 ms, only on Executes, boss slams and the player's death. Off in reduced-motion mode. |
| Zoom | None during combat. A 10% zoom-in over 400 ms on Execute, released over 600 ms. Boss intro uses a 1.5 s pull-out from the boss to the arena. |

**Arenas for a vertical screen**

- Arena footprint is 9 wide by 20 to 28 tall. Width never exceeds 9, so the whole horizontal extent is always visible.
- Enemies spawn at the top and bottom edges, each spawn announced by a marker on that edge 1 second ahead. Side spawns do not exist.
- Hazards (pits, fire lines, pushers) are horizontal bands, because a horizontal band is read at a glance on a tall screen and a vertical one hides behind the character.
- Bosses are placed at the top of the arena and the camera's lead keeps both the boss and the character in frame; boss arenas are 9 by 16 so the fight needs no vertical scroll.
- Projectiles travel mostly vertically; diagonal shots are slow enough to read.

**Scale.** One world unit is one ninth of the screen width (43 pt on the reference phone). The character is 1.2 units tall; normal enemies 1 to 1.6 units; elites 2; bosses 3 to 4. Art is authored at 2x and 3x for a 1-unit grid, so sprites never scale non-integer on the reference phone.

**Safe areas.** The HUD strip starts 8 pt below the top safe area (Dynamic Island and notches), and no button sits within the bottom 34 pt home-indicator area. Both values come from the OS at runtime, never hard-coded.

**Portrait-specific readability checks** (run on every stage before it ships)

- Every telegraph that can hit the character is fully on screen at the moment it starts, on a 9:16 device.
- No enemy attack originates from inside the threat band without an edge indicator.
- Text in the play area is never smaller than 14 pt on the reference phone.
- A playtester holding the phone one-handed (right thumb only, movement by tilting is not supported) can clear world 1 stages, since world 1 is designed to need little movement.

## 7. UI and UX

The interface is a vertical stack of five screens behind a bottom tab bar, with one rule across all of them: the thing the player most likely wants next is a single tap away and sits in the lower half of the screen. In combat the HUD is four elements and nothing else.

**Combat HUD** (section 6 drawing)

| Element | Where | Behaviour |
| --- | --- | --- |
| Health bar | Top strip, left | Drains with hit flash; turns amber under 40% (the moment the Action button may offer a potion); numeric value on long press only |
| Special charge | Under the health bar, thin | Fills from parries and hits; pulses gold at full; the Special button mirrors it |
| Room dots | Top strip, centre | One dot per room in the stage; the boss room is a diamond; filled as cleared |
| Pause | Top strip, right, 44 pt | Opens pause; the game also pauses on app background, incoming call, or control-centre swipe |
| Target health and break | Floating above the pinned or attacking elite or boss | Only for elites and bosses; normal enemies show a small bar on hit for 1 s |
| Boon banner | Slides down from the HUD for 1.2 s | Names the boon just taken; never blocks the play area longer |
| Edge indicators | Just above the thumb band and at the top edge | Show spawns and telegraphs that originate off-screen or under the thumbs |

No damage numbers by default (they fight the telegraph read on a narrow screen); a setting turns them on, small and short-lived.

**Screen map**

| Tab | Screen | Purpose | Primary action (bottom half) |
| --- | --- | --- | --- |
| Map | World map | Vertical scroll of worlds, each a column of stage nodes; the current stage is centred on open | Play next stage |
| Map | Stage preview | Enemy families present, hazard rule, rewards, best clear, mastery objectives | Start |
| Map | Loadout sheet (slides up over preview) | Weapon, armour, two rings, class; swap without leaving the preview | Confirm |
| Hero | Character | Level, stats, class skills, mastery progress | Spend skill point |
| Forge | Inventory and upgrades | Equipment grid, upgrade, dismantle, ring refine | Upgrade |
| Quests | Daily, weekly, achievements, event track | Claimable items first, then in-progress sorted by closeness to done | Claim all |
| Shop | Currencies, cosmetics, passes | Clear labels of what is cosmetic and what is not | Buy |

**In-stage screens**

- Boon pick: three cards in a vertical column, each with icon, name, one line, and a small "stacks: 2/5" marker. The game is paused. Tap a card, then tap again to confirm (first tap enlarges it and shows the full text).
- Results: rewards fly into the currency counters, then experience fills the level bar, then any unlock is shown alone on a full card. Buttons: Next stage (primary, large), Replay, Map. The whole screen can be skipped with one tap after 0.8 s.
- Failure: the killing attack is replayed as a 2 s loop in a small window with its telegraph highlighted, one line of advice, then Retry room (primary) and Change loadout. No ad, no revive offer on the first failure of a stage.

**Flows that matter**

1. Cold start to first fight: splash, no account prompt, tap once on "Begin", straight into stage 1-1 with the tutorial overlays (section 13). Target under 30 seconds from app icon to first parry.
2. Returning session: app opens on the Map with the next stage centred, a single badge on Quests if something is claimable, and a reward popup only if a daily reward is waiting. No more than one popup per session, ever.
3. Stage to stage: Results, Next stage, 1.5 s transition. Loadout changes are offered only when the next stage introduces a new enemy family (a one-line hint, dismissable).
4. Death and retry: under 3 seconds from death to being back in the room.

**Reachability and readability rules**

- Primary buttons: 56 pt or taller, full width or bottom-right, never top of screen.
- Tab bar height 56 pt plus the bottom safe area; five tabs maximum.
- Body text 15 pt minimum, labels 13 pt minimum, numbers in a tabular figure font.
- No horizontal carousels. Lists scroll vertically; comparisons use side-by-side cards that fit one screen.
- Modal dialogs have the destructive option on the left and in muted colour; the safe option is primary.
- Every screen can be left with one tap on a persistent back or close control at the top-left, and the Android back gesture does the same.
- Loading between screens is never a spinner over black; the tab content stays visible and fades.

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

## 9. Content structure and the 30-hour budget

The campaign is 8 worlds of 25 stages (24 stages and a boss), 63 side-dungeon stages and 30 trials: 293 authored stages that take about 30 hours to clear once at average skill, with retries counted and no stage repeated for resources.

![design budget, typed from the content inventory below · first-clear hours including retries](images/09-hours-by-world.png)

Each world adds about 2.4 hours of campaign; side dungeons and trials lift the later worlds to over 4 hours each.

**Inventory and timing assumptions**

| Content | Count | Minutes per first clear (with retries) | Hours |
| --- | --- | --- | --- |
| Campaign stages | 192 | 5.5 | 17.6 |
| Campaign bosses | 8 | 12 | 1.6 |
| Side dungeon stages (3 dungeons of 3 stages per world, worlds 2 to 8) | 63 | 6.5 | 6.8 |
| Trials (6 per world, worlds 4 to 8) | 30 | 8 | 4.0 |
| Total first-clear | 293 |  | 30.0 |

Mastery objectives, boss re-fights with modifiers, daily challenge stages and events are on top of this and are not counted. The per-stage minutes are design targets; the prototype gate (section 17) measures real values on stages 1-1 to 1-8 and the budget is re-run from them.

**Worlds.** Each world introduces one enemy family and one arena rule, then spends its stages recombining them with everything before. Names and themes are original placeholders.

| World | Theme | New enemy family | Arena rule | Boss beat |
| --- | --- | --- | --- | --- |
| 1 Hollow Orchard | Overgrown farmland | Thornbacks: slow melee with long white telegraphs | None; teaches the grammar | Single break cycle, one unparryable slam |
| 2 Salt Flats | Dry seabed | Shellbacks: shielded fronts that only a parry opens | Tide bands that push horizontally | Shield phases; break opens the shell |
| 3 Lantern Marsh | Fog and still water | Wisps: short-range teleports before attacking | Shock pools that chain between enemies standing in them | Boss splits into three wisps after each break |
| 4 Clockwork Quarry | Machines and conveyors | Automata: unparryable red slams, parryable jabs | Conveyor bands that move the character | Two break cycles; conveyors reverse after the first |
| 5 Ember Vaults | Furnace halls | Stokers: buffers that empower others (blue pulse) | Burn lines that cross the arena on a timer | Boss summons stokers; kill order matters |
| 6 Frost Reliquary | Ice crypt | Sentinels: delayed area rings with white edges | Chill floors that slow dodges | Rings overlap; parry the white edges to clear space |
| 7 Sky Bastion | Floating ramparts | Archers: volleys that can be reflected by parry | Wind bands that bend projectiles | Reflection-only damage phase |
| 8 The Undercrown | Below everything | All families, recombined | Rotating rules from worlds 2 to 7 | Three phases, two break cycles each |

**Stage cadence inside a world** (24 stages)

- Stages 1 to 4: the new family alone, the new rule alone, then together.
- Stages 5 to 12: the new family mixed with one earlier family per stage; a mid-world elite at stage 12.
- Stages 13 to 20: two earlier families plus the rule; hazards at full strength; stage 20 is a gauntlet (five rooms, no boon in the last two).
- Stages 21 to 24: boss preparation, each stage rehearsing one boss mechanic in a normal fight.
- Stage 25: the boss.

Every stage must pass the "new decision" test: a designer can name the decision this stage asks that the previous one did not. If not, the stage is cut or changed.

**Side dungeons** (unlocked by mastery stars from the same world). Three stages that remix the world's rule: for example, in Salt Flats, a dungeon where every enemy is shielded and boons are parry-only. Rewards are rings and crafting materials.

**Trials** (unlocked by clearing the world's boss). Fixed-loadout and modifier fights: boss rush, no-damage rooms, Special disabled, parry-only (dodge disabled), speed clears, and a "mirror" trial where telegraph colours are swapped as a grammar test. Rewards are Legendary materials and cosmetics.

**Endgame after world 8.** Boss re-fights with stackable modifiers, mastery hunts (all stars in a world), and the rotating challenge stage from the engagement layer. This is where new content updates land (section 13).

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

## 12. Economy and monetization

The economy is tuned so that the first-clear path alone keeps a player's gear within one level of the world cap, and monetization sells cosmetics, convenience and a season pass, never power. There is no energy system, no gacha, no interstitial ads and no paid revive in the campaign.

**Currencies**

| Currency | Earned from | Spent on | Purchasable |
| --- | --- | --- | --- |
| Coins (soft) | Every stage, quests, daily reward | Weapon and armour levels, respec, potions | No |
| World materials (one type per world) | Stages and dungeons of that world | Forge crafting and upgrades for that world's tier | No |
| Shards | Dismantling equipment | Ring re-rolls (3 shards each), rare Forge recipes | No |
| Gems (hard) | Achievements, mastery stars, season track, bosses | Cosmetics, loadout slots, season pass top-up | Yes |
| Potions (consumable) | Rest rooms, daily reward, Forge (coins) | Healing in combat via the Action button; cap 3 per stage | No |

**Economy targets** (validated by the bots in section 11 and by the analytics in section 16)

- Income from a world's first-clear path funds weapon level 7 of 8 for that world's weapon and armour level 6 of 8, with no stage repeated. Level 8 comes from side dungeons and mastery.
- Ring re-roll shards from dismantling the campaign's surplus drops fund about 6 re-rolls per world.
- Coins never become the bottleneck after world 2; materials do, and materials are world-specific so earlier worlds cannot be farmed for later tiers.
- Respec is free three times, then 500 coins, flat.
- Potions cost 60 coins at the Forge, about one stage's income in world 1 and a fraction of it later, so they are a convenience and not a tax.

**Monetization**

| Offer | Price (USD, placeholder) | What it contains | Fairness rule |
| --- | --- | --- | --- |
| Season pass | 7.99 per 5-week season | Premium track: cosmetics, titles, a cosmetic weapon skin, gem refund of 60%, material bundles | Every gameplay item on the premium track also exists on the free track or in play; the pass is bought with money, never with gems alone, to keep gems from inflating |
| Cosmetic shop | 1.99 to 9.99 | Skins, parry effects, Execute cinematics, frames | No stats |
| Starter bundle | 2.99, once | Cosmetic plus 10 potions and 2,000 coins | Equivalent to about 40 minutes of play; offered once, after stage 1-8, never again |
| Supporter pack | 19.99 | Cosmetic set and a badge | Nothing else |
| Rewarded ads | Free | Double stage rewards (up to 5 per day), one daily material crate, one revive per trial (not campaign) | Opt-in only; never shown unprompted; a one-time 4.99 purchase removes the ad step and grants the rewards directly |

No interstitial ads, no ads on failure screens, no timers that money skips, no paid randomized items (so the Apple and Google odds-disclosure rules in section 2 never apply).

**What this costs us.** The research in section 2 is clear that gacha and energy drive revenue in the portrait survivor-likes, and Brawl Stars lost revenue in the months after removing loot boxes before recovering on earned drops and a pass. The bet here is the Brawl Stars shape: a smaller but more durable payer base. The pass and cosmetics are sized to make that work, and section 16 sets the conversion targets to check it.

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

## 14. Art, audio and game feel

The art direction serves one priority: a telegraph must be readable in under 200 ms on a 6-inch screen held at arm's length. Everything else (style, palette, animation budget) is decided after that constraint.

**Visual direction**

- Original hand-painted 2D with hard silhouettes, three-quarter top-down view so vertical movement reads as depth. No pixel art: pixel sprites lose silhouette at 1 unit on a phone and invite comparison with Pixel Blade.
- Three layers always in this order: ground and hazards, characters, telegraphs and UI. Telegraphs are never occluded by anything.
- Per-world palette of five colours, chosen so that white, red, yellow and blue (the telegraph colours) are absent from the environment. A world that needs red decor uses a desaturated rust that the telegraph test flags as distinct.
- Enemy families are distinguishable by silhouette alone at 1 unit: no two families share an outline; elites are the same silhouette at 1.6x with a jagged outline.
- The character faces the auto-attack target; the weapon is large enough to read which family is equipped.

**Animation rules**

- Every attack has three poses: wind-up (held for the telegraph duration with the flash on the first frame), hit (one frame, the hit frame), recovery.
- The wind-up pose must differ between parryable and unparryable attacks beyond colour: parryable attacks raise a limb, unparryable attacks lower the body.
- Parry: the character's weapon flashes, the enemy's weapon is knocked aside, 80 ms hit stop, a white ring expands from the contact point, a 6-frame screen flash at 15% opacity.
- Soft parry: the same with no hit stop and a smaller ring.
- Execute: 600 ms cinematic with a zoom (section 6) and a unique animation per boss.
- Deaths: enemies fall in under 300 ms and fade; corpses never hide telegraphs.

**Colour-blind modes.** Three palettes (deuteranopia, protanopia, tritanopia) remap the four telegraph colours; shapes and sounds already differ, so the palette swap is sufficient. Tested with a simulation filter on every family's telegraph before shipping a world.

**Audio**

| Event | Sound | Rule |
| --- | --- | --- |
| Telegraph | One sound per family, a rising tone for parryable and a falling one for unparryable | Plays at the flash; the two contours are the audio equivalent of white and red |
| Parry | Short bright metallic transient, pitch up for a perfect parry | The most satisfying sound in the game; iterated on in the prototype |
| Soft parry | Duller version, no pitch-up | Tells the player it was late |
| Dodge | Short whoosh | Confirms the i-frames started |
| Break | A crack with a 300 ms tail | Distinct from everything else |
| Execute | Stinger with a 1 s tail | Music ducks |
| Panning | Sounds from the top of the arena pan slightly up (stereo left-right is useless in portrait); top and bottom spawns use different pitches | Portrait-specific |

Music is per world, with a low-intensity loop in rooms and a high-intensity layer during elites and bosses; both loops share a tempo so telegraphs can be authored on beats for the rhythm feel the research found in mobile counter games.

**Haptics.** Perfect parry: one sharp transient. Soft parry: a light tick. Dodge: none (it would blur with the parry). Break: a double pulse. Execute: a three-pulse pattern. Taking damage: a soft thud. All haptics are a setting and off on devices without a precise actuator.

**Feel checklist** (gate for the prototype in section 17)

- A parry feels decisive with sound off and with haptics off, each tested alone.
- A first-time player describes the parry unprompted after one session.
- Enemy wind-up poses are identified as parryable or not by a tester shown a still frame, with 90% accuracy, across all families.
- No telegraph is confused with a hazard or a boon pickup in a 1-second flash test.

## 15. Technical design

The simulation runs at a fixed 60 Hz step independent of rendering, input is timestamped at touch-down so a parry is judged against when the finger landed and not when the frame drew, and all content is data loaded at runtime. If the game ships as a standalone app the default engine is Unity 6 with the 2D renderer; if it ships inside Playabl's own runtime, this section maps onto that runtime unchanged except for the engine row.

**Engine decision**

| Option | Choose it when | Trade-off |
| --- | --- | --- |
| Unity 6 (2D, URP) | Default for a standalone app; the team has Unity experience; IAP, ads, haptics and analytics plugins are mature | Pro seats at $2,310 per year once revenue passes $200k; larger builds than Defold |
| Godot 4.6 | The team prefers open source and no licence cost; foundation-maintained billing and StoreKit plugins now exist | Reported larger Android builds; smaller plugin ecosystem for ads and analytics |
| Defold | Build size is the top constraint | Lua, fragmented haptics, smaller hiring pool |
| Playabl runtime | The game is a Playabl title | The portrait, touch and data-driven rules below still apply; engine-specific rows do not |

**Architecture**

- Simulation: fixed-step 60 Hz, deterministic given the same inputs and seed. Rendering interpolates between steps. Determinism is what makes the bots in section 11 and replay of the killing blow on the failure screen possible.
- Input: the touch handler records touch-down timestamps from the OS event, not the frame; the parry check compares that timestamp with the hit frame's time. A frame drop cannot turn a good parry into a late one.
- Entities: character, enemies, projectiles and hazards are data-driven entities with behaviour state machines defined in content files; families, traits, boons, boss scripts and stages are JSON validated by schema at build time.
- Telegraph system: a single module owns telegraph timing, colour, shape, sound and haptic for every attack, so the grammar cannot drift between enemies.
- Contextual Action: a priority resolver runs each step and emits the current action; the UI shows it with the 200 ms arm delay (section 5).
- Camera: width-locked orthographic; visible height derived from the device aspect; safe areas read from the OS each frame on resize.
- UI: one canvas scaled by width, anchored to the safe-area root; all layout in percentages and points, no pixel constants.

**Save and progress**

- Autosave on room clear, stage clear, any purchase, any equipment change, and on app background. Save is a versioned JSON blob with a migration table.
- Local save is the source of truth; cloud save through Game Center and Google Play Games Services, last-write-wins with a timestamp and a conflict prompt only if both saves have progress the other lacks.
- No account required. An optional account links purchases across platforms.
- Purchases are validated server-side through the store receipt; nothing else needs a server at launch.

**Performance budgets**

| Budget | Target | Floor |
| --- | --- | --- |
| Frame rate | 60 fps on 2021 mid-range phones (iPhone 12, Pixel 6a class) | 30 fps on 2019 budget Android; never under 20 fps (Play steers users away below that) |
| Slow frames (Android vitals) | Under 5% of frames over 50 ms | Under 25% (Play's slow-session threshold) |
| Crash-free sessions | 99.7% | 99.5%, above Play's 1.09% crash and 0.47% ANR bad-behaviour thresholds |
| Input to photon | Under 80 ms on 60 Hz | Under 100 ms |
| Memory | Under 350 MB resident | Under 500 MB |
| Install size | Under 150 MB initial, worlds 5 to 8 as on-demand packs | Under 200 MB |
| Cold start to Map screen | Under 4 s | Under 6 s |
| Stage load | Under 1 s | Under 2 s |

**Portrait handling**

- Orientation locked to portrait in the manifest and plist. On Android 16 large screens, where the lock is ignored, the game renders a portrait viewport centred with themed side panels (section 6).
- Aspect ratios tested on every build: 9:16, 9:18, 9:19.5, 9:20, 9:21, 3:4, and a 1:1 foldable inner screen. A build fails if any telegraph in the test stage is off screen on any of them.
- Safe areas: top inset from the OS plus 8 pt for the HUD; bottom inset (home indicator) excluded from the button band.
- Floating joystick origin is reset when the thumb lifts; dead zone 8 pt; full deflection at 48 pt.

**Tooling**

- Stage editor: a desktop tool that edits stage JSON against the schema with a live preview on the 9:16 reference frame, runs both bots, and prints the timing and difficulty dials from section 11.
- Telegraph lint: fails a content build if any attack's telegraph is under the minimum, uses a colour outside the grammar, or lacks a sound.
- Replay capture: every death in a playtest build records the last 10 s of inputs and the seed for exact replay.

**Analytics and services.** Event schema in section 16; a privacy-conscious analytics SDK with no advertising identifiers required; crash reporting; remote config for tuning values in section 4 (parry windows, telegraph times, reward multipliers) so live balance changes need no app update. Localization: English at launch, strings externalised from day one, right-to-left layout verified for Arabic in the menus (not combat, which has no text).

## 16. Analytics and success metrics

Success is measured against the top-quartile row of the 2026 benchmarks in section 2, lifted for the genre: D1 35%, D7 10%, D30 3%, and a content-depth check that at least 15% of D30 players have passed 20 hours of active stage time. These are launch targets for the first 60 days, reviewed after soft launch.

**Targets**

| Metric | Target | Benchmark context |
| --- | --- | --- |
| D1 retention | 35% | Median 22%, top quartile about 30%, RPG reference 30.5% |
| D7 retention | 10% | Top quartile 6 to 8%, RPG reference 9.9% |
| D30 retention | 3% | Top quartile 1.6 to 1.8%, RPG reference 3.5% |
| Reach stage 1-2 | 95% of installs | Funnel, section 13 |
| Clear 1-1 first attempt | 90% | Funnel |
| Time to first parry | Under 30 s median | Funnel |
| Session length | 12 min median | All-mobile median 3.1 to 3.5 min; action genre runs long |
| Sessions per day (D7 cohort) | 2 | All-mobile median 3.8 is driven by casual |
| Active stage hours at D30 | 15% of D30 players past 20 h; median D30 player past 8 h | The 30-hour claim, checked |
| World 8 clear rate | 8% of D30 players by day 60 | Content pacing |
| Payer conversion by D30 | 2.5% | No reliable 2026 genre benchmark; revisit after soft launch |
| Season pass attach | 6% of D7 players | Directional |
| Crash-free sessions | 99.7% | Section 15 |

**Event schema** (every event carries player id, session id, build, device class, world, stage, class, weapon)

| Event | Fields | Used for |
| --- | --- | --- |
| stage\_start, stage\_end | stage, result, duration, rooms\_cleared, deaths, potions\_used, boons | Drop-off per stage, first-clear time, 30-hour budget re-run |
| parry | precise or soft or miss, enemy family, attack id, time delta to hit frame | Parry success curves per family; telegraph tuning via remote config |
| dodge | success (i-frames absorbed a hit) or not, direction | Red-attack readability |
| death | killing attack id, health history for 10 s, replay seed | Unfair deaths, the failure screen |
| boon\_pick | offered three, chosen, room | Boon balance, dead picks |
| equip\_change | slot, item, from stage preview or hub | Loadout diversity |
| upgrade, craft, reroll | item, cost, currency balances after | Economy flow, bottleneck detection |
| quest\_complete, reward\_claim, streak\_day | ids, day index | Engagement layer health |
| purchase\_offer\_shown, purchase | offer id, price, context | Conversion by context |
| perf\_sample | fps bucket, slow frames, memory, thermal state | Budgets in section 15 |

**Dashboards reviewed weekly**

- Funnel from install to 1-4 clear, with the two tutorial targets.
- Stage heat map: attempts, clear rate, deaths per clear, median time, for all 293 stages. A campaign stage below 70% first-attempt clear or above 3 deaths per clear is reviewed; a stage above 98% from world 2 onward is also reviewed, because it may be winnable without parrying.
- Parry curves: precise and soft rates by family and by world. A family under 40% precise after its second world is retuned.
- Loadout diversity: share of clears per weapon family per world. A family under 8% share is buffed or its stages are rebalanced.
- Hours distribution: histogram of active stage hours per player by cohort, with the 20-hour and 30-hour lines.
- Economy: median gear level versus world cap at each world entry; shard and material balances.
- Engagement layer: calendar claims, streak lengths, quest completion per quest id, event participation.

**Experiments** (remote config, one at a time, minimum 7 days): parry window 200 versus 220 ms; telegraph minimum 600 versus 700 ms in world 1; calendar day-7 reward type; starter bundle timing (after 1-8 versus after world 1 boss).

## 17. Production plan

The plan is gated on the one thing the research could not settle: whether tap-to-parry feels good enough under touch latency to carry the whole game. Six weeks of prototype answer that before anything else is built, and a world-1 vertical slice must hit D1 30% in a closed test before production of the other seven worlds starts.

![illustrative schedule · 4 phases, 3 gates, launch](images/17-production-timeline.png)

Gates are go or no-go; a failed gate loops the phase, it does not skip it.

**Phases and gates**

| Phase | Weeks | Builds | Gate to pass |
| --- | --- | --- | --- |
| Prototype | 1 to 6 | Combat core with Blade and Hammer, Thornback and Shellback, stages 1-1 to 1-8 in grey-box art, the section 6 camera, haptics, sound for parry only | Section 14 feel checklist; precise parry rate above 50% by stage 1-4 in a 20-person test; testers choose the parry build over an "attack button" control variant in a blind A/B |
| Vertical slice | 7 to 16 | World 1 complete in final art, boss, FTUE, HUD, save, analytics, stage editor and both bots, Forge basics | D1 30% or better in a 300-install closed test; first-clear times within 20% of the section 9 targets; both bots pass on all 25 stages |
| Production | 17 to 44 | Worlds 2 to 8, side dungeons, trials, three classes, full Forge, engagement layer, monetization, cloud save, localization hooks | Content complete: 293 stages pass validation; economy targets in section 12 hold on the bots' first-clear path |
| Soft launch | 45 to 52 | Three markets, remote-config tuning, two season cycles rehearsed | D7 8% or better; crash-free 99.5%; no stage above 3 deaths per clear in the campaign |
| Global launch and Season 1 | 53 onward | Launch, Season 1, first event dungeon | Section 16 targets reviewed at day 30 and day 60 |

**Team** (steady state in production; the prototype needs four people)

| Role | Count | Owns |
| --- | --- | --- |
| Design lead and producer | 1 | This document, gates, schedule |
| Content designers | 2 | 293 stages, bosses, boons, quests; about 10 stages per week between them with the editor |
| Gameplay engineer | 1 | Simulation, combat, enemies, bots |
| Platform and tools engineer | 1 | Editor, save, stores, analytics, performance |
| UI engineer | 1 | HUD, screens, contextual Action, safe areas |
| Character and enemy artist | 1 | Silhouettes, telegraph poses |
| Environment and UI artist | 1 | Arena templates, palettes, UI |
| Animator and VFX | 1 | Attack poses, parry and Execute effects |
| Audio (contract) | 0.5 | Telegraph sounds, parry sound, music |
| QA | 1 | Aspect-ratio matrix, device matrix, content validation |

**Risks and responses**

| Risk | Likelihood | Response |
| --- | --- | --- |
| Parry does not feel decisive on touch | Medium | Gate 1 exists for this; fallback is a larger precise window and a stronger soft tier, then a dedicated parry button variant |
| 293 stages at quality | High | Templates, two bots and the editor are built in the slice, before production; cut side dungeons to two per world before cutting campaign stages |
| Revenue without gacha or energy | Medium | Pass and cosmetics sized on the Brawl Stars precedent; soft launch measures attach before global |
| Six enemies crowd a narrow screen | Medium | Caps in section 10; perfect bot rejects unreadable overlaps |
| Android fragmentation on frame time | Medium | 30 fps floor, slow-frame budget, device matrix in QA from the slice onward |
| Engine or runtime decision slips | Low | Decide before the prototype starts; the open question in section 18 |
| Scope creep from LiveOps | Medium | Engagement layer is fixed in section 13; new systems need a gate review |

## 18. Appendix

**Open questions** (each one changes a section; answers go here and the section is revised)

- [ ] Standalone app (Unity 6 default) or a title inside Playabl's own runtime? Decides the engine row in section 15 and who owns the tooling.
- [ ] Is 8 worlds the launch scope, or do worlds 7 and 8 ship as the first two content updates with 6 at launch (about 22 hours) and the 30-hour target met by week 20 after launch? Section 9 and section 17 both move.
- [ ] Rewarded ads at all, or a purely IAP and pass model? Section 12 assumes opt-in rewarded ads with a 4.99 removal.
- [ ] Starting classes: Warden only at the start, or a class choice at 1-1? Section 8 assumes Warden only, to keep the FTUE to one defense style.
- [ ] Soft-launch markets and the test audience for Gate 2.
- [ ] Working title. "Parrylight" is a placeholder and has not been checked for trademark or store-name conflicts.

**Glossary**

| Term | Meaning |
| --- | --- |
| Precise parry | A tap landing within the 200 ms window before the hit frame; full reward |
| Soft parry | A tap in the 200 to 450 ms tier; half damage, no reward |
| Riposte | The 1.5 s after a precise parry in which auto-attacks deal double damage |
| Break | The meter on elites and bosses that parries fill; full means broken for 3 s |
| Execute | The contextual Action on a broken enemy; a cinematic high-damage strike |
| Telegraph | The wind-up of an attack: a colour, a pose, a sound, a duration |
| Red | An unparryable attack; the only correct answer is dodge or leave |
| Boon | A temporary in-stage upgrade chosen between rooms; expires at stage end |
| Room | One wave set inside a stage; ends when all enemies are dead |
| Stage | Three to five rooms plus a final wave or boss; the unit of content and of saving |
| World | 25 stages, one enemy family, one arena rule, one boss |
| Side dungeon | Three-stage remix of a world's rule, unlocked by mastery stars |
| Trial | Fixed-loadout or modifier fight unlocked by a world's boss |
| Mastery star | Reward for one of a stage's three optional objectives |
| Threat band | The lower 22% of the screen, under the thumbs; telegraphs there are mirrored above it |
| Perfect bot, passive bot | Automated players that validate every stage (section 11) |

**Quick reference: initial numbers in one place**

| Value | Number | Section |
| --- | --- | --- |
| Precise parry / soft tier / whiff recovery | 200 ms / 450 ms / 300 ms | 4 |
| Telegraphs, normal / boss fast / floor | 600 to 800 ms / 450 to 550 ms / 450 ms | 4 |
| Dodge duration / i-frames / cooldown | 250 / 180 / 800 ms | 4 |
| Visible width / character anchor / threat band | 9 units / 45% height / lower 22% | 6 |
| Buttons: Special / Action / minimum | 72 / 60 / 44 pt | 5, 7 |
| Stages: campaign / side / trials | 200 / 63 / 30 (293) | 9 |
| First-clear minutes: stage / boss / side / trial | 5.5 / 12 / 6.5 / 8 | 9 |
| Levels / skill points / classes / weapon families | 60 / 30 / 3 / 5 | 8 |
| Active enemies cap: campaign / trials | 6 / 8 | 10 |
| Frame rate target / floor | 60 / 30 fps | 15 |
| Retention targets D1 / D7 / D30 | 35% / 10% / 3% | 16 |
| Season length / rest | 5 weeks / 1 week | 13 |

**Sources** (pages opened for this document; the figures they support are cited inline in section 2)

- [Pixel Blade stats, rotrends](https://rotrends.com/game/6161049307) · [Pixel Blade World 4 guide, roonby](https://roonby.com/2025/12/17/pixel-blade-world-4-guide-tips-and-tricks-to-clear-faster-and-farm-safely/) · [Pixel Blade rings, Pocket Tactics](https://www.pockettactics.com/pixel-blade-rings)
- [Archero 2 guide, Level Winner](https://www.levelwinner.com/archero-2-beginners-guide/) · [Archero 2 revenue, PocketGamer.biz](https://www.pocketgamer.biz/archero-2-makes-328m-in-first-30-days-from-player-spending) · [Survivor.io teardown, Naavik](https://naavik.co/deep-dives/survivorio-archeros-footsteps/) · [Survivor.io retention, mobilegamer.biz](https://mobilegamer.biz/two-months-in-survivor-io-passes-75m-from-37m-downloads/)
- [Brotato waves](https://brotato.wiki.spellsandguns.com/Waves) · [Brotato i-frames](https://brotato.wiki.spellsandguns.com/Iframes)
- [Nine Sols parry](https://ninesols.wiki.gg/wiki/Parry) · [Sekiro deflection](https://sekiroshadowsdietwice.wiki.fextralife.com/Deflection) · [Dead Cells shield](https://deadcells.wiki.gg/wiki/Shield) · [Hollow Knight combat](https://hollowknight.wiki.fextralife.com/Combat) · [Clair Obscur story mode, Automaton](https://automaton-media.com/en/news/clair-obscur-expedition-33-makes-parrying-and-dodging-easier-in-story-mode-allowing-for-a-more-traditional-turn-based-rpg-experience/)
- [Apple HIG game controls](https://developer.apple.com/design/human-interface-guidelines/game-controls) · [Android game quality](https://developer.android.com/quality/technical) · [Play slow sessions](https://developer.android.com/google/play/vitals/slow-session) · [Play vitals thresholds](https://developer.android.com/google/play/vitals) · [Android form factors](https://developer.android.com/games/develop/multiplatform/make-your-game-compatible-with-all-form-factors)
- [GameAnalytics 2026 benchmarks, summary](https://gamedevreports.substack.com/p/gameanalytics-mobile-and-pc-game) · [GameAnalytics 2026 PDF](https://investgame.net/wp-content/uploads/2026/01/2026-01-27-2026-mobile-pc-benchmarks_compressed.pdf) · [Adjust 2026 summary](https://gamedevreports.substack.com/p/adjust-gaming-app-insights-report) · [Mistplay RPG figures via Segwise](https://segwise.ai/blog/mobile-gaming-app-user-retention-strategies.md) · [Mistplay and AppsFlyer loyalty](https://gamedevreports.substack.com/p/mistplay-and-appsflyer-player-loyalty) · [AppMagic live ops 2025](https://gamedevreports.substack.com/p/appmagic-mobile-live-ops-in-2025)
- [Roblox retention](https://create.roblox.com/docs/production/analytics/retention) · [Roblox onboarding](https://create.roblox.com/docs/production/game-design/onboarding) · [Roblox quest design](https://create.roblox.com/docs/production/game-design/introduction-to-quest-design) · [Roblox season pass](https://create.roblox.com/docs/production/game-design/season-pass-design) · [Roblox engagement rewards](https://create.roblox.com/docs/resources/feature-packages/engagement-rewards) · [Roblox LiveOps](https://create.roblox.com/docs/production/game-design/liveops-essentials)
- [Apple loot box odds rule](https://www.fenwick.com/insights/publications/apple-now-requires-disclosure-of-loot-box-odds) · [Google Play odds rule](https://fenwick.com/insights/publications/google-play-now-requires-disclosure-of-loot-box-odds) · [Brawl Stars loot box removal, Deconstructor of Fun](https://www.deconstructoroffun.com/blog/why-removing-loot-boxes-in-brawlstars-failed) · [Brawl Stars comeback, mobilegamer.biz](https://mobilegamer.biz/supercell-explains-brawl-stars-big-comeback-from-an-all-time-low-to-8-8x-revenue/) · [Battle pass statistics (aggregator)](https://www.shanethegamer.com/research/battle-pass-statistics/)
- [Hades God Mode](https://caniplaythat.com/2021/08/11/hades-god-mode-explained-by-supergiant-games) · [Celeste assist mode](https://newnormative.com/2018/01/25/celestes-assist-mode-brings-welcome-accessibility-options) · [Xbox accessibility guideline 103](https://learn.microsoft.com/en-gb/gaming/accessibility/xbox-accessibility-guidelines/103) · [Game Accessibility Guidelines](https://gameaccessibilityguidelines.com/?p=21)
- [Unity pricing](https://unity.com/pricing-updates) · [Godot mobile update, April 2026](https://godotengine.org/article/godot-mobile-update-apr-2026/) · [Defold IAP extension](https://github.com/defold/extension-iap)
