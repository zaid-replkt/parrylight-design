<!-- from md/01-design.md -->

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
