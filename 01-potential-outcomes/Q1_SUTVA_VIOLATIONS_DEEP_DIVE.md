# 🎯 SECTION 1, QUESTION 1: SUTVA VIOLATIONS IN PRACTICE
## Meta Interview Question (Real Problem, Real Solution)

---

## THE QUESTION (Paraphrased from Meta)

> "You're running an experiment at Meta where you randomly show Ad Creative A vs Creative B to users in their feed. 50% get A, 50% get B. You measure: Did user click on ad?
>
> Problem: Your friend sees Ad A. You see Ad B. But your friend's engagement with Ad A appears in your feed (as their social signal). Does this violate the assumptions of a standard A/B test? How do you design around it?"

---

## PART 1: WHAT IS SUTVA?

### Definition (Simple)
**SUTVA = Stable Unit Treatment Value Assumption**

This is NOT one assumption. It's TWO assumptions packed together:

```
SUTVA = Part 1 (Well-Defined) + Part 2 (No Interference)
```

### Part 1: Well-Defined Treatment
**Question**: Is the treatment clear and unambiguous?

**Example: Medical Trial**
```
Treatment: Give drug A to patient
✅ SUTVA Part 1 satisfied: Drug A is well-defined, dose is fixed, timing is fixed
```

**Example: Netflix Recommendation**
```
Treatment: Show recommended movies to user
❌ SUTVA Part 1 VIOLATED: What IS "recommendation"?
   - Is it the algorithm version? (V1 vs V2)
   - Is it the ranking? (Top 5 vs Top 10)
   - Is it the genre? (Action vs Comedy)
   - Different users might get DIFFERENT treatments under the same "recommendation"
```

### Part 2: No Interference (EXCLUSION PRINCIPLE)
**Question**: Does one unit's treatment affect another unit's outcome?

**Core idea**: 
```
Unit A's outcome should depend ONLY on Unit A's treatment
NOT on what treatment Unit B received

Y_A depends on: T_A (A's treatment)
Y_A does NOT depend on: T_B (B's treatment)
```

---

## PART 2: NETFLIX EXAMPLE (YOU SPOTTED THIS!)

### The Setup
```
Netflix ML experiment:
- 50% of users get Recommendation Algorithm V1
- 50% of users get Recommendation Algorithm V2
- Measure: Click-through rate (CTR) on recommended titles
```

### Why SUTVA Part 2 is VIOLATED

**Scenario**:
```
User A (gets Algorithm V1) watches "Stranger Things"
  ↓
User A posts to their friends: "Just watched Stranger Things, awesome!"
  ↓
User B (gets Algorithm V2) sees this in their social feed
  ↓
User B's CTR is INFLUENCED by what User A watched
  ↓
User B's outcome Y_B now depends on User A's treatment T_A
  ↓
SUTVA VIOLATED ❌
```

### The Interference Graph
```
Treatment:     T_A (Algo V1)  →  T_B (Algo V2)
                    ↓              ↓
                    ↓ (feedback)   ↓
Spillover:     Social signal  ← Interaction
                    ↓              ↑
                    ↓              ↓
Outcome:           Y_A  ←────────  Y_B
                (influenced)  (influenced)

PROBLEM: Y_A depends on T_B (interference) AND Y_B depends on T_A
```

### Real Netflix Metrics
```
CTR = Click-through rate
Watch time = How long they watch
Rating = Star rating given
Completion = Did they finish?

ALL of these can be influenced by other users' recommendations
because Netflix is a NETWORK (users affect each other via social signals)
```

---

## PART 3: UBER SURGE PRICING EXAMPLE (YOUR INTUITION)

### The Setup
```
Uber experiment:
- 50% of drivers get Surge Pricing active
- 50% of drivers get Normal Pricing
- Measure: Did driver accept the ride? (Y = 1 if accepted, 0 if not)
```

### Why SUTVA Part 2 is VIOLATED (Cannibalization)

