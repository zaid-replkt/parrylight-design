# Portrait screen layout (text version of 06-portrait-layout.png)

Reference phone 390 x 844 pt, portrait, y measured from the top. Everything scales by percentage of width.

```
+------------------------------------------+  y 0      top safe area (notch / Dynamic Island)
| HUD strip: health bar | room dots | pause |  y 44..84 (starts 8 pt below the safe inset)
|------------------------------------------|
|                                          |
|            PLAY AREA                     |  9 world units wide, 16+ units tall
|     enemies enter from top edge  ^       |  camera width-locked, follows vertically
|                                          |
|              (o) character  <- held near |  y ~ 45% of screen height (380 pt)
|                  45% of height           |
|                                          |
|~~~~~~~~~~~~~~~~~~~~~~|~~~~~~~~~~~~~~~~~~~|  y 295 (35% from top): control band begins
|  MOVEMENT ZONE       |  DEFENSE ZONE     |
|  left half,          |  right half:      |
|  lower 65%           |  tap = parry      |
|  floating joystick   |  swipe = dodge    |
|  appears where the   |  long-press enemy |
|  thumb lands         |  = pin target     |
|                      |        ( Action ) |  60 pt circle, centre x 342, y 700 (contextual)
|      ( joystick )    |       ( Special ) |  72 pt circle, centre x 342, y 780 (fixed)
|~~~~ threat band: lower 22% of screen; telegraphs under the thumbs are mirrored above the band line (y ~ 658) ~~~~|
+------------------------------------------+  y 844   bottom safe area: home indicator, 34 pt, no buttons
```

Notes: the whole upper play area also counts as defense zone for taps (parry) and swipes (dodge); only the movement zone and the two buttons consume touches differently. Left-handed mode mirrors everything. Enemies spawn only from the top and bottom edges, announced 1 s ahead by edge markers.
