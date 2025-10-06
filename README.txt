# Calisthenics Coach — Project Overview (Steve & Rosie)

## 1) Product vision

A mobile-first coach that builds **personalized calisthenics plans** from a short assessment, adapts to schedule (2–6 days/wk), and shows **percent-progress** toward big skills (e.g., **muscle-up, planche, front lever, handstand push-up**). Progress bars rise when you hit **evidence-based milestones** across **primary** and **supporting** qualities (pull, push/dip, core, technique, mobility), not just arbitrary badges.

---

## 2) Primary users & constraints

* **Users:** Steve & Rosie (beginner→intermediate calisthenics), iPhone/Android.
* **Constraints:** Minimal equipment (bar, rings, floor, parallettes). Sessions 30–60 min. Needs **variety** (no copy‑paste workouts).

---

## 3) Target skill library ("end‑goal" calisthenics skills)

> The app treats these as long‑term goals with milestone graphs and percent completion.

**Upper/Bar/Rings**

* Muscle‑up (bar), Muscle‑up (rings)
* One‑arm pull‑up / chin‑up
* Front lever (tuck → advanced tuck → straddle → full)
* Back lever (tuck → straddle → full)
* Human flag (tuck → straddle → full)
* L‑sit → V‑sit → Manna (advanced)
* Dragon flag
* Skin‑the‑cat (full ROM control)
* Hefesto (very advanced, optional)

**Push/Balance**

* Freestanding handstand (wall → free; 10–30s+)
* Handstand push‑up (pike → wall HSPU → free HSPU)
* 90‑degree push‑up / bent arm press
* Planche (tuck → advanced tuck → straddle → full)
* One‑arm push‑up

**Legs**

* Pistol squat / shrimp squat (assisted → full → weighted)

**Rings strength (optional advanced)**

* Ring support (60s), ring dip (deep), Iron cross / Maltese / Victorian (very advanced; optional database entries)

---

## 4) Foundational movement library (beginner → intermediate)

**Push**: incline push‑up, knee push‑up, standard push‑up, pseudo‑planche push‑up (PPP), pike push‑up, ring push‑up, parallel‑bar dip, straight‑bar dip, ring dip (support, tempo, eccentric).

**Pull**: active hang, scapular pulls, inverted rows (feet in/out), chin‑ups, pull‑ups, chest‑to‑bar, eccentrics, band‑assisted, high pulls, false‑grip hangs; ring rows.

**Core**: hollow/arch holds, dead bug, plank/side plank, hanging knee raise, hanging leg raise to 90°, toes‑to‑bar, L‑sit (tuck → full), compression drills.

**Legs**: air squat, tempo squat, reverse lunge, step‑up, assisted single‑leg squat to box, shrimp squat progressions, calf raises.

**Mobility & scapular control**: shoulder flexion/extension (PVC pass‑throughs), thoracic extension, hip flexor/hamstring/ankle mobility; scapular depress/retract/protract/elevate drills.

**Skill‑bridge drills**: jumping muscle‑up, banded muscle‑up, low‑ring transition, false‑grip transitions, wall handstand holds/walkouts, kick‑ups, wall HSPU eccentrics.

---

## 5) Assessment protocol (10–15 minutes)

**Purpose:** Quantify baseline across push, pull, core, legs, mobility, and skill readiness. Produces normalized scores (0–1) → feeds goal percentages & initial plan.

**Scoring:** For each test, record best set **with strict form**. Convert to a normalized **score = clamp(value / target, 0, 1)**. Targets are conservative beginner/intermediate anchors.

### 5.1 Push

1. **Max strict push‑ups** (target 25)
2. **Max parallel‑bar dips** (target 12)
3. **Pike push‑ups (hips over hands)** reps (target 12)
4. **Ring support hold** (target 30s)

### 5.2 Pull

1. **Active hang** (target 60s)
2. **Scapular pull‑ups** (target 12)
3. **Max strict pull‑ups** (target 10)
4. **Chest‑to‑bar pull‑ups** reps (target 5)
5. **Eccentric pull‑up** 5s tempo × 3 reps (Y/N)

### 5.3 Core

1. **Hollow body hold** (target 60s)
2. **Hanging knee raises** reps (target 12)
3. **L‑sit tuck hold** (target 20s)

### 5.4 Legs

1. **Air squat** max in 60s (target 40)
2. **Assisted pistol** to box (Y/N + depth)
3. **Calf raise** 20/side (target 20)

### 5.5 Mobility/Balance