**Scenario**:
```
Driver A (surge pricing active) sees request at $20 surge
  ↓
Driver A hesitates ("price is high")
  ↓
Driver B (normal pricing) sees SAME request at $12
  ↓
Driver B accepts
  ↓
Driver A's outcome Y_A is influenced by Driver B being in the pool
  ↓
Driver B's outcome Y_B is influenced by Driver A not competing
  ↓
SUTVA VIOLATED ❌
```

### The Interference Graph (Competitor Pool)
```
Treatment:        T_A (Surge)     T_B (Normal)
                    ↓              ↓
                    ↓ (same request pool)
Spillover:    Request competes  Request competes
              for Driver A        for Driver B
                    ↓              ↓
Outcome:          Y_A  ←────────  Y_B
             (affected by pool) (affected by pool)

PROBLEM: A's decision to accept affects B's opportunity to accept
         and vice versa. They're competing for the same requests.
```

### Real Uber Metrics (What's Measured)
```
Acceptance rate = % of requests driver accepted
Earnings = Total $ earned that day
Trip completion = Did trip actually happen?
Driver satisfaction = Did driver mark positive?

ALL affected by:
- Competitive dynamics (surge creates queues)
- Cannibalization (cheap drivers steal surge drivers' requests)
- Network effects (overall driver supply affects ALL drivers' acceptance)
```

---

## PART 4: NETFLIX vs UBER - DIFFERENT INTERFERENCE TYPES

| Aspect | Netflix | Uber |
|--------|---------|------|
| **Interference Type** | INDIRECT (social network) | DIRECT (competitive pool) |
| **Path** | User A posts → User B sees in feed | Driver A rejects → Driver B gets request |
| **Who's Affected** | Treated affects untreated | Treated affects untreated |
| **Observable?** | Hard to see spillover | Easy to see spillover |
| **Severity** | LOW to MEDIUM (depends on social graph size) | HIGH (immediate effect) |
| **Fix Difficulty** | HARD (social graph is complex) | MEDIUM (geographic/temporal separation) |

---

## PART 5: HOW TO FIX UBER SURGE PRICING - DESIGN OPTIONS

### Option 1: Geographic Stratification ✅ (BEST)
```
Design:
- San Francisco City: Apply surge to ALL drivers
- Oakland City: No surge to ANY drivers
- Distance: > 50 miles (no overlap)

Why it works:
✅ Users in SF only book SF drivers (no cannibalization)
✅ Drivers in SF not competing with Oakland drivers
✅ No interference between treatment/control groups
✅ Clear treatment vs control

Challenges:
- Need to ensure cities have similar demand patterns
- Day of week effects (SF might be busier than Oakland)
- Season effects (holiday patterns differ)

Solution: Match cities on:
  - Historical demand curve
  - Driver density
  - Weather patterns
  - Day of week
```

### Option 2: Temporal Stratification ⚠️ (RISKY)
```
Design:
- Monday-Tuesday: Apply surge to all drivers
- Wednesday-Thursday: No surge to any drivers
- Measure acceptance rate each day

Why it DOESN'T work:
❌ User behavior differs by day (Monday vs Wednesday)
❌ Weather affects acceptance (different days have different weather)
❌ Event-driven demand (concert Monday, quiet Wednesday)
❌ Driver habits (part-time drivers work different days)

So your effect is confounded with day-of-week effect:
  Effect = Surge effect + Day-of-week effect (mixed)

Unless you control for these with regression, this is biased.
```

### Option 3: Time-of-Day Stratification ✅ (ALSO GOOD)
```
Design:
- Morning (6am-12pm): Apply surge to all drivers
- Evening (6pm-12am): No surge to any drivers
- Keep days constant (same day, different times)

Why it works:
✅ Same drivers available both times (no personnel changes)
✅ Same underlying demand (same day, just different hours)
✅ No cross-time cannibalization (morning users ≠ evening users)

Challenges:
- Peak hours might differ (morning rush vs evening rush)
- Driver availability differs (some drivers only work mornings)

Solution: Use same-hour on different days and geographic split
```

