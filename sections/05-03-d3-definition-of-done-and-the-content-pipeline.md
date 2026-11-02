<!-- from md/05-build-spec-D-backlog.md -->

## D3. Definition of done and the content pipeline

**Definition of done per content type**

| Content | Done means |
| --- | --- |
| Enemy record | Fields complete per A4; silhouette distinct from every other family at 1 unit; two wind-up poses (parryable raised, unparryable lowered); telegraph lint passes; sounds for every attack; appears in the enemy encyclopedia with its one-line counter |
| Campaign stage | File validates; perfect bot clears with 0 damage; passive bot dies by the final room (world 2 onward: by room 3); dials within the block target (B5); first-clear estimate within 20% of the block target; three mastery objectives of different types; the "new decision" field filled and approved by a second designer; played once by a human on a 9:16 device and once on a 3:4 device |
| Boss | Script per B6; every attack rehearsed by a stage in 21 to 24; a no-damage clear is possible for the perfect bot; break count and finisher verified; intro and victory beats; unique Execute animation |
| Side dungeon | Three stages as above; the remix rule is visible in the first room; elite pair script; reward entry in the loot table |
| Trial | Type rule enforced by data flags; assists disabled; pass condition tested by both bots (perfect passes, passive fails) |
| Boon | Effect implemented as a rule hook, not a special case; stack cap; class exclusion; shows correctly on the pick card and the pause list; one automated test per boon |
| Skill node | Effect hook; tooltip string; respec returns it; one test |
| Ring affix | Value range by quality; cap across both rings enforced; re-roll excludes duplicates on the same ring |
| Quest or achievement | Progress hook fires from the right event; claim flow; string; a test that completes it in a scripted run |
| Screen | Matches C1 positions within 4 pt; all states reachable; back gesture and close control; safe-area insets on the device matrix; strings from the table, none hard-coded; analytics events on open and primary action |
| Cosmetic | Readability check against the telegraph palette and colour-blind modes; no silhouette change |

**Content pipeline** (one stage, start to ship)

1. Designer picks the block in B5 and writes the stage file in the editor (spawns, timings, rule parameters, boon pool, mastery, rewards from A1).
2. Editor runs schema validation and both bots locally; the designer adjusts until the dials and the time estimate are inside the targets.
3. Designer fills `new_decision` in the file; a second designer approves it in review or sends it back.
4. CI runs validation and both bots on the merge; failures block the merge.
5. Art attaches the arena template decoration and any new record's assets; the telegraph palette check runs on the world's palette.
6. QA plays the stage on the device matrix (one 9:16, one 9:19.5, one 3:4, one low-end Android) and checks the portrait readability list in design section 6.
7. The stage ships behind the world's unlock; analytics watch its first-attempt clear rate and deaths per clear for the thresholds in section 16; a stage outside them goes back to step 1 with the data attached.

**Weekly content cadence in production**: 10 stages across two designers, which with 268 remaining stages is 27 weeks; the schedule in section 17 allows 28. Bosses, dungeons and trials are inside that count (a boss counts as 4 stages of effort, a dungeon as 3, a trial as 1).

**Cuts in order, if the schedule slips**: third side dungeon per world (saves 21 stages), trials in worlds 4 and 5 (12), world 8's side dungeons (9). Campaign stages and bosses are never cut; the 30-hour target drops to about 26 hours after the first cut and is restored by the first content update.
