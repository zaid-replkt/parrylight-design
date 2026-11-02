<!-- from md/04-build-spec-C-screens-and-copy.md -->

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