1. **Shoulder flexion** overhead without rib flare (pass/fail/needs work)
2. **Thoracic extension** wall test (pass/needs work)
3. **Ankle dorsiflexion** knee‑to‑wall distance (cm)
4. **Single‑leg balance** (eyes open) (target 30s/side)

### 5.6 Skill readiness checks (binary or time)

* **Wall handstand hold** 30–60s
* **False‑grip hang** 10–30s
* **Low‑ring transition drill** 5 smooth reps

**Output:** Normalized sub‑scores: `push`, `pull`, `core`, `legs`, `mobility`, `skill_readiness` ∈ [0,1]. Store raw metrics too.

---

## 6) Schedule input & training templates

* User selects **days/week** (2–6), available time (30/45/60 min), equipment, and **preference for variety**.
* App chooses a template:

  * **3 days/wk (example)**:

    * **Day A (Push + Legs + Skill)**
    * **Day B (Pull + Core)**
    * **Day C (Mixed Skill + Full‑body)**
  * 2d/wk (upper/lower), 4d/wk (push/pull/legs/skill), 5–6d/wk (split with micro‑skills daily).
* Includes **progression rules** (volume up 5–10%/wk, deload week 4 or auto‑deload if RPE >9 or reps fall >20%).

---

## 7) Variety engine

* Each workout slot uses a **movement family** with **rotations**:

  * Push slot: **push‑up → ring push‑up → PPP → pike push‑up → dips (bars) → straight‑bar dips**
  * Pull slot: **rows → band chin‑ups → pull‑ups → chest‑to‑bar → high pulls**
  * Core slot: **hollow → hanging knees → leg raise → L‑sit (tuck)**
  * Skill slot: **false‑grip, transition, wall HS, kick‑ups, band MU**
* **Session flavors** (auto‑rotate): straight sets, EMOM, AMRAP (cap), tempo work, density blocks.
* Keeps novelty while training the same qualities.

---

## 8) Goal engine & percent‑progress model

**Principles**

* Each “end skill” has **weighted components**. Hitting milestones in any component raises the goal’s progress bar.
* Percentages are **evidence‑informed heuristics**, adjustable per user data.
* **Normalized scoring** per component: convert reps/holds/weights to 0–1, multiply by component weight.

### 8.1 Muscle‑up (bar) — component weights

* **Pulling strength & power** – **40%**
* **Dip/press strength** – **30%**
* **Technique/transition** – **15%**
* **Core & scapular control** – **15%**

> Total = 100%. Each component is distributed across granular milestones (below). The app sums achieved items (capped at the component’s max).

### 8.2 Muscle‑up milestones → percent allocation

**A) Pulling (40%)**

* Strict pull‑ups (best set): 0→10 reps maps **0→36%** of total (approx):
  0r=0%, 1=3%, 2=6%, 3=9%, **4=12%**, 5=16%, 6=20%, 7=24%, 8=28%, 9=32%, 10=36%
* Chest‑to‑bar 5 reps: **+2%** (cap if already strong)
* High pull (bar at lower chest) ×3: **+2%**

> Pulling cap **= 40%**

**B) Dip/press (30%)**

* Parallel‑bar dips 0→15 reps maps **0→18%**: 0=0%, 5=6%, 10=12%, **15=18%**
* Weighted dip **+10% BW ×5**: **+6%**
* Straight‑bar dips ×10: **+6%**

> Dip/press cap **= 30%**

**C) Technique/transition (15%)**

* False‑grip hang 30s: **+3%**
* Low‑ring transition drill ×5 smooth reps: **+4%**
* Banded bar MU (light band) ×3: **+4%**
* Jumping bar MU ×5 (clean turnover): **+4%**

> Technique cap **= 15%** (sum capped)

**D) Core & scapular (15%)**

* Hollow body hold 60s: **+5%**
* Scapular pull‑ups ×10: **+3%**
* Toes‑to‑bar ×8: **+4%**
* Hanging leg raise to 90° ×8: **+3%**

> Core/scap cap **= 15%** (sum capped)

**Starting from Steve’s example:**
If current best is **4 strict pull‑ups**, progress = **12%** of the full 100% (other components unscored yet). As you add dips/core/technique milestones, your MU bar climbs even before your pull‑ups jump—reflecting real cross‑over adaptations.

**Computation (pseudocode)**

```pseudo
function muscleUpProgress(userMetrics):
  p = pullComponent(userMetrics)      // 0..40
  d = dipPressComponent(userMetrics)  // 0..30
  t = techniqueComponent(userMetrics) // 0..15
  c = coreScapComponent(userMetrics)  // 0..15
  return min(100, p + d + t + c)
```

