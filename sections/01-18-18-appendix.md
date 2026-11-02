<!-- from md/01-design.md -->

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