### Option 4: User-Side Treatment ✅ (BEST IF POSSIBLE)
```
Design:
Instead of treating drivers, treat USERS:
- 50% of users: Charged surge price
- 50% of users: Never charged surge (control)

Why it works:
✅ No driver pool interference (all drivers available to all users)
✅ Pure effect: Does surge affect user booking?
✅ Cleaner SUTVA

Challenge:
- User side: If User A sees surge, does User B get affected? (NO)
- Because User B isn't competing for same driver

But:
- Demand side interference: If all A-users don't book (due to surge),
  then driver supply drops for B-users
- Still need to be careful
```

---

## PART 6: WHAT META ACTUALLY CARES ABOUT (In Ad Experiments)

### Meta's Real SUTVA Violations

**The Social Network Problem**:
```
You show Ad Creative A to User X
  ↓
User X clicks and interacts with brand (e.g., follows page)
  ↓
Your friend Y sees User X's interaction in their news feed
  ↓
Friend Y is now MORE LIKELY to click similar ads (viral effect)
  ↓
Friend Y's outcome is influenced by User X's treatment
```

**Meta's Design Solution**:
1. **Cluster Randomization**: Randomly assign entire friend clusters (not individuals)
   - If User X assigned to A, all their close friends stay in same experimental condition
   - Reduces interference within clusters

2. **Geographic Cluster Randomization**: 
   - Randomize by country/region instead of by user
   - Ad A shown to all users in Germany
   - Ad B shown to all users in France
   - Reduces cross-border interference