---

## 9) Example 3‑day/week plan (beginner, 45–60 min, with variation)

**Day A – Push + Legs + Skill (Tempo focus)**

* Warm‑up: 5–7 min (shoulders, wrists, hips), scapular control
* A1) **Push‑up** (or incline) 4×6–10 @3010 tempo, rest 60–90s
* A2) **Air squat** 4×12–15 @2111 tempo (pair with A1)
* B) **Parallel‑bar support hold** 3×20–30s
* C) **Pike push‑up** 3×6–8
* D) **Skill block** (10 min): false‑grip hang practice + low‑ring transitions
* Finisher: **Hollow hold** 3×20–40s

**Day B – Pull + Core (Density block)**

* Warm‑up + hanging mobility 5 min
* A) **Row or band‑assist chin‑up** 5×6–10 (every 75s)
* B) **Scapular pull‑ups** 4×8–10
* C) **Hanging knee raises** 4×8–12
* D) **Hip hinge / reverse lunge** 3×10/side
* Skill: **High pull drill** 6×1–3 (quality reps)

**Day C – Mixed Skill + Full‑body (EMOM)**

* EMOM 18 min (rotate 6 rounds):

  1. Push slot: ring push‑ups 6–10
  2. Pull slot: inverted rows 8–12
  3. Core slot: L‑sit tuck hold 10–20s
* Add 10 min **technique**: banded muscle‑up practice (light band), 4–6 sets of 2–3 smooth reps
* Cooldown & mobility 5 min

**Weekly progression rules**

* Add 1–2 reps **or** an extra set **or** increase time‑under‑tension/tempo.
* If RPE ≥9 for 2+ sets, keep same prescription next week.
* **Retest** key metrics every 4–6 weeks (or when app detects consistent PRs).

---

## 10) Program generator (MVP logic)

Input: assessment metrics, schedule (days/wk), available time, selected **primary goal(s)**.
Output: 4‑week microcycle plan with day templates + auto‑rotating variants + technique work aligned to goals.

**Heuristics**

* If **muscle‑up** selected, guarantee per week:

  * 2× pull strength exposures
  * 1–2× dip/press exposures
  * 2× core/scap exposures
  * 1× technique/transition block
* Volume scaled by `pull` and `push` assessment scores (lower scores → more sub‑max, higher frequency practice; higher scores → lower reps, higher intensity/tempo/weighted progressions).

---

## 11) Data model (draft)

```json
// Movement taxonomy
{
  "id": "pull_up_strict",
  "family": "pull",
  "level": "beginner_to_intermediate",
  "prereqs": ["active_hang", "scap_pull"],
  "metrics": { "type": "reps", "best_set": true },
  "progressions": ["band_chin_up", "eccentric_pull_up", "chin_up", "pull_up"]
}
```

```json
// Goal definition (muscle-up)
{
  "id": "goal_muscle_up_bar",
  "weights": { "pull": 40, "dip": 30, "tech": 15, "core": 15 },
  "milestones": {
    "pull": [
      {"metric": "pull_up_strict_best", "map": [[0,0],[1,3],[2,6],[3,9],[4,12],[5,16],[6,20],[7,24],[8,28],[9,32],[10,36]]},
      {"metric": "chest_to_bar_5reps", "value": true, "gain": 2},
      {"metric": "high_pull_3reps", "value": true, "gain": 2}
    ],
    "dip": [
      {"metric": "parallel_dip_best", "map": [[0,0],[5,6],[10,12],[15,18]]},
      {"metric": "weighted_dip_10pctBWx5", "value": true, "gain": 6},
      {"metric": "straight_bar_dip_10", "value": true, "gain": 6}
    ],
    "tech": [
      {"metric": "false_grip_30s", "value": true, "gain": 3},
      {"metric": "low_ring_transition_5smooth", "value": true, "gain": 4},
      {"metric": "banded_mu_light_3", "value": true, "gain": 4},
      {"metric": "jump_mu_5_clean", "value": true, "gain": 4}
    ],
    "core": [
      {"metric": "hollow_60s", "value": true, "gain": 5},
      {"metric": "scap_pullups_10", "value": true, "gain": 3},
      {"metric": "toes_to_bar_8", "value": true, "gain": 4},
      {"metric": "hanging_leg_raise_90deg_8", "value": true, "gain": 3}
    ]
  },
  "caps": {"pull": 40, "dip": 30, "tech": 15, "core": 15}
}
```

