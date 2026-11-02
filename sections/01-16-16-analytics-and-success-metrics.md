<!-- from md/01-design.md -->

## 16. Analytics and success metrics

Success is measured against the top-quartile row of the 2026 benchmarks in section 2, lifted for the genre: D1 35%, D7 10%, D30 3%, and a content-depth check that at least 15% of D30 players have passed 20 hours of active stage time. These are launch targets for the first 60 days, reviewed after soft launch.

**Targets**

| Metric | Target | Benchmark context |
| --- | --- | --- |
| D1 retention | 35% | Median 22%, top quartile about 30%, RPG reference 30.5% |
| D7 retention | 10% | Top quartile 6 to 8%, RPG reference 9.9% |
| D30 retention | 3% | Top quartile 1.6 to 1.8%, RPG reference 3.5% |
| Reach stage 1-2 | 95% of installs | Funnel, section 13 |
| Clear 1-1 first attempt | 90% | Funnel |
| Time to first parry | Under 30 s median | Funnel |
| Session length | 12 min median | All-mobile median 3.1 to 3.5 min; action genre runs long |
| Sessions per day (D7 cohort) | 2 | All-mobile median 3.8 is driven by casual |
| Active stage hours at D30 | 15% of D30 players past 20 h; median D30 player past 8 h | The 30-hour claim, checked |
| World 8 clear rate | 8% of D30 players by day 60 | Content pacing |
| Payer conversion by D30 | 2.5% | No reliable 2026 genre benchmark; revisit after soft launch |
| Season pass attach | 6% of D7 players | Directional |
| Crash-free sessions | 99.7% | Section 15 |

**Event schema** (every event carries player id, session id, build, device class, world, stage, class, weapon)

| Event | Fields | Used for |
| --- | --- | --- |
| stage\_start, stage\_end | stage, result, duration, rooms\_cleared, deaths, potions\_used, boons | Drop-off per stage, first-clear time, 30-hour budget re-run |
| parry | precise or soft or miss, enemy family, attack id, time delta to hit frame | Parry success curves per family; telegraph tuning via remote config |
| dodge | success (i-frames absorbed a hit) or not, direction | Red-attack readability |
| death | killing attack id, health history for 10 s, replay seed | Unfair deaths, the failure screen |
| boon\_pick | offered three, chosen, room | Boon balance, dead picks |
| equip\_change | slot, item, from stage preview or hub | Loadout diversity |
| upgrade, craft, reroll | item, cost, currency balances after | Economy flow, bottleneck detection |
| quest\_complete, reward\_claim, streak\_day | ids, day index | Engagement layer health |
| purchase\_offer\_shown, purchase | offer id, price, context | Conversion by context |
| perf\_sample | fps bucket, slow frames, memory, thermal state | Budgets in section 15 |

**Dashboards reviewed weekly**

- Funnel from install to 1-4 clear, with the two tutorial targets.
- Stage heat map: attempts, clear rate, deaths per clear, median time, for all 293 stages. A campaign stage below 70% first-attempt clear or above 3 deaths per clear is reviewed; a stage above 98% from world 2 onward is also reviewed, because it may be winnable without parrying.
- Parry curves: precise and soft rates by family and by world. A family under 40% precise after its second world is retuned.
- Loadout diversity: share of clears per weapon family per world. A family under 8% share is buffed or its stages are rebalanced.
- Hours distribution: histogram of active stage hours per player by cohort, with the 20-hour and 30-hour lines.
- Economy: median gear level versus world cap at each world entry; shard and material balances.
- Engagement layer: calendar claims, streak lengths, quest completion per quest id, event participation.

**Experiments** (remote config, one at a time, minimum 7 days): parry window 200 versus 220 ms; telegraph minimum 600 versus 700 ms in world 1; calendar day-7 reward type; starter bundle timing (after 1-8 versus after world 1 boss).
