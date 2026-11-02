<!-- from md/01-design.md -->

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
