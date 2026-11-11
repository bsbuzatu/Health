# Healthy Life — training, fasting and food log

Single-file offline PWA for strength training, Zone 2 cardio, fasting and preset meals. No build step, no dependencies, no backend. All data lives in the browser (IndexedDB) and never leaves the device.

**Live:** https://bsbuzatu.github.io/Feeder/
**Build:** `2026-11-10-v11.4.2`
**Repo name unchanged** (`feeder`) — only the app's display name changed, so the Pages URL and any home-screen shortcut keep working.

---

## What it does

| Tab | Purpose |
|---|---|
| **Gym** | Week plan, next session (A→B→C rotation), run a Full-Body session, Zone 2 timer or manual walk entry |
| **Fast** | Start / end a fast (16 h target), edit start and end afterwards, 7-day average, history |
| **Food** | **Log** a meal by tapping its code (+ optional comment) · **Meals** raw weights for one day of each preset · **Shop** tap the meals you'll buy for, get the aggregated raw-weight list · **List** approved foods |
| **Stats** | Body composition, waist, Health card (FibroScan / CAP / labs vs targets), fasting and intake averages, volume |
| **Settings** | Targets (kcal, protein, fast hours, goal weight), export / import JSON v4, deload, Zone 2 calibration, wipe |

---

## v11.5.1 (11 Nov 2026)

Fix: on iOS 26 the rest timer and tab bar floated mid-screen over the set rows after the keyboard closed, and the page jumped while typing.
- Layout is now an app shell: header, rest box and tab bar are flex rows, only the content area scrolls. Nothing is `position:fixed`, so the rest box cannot cover a set.
- Shell height is pinned to the tallest window height seen; the document is un-panned once the keyboard is gone.
- No data, store, export or program changes.

## v11.5 (10 Nov 2026)

- **Food → Log records what was eaten.** Pick a meal; every ingredient gets a row with the planned raw grams in grey. The box is empty until you type; an empty box means not eaten (confirmed on save). "+ ingredient" offers only allowed foods; "Fill planned" copies the plan when you ate exactly that. Macros are computed from the typed grams.
- **Free entry** replaces Various/Estimate: free text + grams for parties and restaurants. Stored as text, not counted in the day totals, shown as off-plan.
- **Meal set rebuilt**: no dairy foods (whey isolate stays), smaller batch portions, oat-banana blender shake, weekend omelette with rye and berries. Every morning item + two portions of any batch = 2,140–2,240 kcal and 159–183 g protein.
- **Protein target 165 g** (stored 185 is migrated once).
- **Session B**: overhead triceps removed; rests on RDL, overhead press and incline DB press 120 s. Weekly triceps target 4 sets.
- **Stats**: 7-day mean weight, 4-week rate, waist change come first; scale body composition moved to a muted trend-only line.
- **Zone 2** weekly target 120 min (3 × 40).
- Food list: beef, sardines and mackerel capped at once a week; dairy foods, chickpeas and beans moved to the avoid list.
- hs-CRP is entered in mg/dL, as the lab prints it.
- Fixed escape codes that were displayed literally in some static texts.

## v11.4.2 (10 Nov 2026)

Bug fix: **Edit start** on a running fast could not be used — the card was rebuilt every second (since the seconds display of v11.3), which destroyed the date-time input and closed the picker. The controls are now built once and only the live block (timer, bar, estimate) is repainted.

---

## v11.4.1 (10 Nov 2026)

Label only: the fast card and dashboard now say **fat used as fuel (est. — not net loss)** instead of "fat oxidised". The number is the resting fuel mix during the fast (RQ-based: ~45 % fat after a meal rising to ~85 % by 18 h); net fat loss over the day is the energy deficit, read from the scale trend.

---

## v11.4 (9 Nov 2026)