3. **Time-Window Randomization**:
   - Week 1: Show Ad A to all users
   - Week 2: Show Ad B to all users (new users who didn't see Week 1)
   - Reduces temporal interference

4. **Burn-In Period**:
   - Run experiment for 2-3 weeks before measuring
   - Let social network effects stabilize
   - Then measure (effects are consistent)

---

## PART 7: KEY INSIGHT - When to Worry About SUTVA

### High Risk (Definitely Violates SUTVA Part 2):
```
✅ Social networks (Facebook, Twitter, LinkedIn, TikTok)
✅ Marketplace experiments (Uber, Airbnb, DoorDash - supply/demand pools)
✅ Peer effects (one user's choice affects group)
✅ Capacity constraints (limited inventory)
✅ Reputation systems (one person's rating affects others' choices)
```

### Low Risk (Probably Safe):
```
✅ Medical trials (patients don't interact)
✅ Email experiments (users don't share treatment info)
✅ Website A/B tests (different users, different sessions)
✅ Recommendation engines (if no social feedback loop)
```

### How to Detect:
```
Ask yourself: "If User/Driver A gets treatment T_A,
does this DIRECTLY or INDIRECTLY affect User/Driver B's outcome?"

If YES → SUTVA violated, fix it
If NO → SUTVA probably OK (but check other assumptions)
```

---

## PART 8: DECISION TREE - Fix Your SUTVA Problem

```
START: You suspect SUTVA violation

   1. What type of interference?
      ├─ Social network effects?
      │  └─ FIX: Cluster randomization OR geographical split
      │
      ├─ Competitive pooling?
      │  └─ FIX: Geographical split OR user-side treatment
      │
      └─ Temporal spillover?
         └─ FIX: Time-of-day split OR long burn-in period

   2. Can you spatially separate?
      ├─ YES → Geographic randomization (BEST)
      │
      └─ NO:
         ├─ Can you temporally separate?
         │  ├─ YES → Time-of-day OR different dates
         │  │
         │  └─ NO:
         │     └─ Use cluster randomization
         │        (group similar units together)

   3. Implement & Validate:
      ├─ Check: No spillover between treatment/control?
      ├─ Check: Comparable pre-treatment characteristics?
      └─ ONLY THEN: Measure your causal effect
```

---

## PART 9: CODE EXAMPLE - Detecting SUTVA Violations

### Scenario: Uber Surge Pricing
```python
# Data: Drivers, their treatment, their acceptance
import pandas as pd
import numpy as np

# Simulated data
df = pd.DataFrame({
    'driver_id': range(1, 101),
    'treatment': np.random.binomial(1, 0.5, 100),  # Surge (1) vs Normal (0)
    'accepted': np.random.binomial(1, 0.6, 100),   # Did they accept? 
    'geographic_region': ['SF', 'SF', 'Oakland', 'Oakland'] * 25,
})

# RED FLAG: Check if treatment in one region affects outcomes in another region
control_drivers_sf = df[(df['treatment']==0) & (df['geographic_region']=='SF')]['accepted'].mean()
treatment_drivers_sf = df[(df['treatment']==1) & (df['geographic_region']=='SF')]['accepted'].mean()

control_drivers_oakland = df[(df['treatment']==0) & (df['geographic_region']=='Oakland')]['accepted'].mean()
treatment_drivers_oakland = df[(df['treatment']==1) & (df['geographic_region']=='Oakland')]['accepted'].mean()

print(f"SF Control Acceptance: {control_drivers_sf:.2%}")
print(f"SF Treatment Acceptance: {treatment_drivers_sf:.2%}")
print(f"Oakland Control Acceptance: {control_drivers_oakland:.2%}")
print(f"Oakland Treatment Acceptance: {treatment_drivers_oakland:.2%}")

# If acceptance rates are very different between regions,
# it suggests confounding, not pure treatment effect
# (SUTVA violated + other confounders)
```

### Detecting Interference via Request-Level Data
```python
# Better: Use request-level data
# For each request, check: Did treatment affect competing drivers?

requests = pd.DataFrame({
    'request_id': range(1, 101),
    'driver_a_id': range(1, 51),
    'driver_b_id': range(51, 101),
    'driver_a_treatment': np.random.binomial(1, 0.5, 100),
    'driver_b_treatment': np.random.binomial(1, 0.5, 100),
    'driver_a_accepted': np.random.binomial(1, 0.6, 100),
    'driver_b_accepted': np.random.binomial(1, 0.6, 100),
})

# INTERFERENCE CHECK:
# If driver_a has surge (T=1) and accepts, does driver_b have lower acceptance?

surge_drivers_who_accepted = requests[
    (requests['driver_a_treatment']==1) & 
    (requests['driver_a_accepted']==1)
]['driver_b_accepted'].mean()

surge_drivers_who_rejected = requests[
    (requests['driver_a_treatment']==1) & 
    (requests['driver_a_accepted']==0)
]['driver_b_accepted'].mean()

print(f"Driver B acceptance when A (surge) accepted: {surge_drivers_who_accepted:.2%}")
print(f"Driver B acceptance when A (surge) rejected: {surge_drivers_who_rejected:.2%}")

# If these are DIFFERENT, there's INTERFERENCE
# (A's acceptance affects B's acceptance - SUTVA violated)
```

---

## PART 10: YOUR META INTERVIEW ANSWER

### What They're Testing:
1. Do you recognize SUTVA violations? (YES ✅)
2. Can you explain WHY it's violated? (Interference mechanism)
3. Can you propose a FIX? (Design solution)
4. Do you understand tradeoffs? (Geographic vs Temporal vs Cluster)

### Your Answer Framework:

```
"Yes, this violates SUTVA Part 2 (No Interference) because:

1. MECHANISM: User A gets Ad Creative A → User A engages 
   → User A's engagement shows up in their friends' feeds 
   → Friend B's engagement is now influenced by A's treatment
   → This means Y_B depends on T_A (interference)

2. WHY IT MATTERS: A standard t-test assumes:
   E[Y_i(1)] - E[Y_i(0)] is the pure treatment effect
   But if Y_B(1) is affected by A's treatment, this breaks down

3. DETECTION: Run A/B test → If you see spillover effects
   (control users in friend network perform differently),
   that's evidence of SUTVA violation

4. HOW TO FIX:
   BEST: Cluster randomization (randomize friend clusters, not individuals)
   WHY: Keeps interfering units in same treatment condition
   
   ALTERNATIVE: Geographic split (different countries)
   WHY: No cross-country social network effects
   
   NOT RECOMMENDED: Individual randomization without spillover control
   WHY: Biased effect estimates

5. VALIDATION:
   - Check covariate balance in treatment/control (should be equal)
   - Run A/A test (no treatment, should see no difference)
   - Check for spillover correlations in treatment/control groups
   - If clusters used: verify randomization was at cluster level"
```

