# 6-7 — Game Design

A psychic-testing guessing game. Tap 6 or 7. The orb knows which one is right. Are you?

---

## 1. Vision & pillars

**Pitch:** A 20-second psychic test you can't stop re-taking. The game is honest — it's a true
50/50 — and that honesty *is* the hook: every streak, hot run, and weird stat is real, so it
feels genuinely spooky when it happens.

**Pillars (every feature must serve one):**
1. **Fast** — a guess resolves in ~200ms; input is never blocked; a speedrunner can play ~2 guesses/sec.
2. **Honest** — fair RNG, pre-committed targets, real stats with chance baselines shown. No pity wins, no rigging. The spookiness must be earned.
3. **Playful, lightly psychic** — flat, colorful, fun: something the generation that invented the
   6-7 meme would appreciate, and adults too. The intuition angle stays subtle and informative —
   "can you feel it?" — never occult. The meme is seasoning (bouncing cards, 666/777 beats,
   67% certification), not the whole dish.

---

## 2. The core loop

```
READY ──tap 6 or 7──▶ REVEAL (≤500ms, interruptible) ──▶ READY
  ▲                                                      │
  └────────── next target already generated ─────────────┘
```

- **Ready state:** crystal orb in center shows `?` with a subtle idle pulse. Reaction timer starts now.
- **Tap:** two giant cards — 6 and 7 — side by side in the thumb zone, idle-bouncing in alternation
  (the 67 hand-gesture homage). Tap registers on pointer-down.
- **Reveal (~500ms full, interruptible):** ~70ms micro-anticipation (orb squeezes) → number pops with
  a burst (~150ms in) → celebration tail settles by ~500ms. The anticipation beat matters: dopamine
  fires on *anticipation* more than reward (Schultz; slot-machine research). A next tap at any moment
  cuts the animation short and resolves instantly — fast players set the tempo, never the animation.
- **Win feedback:** color burst + particles, streak counter ticks with a pitch-rising blip
  (one semitone per consecutive win — the Tetris/Candy Crush ladder), small haptic.
  Celebration layers are fire-and-forget — they never block the next tap.
- **Loss feedback:** ~120ms. Orb dims gray, correct number shown small, soft thud. Never punishing.
- **Input is never blocked.** Tapping mid-celebration cancels it and resolves the next round.
  This is what makes rapid-fire play possible.

---

## 3. Research notes → mechanics map

What the psi-training literature actually does, and what we steal from it:

| Practice (source) | What they do | Our mechanic |
|---|---|---|
| **Zener card runs** (Rhine, Duke 1930s) | Runs of 25, 5 symbols, chance=20%, score vs. chance, ≥50 trials for reliability. "Open deck" gives per-guess feedback for training. | **Sets of 9**, chance=4.5, set won at 6+, per-guess feedback, lifetime trial count displayed ("psychics need volume"). |
| **Psi-missing** (Rhine) | Scoring significantly *below* chance is treated as equally anomalous — evidence of psi working in reverse. | The **Reverse Oracle** stat: a 1/9 set is as rare as an 8/9 (2%). Celebrate it: "Wrong on purpose? Scoring this low is just as spooky." Losses become content. |
| **Decline effect** (Rhine) | Scores start high, sag in the middle of long runs, recover at the end — boredom kills performance. | Keep sets **short (9)**, vary celebrations, escalate novelty with streaks. Never let the game feel like a grind of identical trials. |
| **Analytical Overlay / AOL** (CRV remote-viewing protocol) | Overthinking = "conclusion-jumping" noise contaminating the raw signal. Viewers train to act on first impressions; immediate feedback is mandatory ("without feedback you aren't doing CRV"). | **Gut vs. Brain stat**: bucket every guess by reaction time. "⚡ Instinct taps: 54% · 🧠 Overthought taps: 47%." The game's headline insight — and exactly the speed/accuracy relationship we want to surface. |
| **Red/black card drill** (intuition-development practice) | THE classic home exercise: guess red or black before each flip, trust the first flash, keep a journal of hits. | Validation that the core game IS the established drill, digitized. The stats page is the "intuition journal," auto-kept. |
| **Confidence calls** (Rhine's labs) | Subjects flag trials where they "felt sure"; high-confidence trials analyzed separately. | **Called Shots** (post-MVP): long-press your guess to "call it" — double streak credit if right. Stats track called-shot accuracy separately. |
| **Ritual / intention setting** (modern intuition practice) | Brief centering before a session. | Optional 1-beat "breathe" pulse when a run starts (skippable by tapping). Sells the ritual without costing speed. |

---

## 4. Dopamine architecture

The game is natively a **variable-ratio reinforcement schedule** (the strongest habit-forming
schedule known) — 50% wins with escalating streak jackpots. We don't need to manufacture a slot
machine; we need to *surface* the one that's already there.

**The streak ladder** (probability of reaching from any start: 1/2ⁿ):

| Streak | Odds | Juice |
|---|---|---|
| 2 | 1/4 | Counter glow |
| 3 | 1/8 | Color shift + bigger particle burst + haptic pattern |
| 5 | 1/32 | Flame mode 🔥, screen edge glow |
| 6 | 1/64 | **"666 — ominous."** easter egg beat |
| 7 | 1/128 | **"LUCKY 7s"** — jackpot-tier celebration, the game's signature moment |
| 10 | 1/1024 | Full-screen flourish, permanent badge |

Pitch-rising audio per win in a streak is the cheapest, most effective dopamine lever we have.
Reset on loss = soft thud + immediate display of `best: N` (the record persists; the loss doesn't erase identity).

**Flavor layer:** streaks built on 6-wins lean "sixth sense," streaks on 7-wins lean "lucky" —
the game keeps asking: **is it 6th sense, or lucky 7?**

**Near-miss surfacing** (near-misses activate win circuitry in the striatum — slots research):
- "1 away from your best streak!"
- Set summary: "5/9 — one short of the set win."
- Never fabricate near-misses (no rigged "almost" reveals) — only *report true ones*.

**Endowed progress:** the 9 set-dots are always drawn (empty) — completing a partially-filled
frame is a drive. Set 4/9 *feels unfinished*, which carries you to 9.

**Session shape:** a set = 9 guesses × 1–2s = **15–35 seconds**. Summary screen is the
stop/continue decision point: giant NEXT SET, small share/stats. "One more set" should be
the path of least resistance; stopping should feel like closure (stats = souvenir), never guilt.

---

## 5. Sets of 9 & the 6-7 of it all

Play happens in **sets of 9 guesses**. Chance expectation: 4.5. **Score 6 or better and you win
the set** — you literally need *a six or a seven* (or more) out of nine, and 6/9 = **67%**.
The threshold is the meme, and it's statistically honest: pure luck wins a set only ~25% of the time.

| Score | P(≥k) by luck | Summary copy |
|---|---|---|
| 9 | 0.2% | "A perfect set is 1 in 512. Who told you?" |
| 8 | 2.0% | "1 in 51 by pure luck. Suspicious." |
| 7 | 9.0% | "Top 9% of luck. The sevens like you." |
| 6 | 25.4% | "**SET WON** — only 1 in 4 coin-flippers pull this off." |
| 5 | 50.0% | "Dead-on coin-flip territory. One more next time." |
| 4 | 74.6% | "A hair below chance. Slightly haunted." |
| 3 | — | "Reverse 6-7: as rare as winning the set, the wrong way." |
| ≤2 | (≤9% low) | "Bottom 9%. Reverse oracle rising." |
| 0 | (0.2% low) | "Perfectly wrong: 1 in 512. Honestly impressive." |

Set summary also shows: best streak in set, ⚡gut vs 🧠brain split, lifetime strip, certification progress.

### The grid — set visualization

The set fills a **3×3 grid** in reading order; each row is a trio of guesses. Hit cells fill in
the target's color (grape 6 / shamrock 7) with the number; missed cells dim gray showing what it
was. The cell up next has a darker dashed border.
- **Row markers** (right of each row, pop in when the trio completes):
  ★ gold = 3/3 · ✓ shamrock = 2/3 · – muted = 1/3 · ✕ red = 0/3.
- **Lines:** three hits in any row, column, or diagonal get a persistent gold outline; columns and
  diagonals also fire a "line! bonus vision" toast. A 3/3 row is both a star and a line.
- The summary sheet replays the set as a mini grid with the same markers.

### 67 Certified — the flagship achievement

Maintain a **67%+ hit rate on individual guesses across your last 33 sets** (≥2/3 of 297 guesses,
i.e. 198+) and you are **67 CERTIFIED** — a *live status*: it can lapse and be re-earned.
A **maintenance tracker** counts how many consecutive sets you've stayed certified
("5 sets strong"), with the longest run recorded in stats.
Honest math: a 33-set window certifies by pure luck ~5.7σ above chance — about 1 in 200 million.
Certification is deliberately "the universe broke" tier.
UI: gold chip in the header while certified; progress in stats ("last 33: 58% — need 67%").

### The 76 award — reverse oracle certification

The mirror image: a **67%+ *miss* rate over the last 33 sets** (≤99 hits of 297) earns the
**76 AWARD** — being reliably wrong at this scale is exactly as anomalous as being reliably right
(psi-missing, Rhine). Red chip in the header, its own maintenance run + best-run tracker, and a
descending fanfare when earned.

---

## 6. Stats — "The Psi Profile"

The retention backbone for the curious. All real, all against visible chance baselines
(shaded "chance zone" bands so deviations read honestly).

1. **Overview:** lifetime hit% inside a chance band (±2σ for n), total guesses, best streak,
   best set, **Psi Index** — a playful gauge that is literally the z-score:
   `z = (hits − n/2) / (√n / 2)`. Labels: −2σ "Reverse Oracle" … 0 "Mortal" … +2σ "Statistically Spooky."
   Early on the gauge swings wildly (small n) — honest *and* exciting; it stabilizes as you play,
   which quietly teaches the statistics.
2. **Gut vs. Brain:** hit% by reaction-time bucket — ⚡ <700ms / ~ 700–1500ms / 🧠 >1500ms —
   plus median reaction time. The headline stat.
3. **Patterns — Team 6 vs Team 7:** pick bias ("You pick 7 62% of the time" — humans famously
   over-pick 7), hit% on 6-picks vs 7-picks ("is it 6th sense, or lucky 7?"), hit% by hour of day
   ("you're sharpest at 11pm"), last-100 sparkline, current hot/cold reading.
4. **History:** daily-run calendar, records.

---

## 7. Retention systems

- **The Daily 9** — date-seeded PRNG, so every player on Earth gets the *same hidden sequence*
  each day. One attempt per day. Wordle-grade share string, zero backend:
  ```
  6-7 Daily #214 — 7/9 ✅ set won
  🟣🟢⚪🟢🟢🟣⚪🟣🟢 best streak 4
  ```
- **Records & badges:** 67 Certified (flagship), best streak, best set, lifetime milestones
  (100/1k/10k guesses), Lucky 7s count, Reverse Oracle sets, perfect Daily.
- **Titles (XP by volume, always accruing — progress never depends on luck):**
  Coin Flipper → Lucky Guesser → Hunch Haver → Pattern Seer → Vibe Reader →
  **Sixth Senser → Seventh Senser** → Oracle. (The 6→7 climb embedded in the title track.)
- **No dark patterns:** no daily-streak guilt copy, no consumables, no timers pressuring return.
  The pull is curiosity ("is my gut stat still holding?"), not obligation.

---

## 8. Modes

| Mode | What | When |
|---|---|---|
| **Classic** | Sets of 9, the core game | MVP |
| **Daily 9** | Shared seed, 1/day, shareable result | v1.1 |
| **Zen** | Endless, no run framing, ambient — the "ganzfeld mode" (relaxed state purportedly helps psi) | P2 |
| **Rush** | 30 seconds, max hits — leans on the speed stat | P2 |
| **Called Shots** | Long-press = confidence call, 2× streak credit | P2 |
| **The 67** | 67-guess marathon, meme homage | P3 easter egg |

---

## 9. Mobile UX spec

```
┌─────────────────────┐
│ 6·7      [67✓][▦][♪]│  brand · cert chip · stats · mute
│  ●●●●○○○○○  set 4/9 │  set dots (endowed progress)
│      🔥 4  best 7   │  streak + record
│                     │
│       ╭─────╮       │
│       │  ?  │       │  the orb — reveal zone, center
│       ╰─────╯       │  ("can you feel it?" / ⚡ 412ms)
│                     │
│  ┌───────┐┌───────┐ │
│  │   6   ││   7   │ │  two giant CARDS, thumb zone,
│  └───────┘└───────┘ │  idle-bouncing in alternation
└─────────────────────┘  (the 67 hand gesture)
```

- Portrait, one-hand. Cards ≥ 120px tall, huge type. Idle bounce: ~1.5s cycle, a few px,
  offset half-cycle apart — reads as the meme gesture without inviting mistaps.

**Aesthetic — "candy-flat toy arcade":** flat, colorful, fun; psychic subtle, never occult.
- Palette: warm cream bg `#FFF4E4`, ink `#2A2140`; **6 = grape `#7A5CFF`** (sixth sense),
  **7 = shamrock `#14B873`** (lucky 7), **gold `#FFB42E`** for certification/jackpot moments.
  Dark-mode variant: deep plum bg, same accents.
- Depth via hard-offset solid shadows (chunky pressable cards) — no blur, no gradients.
- Type: chunky rounded display (Lilita One) for numerals/score + Baloo 2 for UI;
  falls back to `ui-rounded`/system when offline.
- Particles burst in the color of the revealed number (grape for 6, shamrock for 7).
- Copy voice: lowercase, playful, lightly self-aware ("can you feel it?").
- `touch-action: manipulation`, `user-select: none`, proper viewport meta, safe-area insets.
- Animations: CSS `transform`/`opacity` only (GPU-composited; no layout thrash at 2 taps/sec).
- **Audio:** WebAudio oscillator blips (no asset files) — pitch ladder on streaks. iOS requires
  unlock on first tap (our taps are gestures — free). Mute toggle persisted.
- **Haptics:** `navigator.vibrate` (Android; iOS Safari unsupported — degrade silently).
- `prefers-reduced-motion` respected (skip particles/shake, keep color).
- PWA/installable: already P3 in roadmap.

---

## 10. Fairness & integrity (non-negotiable)

- RNG: `crypto.getRandomValues`. Target generated **before** the player taps — the whole run's
  sequence pre-committed at run start.
- Stated in-app ("the number is chosen before you tap"). Trust is the product: stats are only
  interesting if the game is provably not rigging against you.
- Never manipulate odds. No pity wins, no manufactured near-misses, no "engagement-optimized" RNG.
- Nerd-cred P3: show hash of the run sequence at start, reveal seed at end — provable fairness.

---

## 11. Data model (localStorage, schema-versioned)

```js
guess: { t, rt, pick, target, hit, streak, runId, mode }
// t: epoch ms · rt: ready→tap ms · pick/target: 6|7
```
Raw log capped (~last 5,000 guesses); aggregates (by bucket/hour/pick) maintained incrementally
beyond that. Export-as-JSON button (it's *their* psychic journal).

---

## 12. Build sequencing

- **MVP (v1):** core loop + streak ladder (visual + audio) + sets of 9 w/ set-win + summary w/
  luck copy + 67 Certified tracking + basic stats (hit%, best streak, sets won, gut-vs-brain,
  Team 6/7) + localStorage.
- **v1.1:** Daily 9 + share string.
- **v1.2:** full Psi Profile, badges/titles, haptics polish, settings (mute, reduced motion).
- **P2:** modes (Zen, Rush, Called Shots).

---

## 13. Decisions log (2026-06-11)

1. **Layout:** two-card design (6 and 7 as tap cards) with the orb in the middle showing the result.
2. **Reveal:** orb burst. Full animation ~500ms; a next tap cuts it short instantly.
3. **Meme integration — light:** cards idle-bounce in alternation (67 hand gesture); 666/777 streak
   beats; "six… SEVEN!" easter egg; "is it 6th sense, or lucky 7?" as recurring flavor question.
4. **Sets of 9**, win at 6+ (6/9 = 67%). Stats accumulate lifetime.
5. **67 Certified:** maintain ≥67% over last 10 sets (rolling). Flagship achievement.
6. **Aesthetic:** flat, colorful, fun — Gen-Alpha-friendly, adult-clean. Psychic framing subtle and
   informative ("can you feel it?"), never occult. Candy-flat palette: grape 6 vs shamrock 7 + gold.
7. **Called Shots:** held for P2. MVP friction stays at zero.

## 14. Decisions log (2026-06-12)

1. **Grid visualization shipped:** sets render as a 3×3 grid (rows = trios) with row outcome
   markers (★ 3/3 gold, ✓ 2/3, – 1/3, ✕ 0/3) and gold-outlined hit-lines (see §5).
2. **Certification rebased to 33 sets**, judged on individual-guess hit rate (≥2/3), with a
   consecutive-sets maintenance tracker (current + best).
3. **76 award added** — the psi-missing mirror (≥2/3 miss rate over 33 sets), red chip, own tracker.
4. **Intuition tips shipped:** one per set summary, rotating pool of 14, remote-viewing practices
   in plain playful language ("trust the first flash…"). No jargon, no woo.