```json
// Session log
{
  "user_id": "steve",
  "date": "2025-10-05",
  "movements": [
    {"id":"pull_up_strict", "sets":[{"reps":4},{"reps":3},{"reps":2}]},
    {"id":"parallel_dip", "sets":[{"reps":5},{"reps":5}]}
  ],
  "notes": "Felt good; band MU technique smoother",
  "rpe_avg": 7
}
```

---

## 12) Algorithms (pseudocode)

**12.1 Percent progress update**

```pseudo
function updateGoalProgress(goalDef, userMetrics):
  total = 0
  for component in goalDef.milestones:
    gained = 0
    for m in component:
      if m.map exists:
        gained = max(gained, interpolateMap(m.map, userMetrics[m.metric]))
      else if userMetrics[m.metric] == m.value:
        gained += m.gain
    total += min(gained, goalDef.caps[component])
  return min(total, 100)
```

**12.2 Plan generator (3d/wk template)**

```pseudo
function buildWeek(schedule, assessment, goals):
  days = schedule.daysPerWeek // e.g., 3
  template = [DayA, DayB, DayC]
  scale = volumeScale(assessment) // lower scores -> more practice sets
  for i in 1..days:
    day = template[i]
    plan[i] = assembleDay(day, goals, scale, varietySeed=i)
  return plan
```

**12.3 Variety rotation**

```pseudo
function nextVariant(family, weekIdx):
  variants = registry[family]
  return variants[weekIdx % len(variants)]
```

---

## 13) UX flows (MVP)

**Onboarding** → `Assessment` (guided timers, strict form videos) → `Schedule` (days/time/equipment) → `Select end goals` → `Plan preview` (4‑week microcycle) → `Start Workout`.

**Home/Dashboard**:

* Today’s session card, streak, recovery tip
* **Goal progress bars** (e.g., Muscle‑up 12% → 18% this week)
* Milestones unlocked list (with what moved the needle)

**Workout screen**: set/rep timers, technique video thumbnails, RPE slider, substitution button (keep quality), rest countdown.

**Post‑workout log**: PR detection, prompt to update milestone metrics (e.g., “New best: dips ×10?”), auto‑recompute goal percentages.

**Progress**: graphs (reps/holds over time), milestone badges (real milestones, not gimmicks), retest scheduler.

---

## 14) Technical stack (suggested)

* **App**: React Native + Expo (TypeScript) for iOS/Android.
* **Logic service**: Python **FastAPI** microservice (progress calc + plan generation).
* **Storage**: Local SQLite (offline‑first) + optional cloud sync (Supabase/Postgres).
* **Auth/share**: private accounts + **partner sync** (Steve ↔ Rosie shared goals/PRs).
* **Analytics**: lightweight local; optional export to Apple Health/Google Fit (future).

**Project structure**

```
app/
  screens/
  components/
  state/
  data/
server/
  main.py (FastAPI)
  planner.py
  goals.py
  models.py
```

---

## 15) Safety & coaching rules

* Master **strict form**; use controlled eccentrics before adding bands/weights.
* Cap sets near **RPE 7–8**; avoid repeated grindy singles.
* Deload or rotate variants on elbow/shoulder irritation; emphasize **scapular control** and wrist prep.

---

## 16) Roadmap

**MVP (2–3 sprints)**

1. Assessment flow + normalization + local storage.
2. Goal engine (muscle‑up only) with percent progress + dashboard bars.
3. 3‑day template generator + variety engine + workout logger.
4. Retest flow + simple analytics.

**v1.1**: Add front lever, handstand, pistol goal models; technique video library; partner sharing.
**v1.2**: Weighted progressions, deload detection, RPE auto‑regulation.
**v1.3**: Health integrations, notifications, habit scaffolding.

---

## 17) Open questions

* Preferred **video cue** style (quick 15–30s clips vs. step‑by‑step)?
* Do we want **autoregressive goals** (e.g., picking 2 primaries max to avoid dilution)?
* How aggressively should the app adjust the plan after a missed week?
* Include **rings** by default or as an optional equipment toggle?

---

## 18) Example: applying Steve’s baseline (4 strict pull‑ups)

* Pulling component instantly grants **12%** (per mapping).
* Early gains without more pull‑ups: hit **dips ×10** (+12% of total over time), **hollow 60s** (+5%), **scap pulls ×10** (+3%), and **low‑ring transitions ×5** (+4%).
* That path could bring you from **12% → 36–40%+** even before you reach 6–7 pull‑ups, keeping motivation high while addressing real prerequisites.

---

### Done. This is ready to build.