1. **Warm-ups redefined.** Heavy barbell / leg-press lifts (squat, bench, RDL, hip thrust, leg press) get two warm-up rows: ~50 % × 8 and ~75 % × 3. Dumbbell, row and pulldown compounds get one: ~60 % × 6. Warm-ups are computed from the working weight, rounded to the exercise increment, and stay excluded from volume. The point: ramp up fast and low-rep, then do **three working sets at one load**. The export showed ramps (40/60/60) being logged as working sets, which halves the real hard-set count.
2. **Meal set rebuilt — eight batches, no chickpeas.** M1 chicken · brown rice · green beans; M2 trout (or salmon) · potatoes · yogurt-dill · salad; M3 turkey · bulgur · roasted vegetables; M4 pork tenderloin · sweet potato · yogurt · salad; M5 cod · sweet potato · spinach · yogurt-lemon; M6 tuna · quinoa · tomato-cucumber · olives; M7 chicken · whole-wheat pasta · tomato-basil · parmesan; M8 frittata · potatoes · peppers · yogurt. Skyr → Greek yogurt 2 %. Every morning item × every batch (24 days) lands in 2,060–2,250 kcal and 182–215 g protein, fat ≥ 53 g — verified with the app's own `mealMacros`.
3. **Various (VAR).** Pick ingredients from the food table and type raw grams, several lines per meal; macros are computed and the lines are stored with the meal (`items:[{k,q}]`) so an export can be analysed. **OTH** remains for a bare kcal/protein estimate. Day totals now show kcal, protein, carbs and fat; the 14-day history shows P / C / F per day.
4. **Shop rebuilt.** Select meals with day counts (batches, omelette, shakes); the list contains **only** the selected meals' raw ingredients, summed and rounded up to 50 g (10 g for staples, whole pieces for eggs/lemons/garlic). Every quantity is an input: type the real pack weight and it is kept until Clear. No stock/always sections, no ticking.
5. Food table extended (trout, pork tenderloin, bulgur, whole-wheat pasta, parmesan, olives, green beans, fruit, oats, cottage cheese, bread, nuts, avocado, carrot, cabbage, mushrooms, cheese, white beans, shrimp) so Various covers normal eating out.

---

## v11.3 (9 Nov 2026)

1. **Set boxes start empty; last session lives in the placeholder.** Set *j* today shows set *j* of the last session of that exercise, verbatim — no ≥ 80 % "working set" filter, no padding of missing sets, no suggestion. A session that had two sets shows two placeholders and an empty third row. A set cannot be confirmed until both numbers are typed. (v11.2 still pre-filled editable values, which a checkmark could save unedited — see *Progression*.)
2. **Fast tab rebuilt.** Timer shows `h:mm:ss`. While fasting: elapsed, time to target, and an estimate of fat oxidised so far. After *End fast*: the card freezes on the **last fast** — duration, start → end, target met or not, fat estimate. The eating-window counter is gone. Dashboard: fasts this week, average length, ≥ target count, streak at target, hours fasted in 7 days, fat oxidised in 7 days, longest in 30 days.
3. **Fat-oxidation estimate** (`fastEstimate`): Mifflin-St Jeor BMR from the latest weight and the age/height in Settings, spent at resting rate; share of energy from fat 45 % in the first 4 h, rising to 75 % at 12 h and 85 % from 18 h; 9.4 kcal/g. It is labelled *estimate* everywhere: it is fat **oxidised during the fast**, not net fat lost — the eating window decides the net. The scale trend over 4 weeks is the real number.
4. **Measurements: circumferences and blood pressure.** New fields biceps, forearm, chest, thigh, calf (cm) and systolic / diastolic / pulse. Stored in the existing `metrics` store (export format unchanged, v4). Stats shows the latest circumferences with deltas, flags when the last set is older than 35 days, and shows the latest BP with a flag when it is older than 3 months or none exists.
5. **Health card:** nine more lab definitions — serum iron, TIBC, TSAT, HOMA-IR, uric acid, creatinine, 25-OH vitamin D, FIT, calprotectin.
6. **Privacy:** the one-off lab seed (a real result hard-coded in the source) and the hard-coded starting weight were removed; the Health card now reads everything from IndexedDB. Settings gains *Age* and *Height* for the estimate (defaults in code are generic).

---

## v11.2 (5 Nov 2026)

