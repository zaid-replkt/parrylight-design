<!-- from md/02-build-spec-A-formulas-and-systems.md -->

## A2. Combat resolution

One damage formula, one parry resolver, one break rule and four status effects. Everything is integer damage after rounding, and every random roll uses the stage seed so the bots and the death replay are deterministic.

**Damage from the player**

```latex
\mathrm{Damage} = \max\big(1,\ \mathrm{round}((\mathrm{BaseAttack} + \mathrm{WeaponAttack}) \cdot m_{skill} \cdot m_{riposte} \cdot m_{broken} \cdot m_{crit} \cdot m_{boon}) - \mathrm{EnemyDefense}\big)
```

- m\_skill: 1.0 for an auto-attack; the Special's own multiplier (A3).
- m\_riposte: 2.0 during the riposte window (3.0 with Blade), else 1.0.
- m\_broken: 1.5 while the target is broken, else 1.0.
- m\_crit: 2.0 on a critical hit, else 1.0. Base crit chance 5%, raised by rings and skills; capped at 40%.
- m\_boon: product of active boon multipliers (B1), capped at 2.5.
- EnemyDefense: a flat value per family and world (A4), applied last, never reducing below 1.

**Damage to the player**

```latex
\mathrm{Damage} = \max\big(1,\ \mathrm{round}(\mathrm{AttackPower} \cdot m_{parry} \cdot m_{assist}) - \mathrm{Defense}\big)
```

- m\_parry: 0 on a precise parry, 0.5 on a soft parry, 1.0 otherwise. Red attacks ignore the parry entirely (m\_parry stays 1.0).
- m\_assist: 1.0 by default; the "hold to guard" assist applies 0.5 while held (no riposte, no break).
- Defense comes from armour (A3) and the Warden tree; capped so it never exceeds 40% of the incoming attack power (check after subtraction: if Damage < 0.6 × AttackPower × m\_parry × m\_assist, raise it to that).

**Parry resolver** (runs on the simulation thread at 60 Hz; times in ms; constants are remote-config keys in A7)

```
on TouchDown(zone == DEFENSE, t_touch):
  if parry.recoveryUntil > t_touch: return            // whiffed recently, ignore
  if parry.spamCount >= 2 and t_touch < parry.spamResetAt: return   // third rapid tap: no parry
  window = PRECISE_MS (200)                           // widened by assist to 280
  if parry.spamCount == 1 and t_touch < parry.spamResetAt: window = PRECISE_SPAM_MS (120)
  parry.activeFrom = t_touch - INPUT_BUFFER_MS (100)
  parry.preciseUntil = t_touch + window
  parry.softUntil   = t_touch + SOFT_MS (450)         // 550 with assist
  parry.spamCount   = (t_touch < parry.spamResetAt) ? parry.spamCount + 1 : 1
  parry.spamResetAt = t_touch + SPAM_WINDOW_MS (400)  // extended to 600 after a third tap
  play(parryStartAnim)

on EnemyHitFrame(attack, t_hit):                      // the last frame of the telegraph
  if attack.red: applyDamage(player, attack.power, m_parry=1.0); return
  if parry.activeFrom <= t_hit <= parry.preciseUntil:
      precise(attack)                                 // damage 0, stagger, riposte, break, Special charge
  elif t_hit <= parry.softUntil:
      soft(attack)                                    // damage x0.5, no stagger, no riposte, no break
  else:
      applyDamage(player, attack.power, m_parry=1.0)
      parry.recoveryUntil = max(parry.recoveryUntil, t_hit)

on ParryWhiff():                                      // precise window expired with no hit resolved
  parry.recoveryUntil = now + RECOVERY_MS (300)
```

A precise parry also consumes the attack: the attack cannot hit twice, and a multi-hit attack (volley) resolves each projectile separately against the same window, so one tap can reflect up to three arrows if they arrive inside 200 ms.

**Precise parry effects** (in this order)

1. Damage set to 0; hit stop 80 ms; haptic transient; parry sound with pitch-up if the tap was within the first 60 ms of the window ("perfect", used by skills).
2. Attacker staggered: 1.0 s normal, 0.6 s elite; bosses are not staggered.
3. Riposte window: 1.5 s (1.8 s at Blade mastery 3).
4. Break added: normal 0 (no bar), elite +25, boss +Break\_per\_parry from its script (B6), Hammer doubles it.
5. Special meter +16 (so 6 parries fill 100; Warden +20).
6. Projectiles are reflected back along their path at 1.5x speed and deal the weapon's current attack to the first enemy hit.

**Hits on enemies**: Special meter +4 per auto-attack hit (25 hits fill 100; Ranger +5). Break +2 per hit on elites and bosses.

**Break.** Elites: bar of 100, decays 10 per second when not hit, breaks at 100 for 3.0 s, then resets to 0 and the elite is immune to break for 8 s. Bosses: bar size and decay from the script (B6); on break, the current attack is cancelled, the boss is broken for 3.0 s, Execute becomes available. Execute damage = 6 × (BaseAttack + WeaponAttack), ignores defense, ends the broken state.

**Status effects** (applied by weapon trait, boons or skills; one stack each except Bleed)

| Status | Effect | Duration | Stacks | Applied by |
| --- | --- | --- | --- | --- |
| Burn | 4% of the applier's attack per 0.5 s | 4 s, refreshed | 1 | Wand trait, boons |
| Chill | Move and attack speed 0.7x; telegraphs 15% longer | 3 s | 1 | Chakram trait, boons |
| Shock | On application, 50% of the hit's damage jumps to the nearest enemy within 2 units | instant | n/a | Spear trait, boons |
| Bleed | Target takes +10% damage per stack | 5 s | up to 3 | Blade trait, boons |

Status effects never apply to the player; enemy hazards use their own rules (A4).

**Worked example** (world 2, stage 7, level 11, Rare Blade level 3)

- Player attack = 24.0 + 21.2 = 45.2. Thornback (world 2) HP 284, defense 4. Auto-attack: round(45.2) − 4 = 41 per hit, 2.0 per second: dead in 7 hits, 3.5 s.
- The Thornback swings (white, 800 ms). Tap at 150 ms before the hit frame: precise. Damage 0, stagger 1.0 s, riposte: next hits deal round(45.2 × 3.0) − 4 = 132, so two hits in the riposte window kill it: 1.0 s.
- Same swing, tap 320 ms before the hit frame: soft. Attack power 23 × 0.5 = 11.5, round 12, minus armour defense 3 = 9 damage; floor check: 0.6 × 23 × 0.5 = 6.9, so 9 stands. Player health 235 to 226.
- A Shellback jab unparried: 23 − 3 = 20 damage, about 8.5% of health; eight unparried hits kill, as designed (12% at the world's entry level, less once levelled).
