<!-- from md/01-design.md -->

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