1. **Renamed to Healthy Life.** Title, home-screen name (`apple-mobile-web-app-title`), header strip. Export files are now `healthy-life-YYYY-MM-DD.json` and carry `app: "healthy-life"`; the export format is still **v4** and import still accepts v2–v4, so older exports load unchanged.
2. **Real icon files** replace the inline SVG letter: `favicon.ico` (16 / 24 / 32 / 48 / 64 / 128 / 256 px) and `apple-touch-icon.png` (180 px) — green pulse line on black, matching the app theme. Both must sit next to `index.html` in the repo root.
3. **Full-Body B — Chest Fly is now a dumbbell fly** (`dbFly`, "DB Chest Fly (flat bench)"), 2 × 12–15, RIR 1.
4. **Full-Body B — Cable Lateral Raise replaced by Machine Lateral Raise, both arms** (`machLat`), 2 × 12–20, RIR 1. The gym has several pulley stations whose stacks do not align, so the cable series (3.4 → 9 kg across sessions) was never a progression series — it was equipment noise.
5. **Tap a number box and it clears.** See below.

Both new exercises got **new exercise ids**, not renames. `cabFly` and `cabLat` stay in the catalogue so the old history still maps and still counts in volume stats, but their loads are not carried into the new movements — machine fly at 56 kg and a DB fly at 12 kg per hand are not the same number. The first DB fly and machine lateral raise sessions therefore start with **empty boxes and no "Last:" line**; from the second session both progress normally.

### Tap-to-clear number boxes

Previously the box held the last recorded value and iOS often placed the caret at the start, so typing `70` over `65` produced `7065`.

Now, for every numeric box in the app (sets, warm-ups, measurements, targets, labs, Zone 2):

- tap it → the box empties and the old value moves into the **placeholder**, dimmed;
- type → only what you typed is in the box;
- leave without typing → the old value comes back;
- delete the value on purpose → it stays empty.

Nothing is ever read out of a placeholder. `boxVal()` / `rv()` return the typed value, or the parked value if the box was only tapped, or `''` if it was deliberately emptied, and every numeric read in the app goes through them. The integrity rule is unchanged: **a set cannot be confirmed without real numbers in both boxes.**

Set and warm-up rows now write on `input` rather than `change`, so a value is captured as it is typed and never depends on blur ordering.

---

## Training program (v11)

Full-Body ×3 per week (Mon / Wed / Fri, 07:00, fasted). Replaced a 4-day Upper/Lower split because actual attendance was 2.6–2.9 sessions per week and the missed days fell disproportionately on lower body — quads were getting 7 sets/week and hamstrings 5, both below the hypertrophy threshold.

| Session | Exercises |
|---|---|
| **A — Squat + Bench** | Back Squat · Bench Press · Supinated Pulldown · One-Arm Machine Row · Seated Leg Curl · DB Lateral Raise · Overhead DB Triceps Ext · Machine Ab Crunch |
| **B — Leg Press + OHP** | Leg Press · RDL · Seated DB OHP · Single-Arm DB Row · **DB Chest Fly** · **Machine Lateral Raise** · Hammer Curl · Overhead DB Triceps Ext · Seated Calf |
| **C — Hip Thrust + Incline** | Hip Thrust · Incline DB Press · Close-Grip Pulldown · Leg Extension · Seated Leg Curl · Face Pull · Incline DB Curl · Rope Pushdown · One-Leg Calf · Pallof |

Straight sets, same load across sets. RIR 2 on compounds, RIR 1 on isolation. One warm-up set per compound, logged separately and excluded from volume. No supersets, no drop sets. Rotation is by **letter, not weekday**: the next session is the one after whatever was last lifted.

Weekly volume at 3 sessions: quads 8 · hamstrings 8 · chest 8 · back 9 · delts 9 · glutes 3 · calves 4 · biceps 4 · triceps 6 · abs 4. Tracked live in **Stats → Sets per muscle group (7 days)**.

---

## Progression

**Double progression, manual.** The boxes are empty; the **placeholder** of each set shows the same set of the last session, exactly as it was — no suggestion, no automatic increase. Hitting the top of the rep range on every set is the signal to add the smallest real increment next time, and that decision is typed in by the lifter.

Increments (`inc` in `SESSIONS`): 5 kg on leg press / hip thrust / pulldowns / machines, 2.5 kg on barbell and dumbbell presses and rows, 1 kg on DB lateral raises and incline curls. Barbell lifts never go below the 20 kg bar.

Confirming a set saves exactly what was typed. Empty boxes are rejected; placeholders are never read.

