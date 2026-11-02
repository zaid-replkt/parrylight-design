<!-- from md/04-build-spec-C-screens-and-copy.md -->

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
