<!-- from md/01-design.md -->

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