> **Why the boxes are not a prescription.** A v3 export contained identical set-for-set entries repeated across four separate sessions (Lying Leg Curl 35 × 12 × 3 on 10.07, 21.07, 03.08, 10.08). The build of the time pre-filled a computed prescription and the checkmark saved it unedited, so part of the tonnage series was fictional. Since v10.3 the boxes are a record, not a suggestion.

---

## Deload mode

Settings → toggle. Sessions run at −40 % sets, same weights, RIR 3–4. Every 4 weeks, or on persistent joint pain or a 3-week stall. In-app triggers: bench or squat regression two sessions running, resting HR more than 5 bpm above baseline, sleep under 6 h for three nights.

---

## Zone 2

Calibrated 22 Aug 2026 (RHR ≈ 67, HRmax estimated 177, Tanaka — not measured directly).

**Working target: 118–133 bpm, hard cap 135.** Treadmill 6–6.5 km/h at 6–10 % incline, adjusting incline to hold 125–132; talk test = full sentences. 3 × 40 min on non-lifting days (Tue / Thu / Sat) = 120 min/week; 50 min sessions later. Never after lifting.

Logged as `type:'cardio'` workouts with duration and avg/max HR entered manually; the weekly total shows on the Gym tab and in Stats.

> Recalculate if resting HR shifts materially or HRmax is measured. An earlier build shipped 130–142, which is Zone 3 for this profile.

---

## Data model

IndexedDB, stores: `workouts`, `metrics`, `fasts`, `meals`, `labs`, `settings`, `entries` (legacy food entries, preserved but not displayed).

```js
// strength
{ date, type:'strength', sessionId, sessionName, startTs, endTs, deload?,
  exercises:[{ exId, name, targetSets, targetReps, rir, rest, unit, inc,
               wuSets:[{weight,reps,done}], sets:[{ weight, reps, done }] }] }

// metrics (v11.3 adds the optional circumference and BP keys)
{ date, weight?, waist?, muscleMass?, fatMass?, biceps?, forearm?, chest?, thigh?, calf?, sys?, dia?, pulse?, timestamp }

// cardio
{ date, type:'cardio', sessionId:'zone2', startTs, endTs, z2min, avgHR, maxHR,
  targetLo, targetHi }
```

Only confirmed sets are persisted — unchecked rows are stripped on finish.

### Exercise identity

Every exercise has a stable `exId` plus an alias list in the `EX` map, so renaming a display name does not orphan history (`Chest-Supported DB Row` → `One-Arm Machine Row` still resolves to `csRow`).

Changing the *name* keeps the history; changing the *equipment* should not. When a movement moves between cable, machine, dumbbell or barbell, give it a **new id** and leave the old one in the catalogue — as `dbFly` and `machLat` did in v11.2. Loads on different equipment are not a series.

---

## Export / import

**Settings → Export JSON** writes `healthy-life-YYYY-MM-DD.json`: workouts, metrics, fasts, meals, labs, settings, the exercise catalogue, the current program and the meal presets.

Import merges rather than overwrites: workouts are de-duplicated on `date|sessionId` (plus `startTs` for cardio), and existing metric fields win over imported ones. v2, v3 and v4 files all load.

**Export before every deploy.** IndexedDB is keyed to the origin, not the file, so data survives replacing `index.html` — verify it rather than assume it.

---

## Deploy

Copy `index.html`, `favicon.ico` and `apple-touch-icon.png` to the repo root on `main`. GitHub Pages publishes in 1–2 minutes.

The page sends `no-cache` headers, but iOS sometimes keeps the old version in memory: close the PWA from the app switcher and reopen. Confirm `2026-11-10-v11.4.2` in **Settings → Database contents**. If the home-screen icon does not change, remove the shortcut and add it again — iOS caches the icon at install time.

---

## Constraints and conventions

- Single file plus the two icons. No bundler, no npm, no external requests.
- Vanilla JS. No framework.
- Dark theme, neon green (`#39FF14`); blue (`#4aa3ff`) reserved for cardio.
- English throughout, sized for reading mid-set without glasses.
- **The repo is public.** Lab values, dates of birth and names stay in IndexedDB and in local exports — never in committed code or in this README.

---

## License

None. Personal project.
