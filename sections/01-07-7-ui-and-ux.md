<!-- from md/01-design.md -->

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
