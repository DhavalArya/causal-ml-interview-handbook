# 🎓 TIER 1 FOUNDATION: CAUSATION vs CORRELATION
## The #1 Reason Causal ML Exists

---

## CONCEPT 1: CAUSATION vs CORRELATION

### 🧠 INTUITION FIRST (No Math)

**The Problem:**
```
You observe: People who drink coffee have higher productivity
Conclusion:  Coffee causes higher productivity ❌ WRONG!

Alternative explanation: 
- Productive people drink MORE coffee (reverse causation)
- Night-shift workers drink coffee AND work late (both high productivity)
- Morning people are naturally alert, coffee just habit (spurious correlation)

The Root Issue:
Correlation: X and Y move together in data
Causation: X → Y means changing X causes Y to change
```

**A Classic Example:**
```
OBSERVATION: Ice cream sales ↑ in summer, Drowning deaths ↑ in summer
CORRELATION: Ice cream sales strongly correlated with drowning deaths

NAIVE CONCLUSION: Ice cream causes drowning! Ban ice cream! ❌

REAL CAUSATION: 
Temperature is the confounder (common cause)
  Temperature → ↑ Ice cream sales
  Temperature → ↑ Beach visits → ↑ Drowning risk

So the causal graph is:
  Temperature
      ↙        ↘
Ice cream    Drowning
(correlated, but NOT causal)
```

---

### 📖 FORMAL DEFINITION

**Correlation:**
```
Corr(X, Y) = statistical measure of joint movement
Range: -1 to +1
- Corr = 1: perfect positive movement (X↑ then Y↑)
- Corr = 0: no linear relationship
- Corr = -1: perfect negative movement (X↑ then Y↓)

Example: Corr(coffee, productivity) = 0.45
"People who drink coffee are 45% more likely to be productive than average"
```

**Causation:**
```
X causes Y if: Intervening on X (forcing X to change)
              directly results in Y changing

Example: Causation(coffee → alertness)?
Test: Force someone to drink coffee (intervene)
      → Does their alertness increase directly from coffee?
      → If YES: Causation exists
      → If NO: Only correlation

Notation: 
  Corr(X, Y) is observable in data
  Causal(X → Y) requires intervention (experimental or design trick)
```

**Key Difference:**
```
CORRELATION (observational):
- "What happened in the data?"
- Can compute from passive observation
- Can be spurious (misleading)

CAUSATION (interventional):
- "What would happen if we forced a change?"
- Requires experiment, randomization, or clever design
- Tells you if changing X actually changes Y
```

---

### 🎯 WHY IT MATTERS (Business Impact)

**Scenario 1: Wrong Causation Cost**
```
SCENARIO: Your boss sees correlation between:
  "Users who use mobile app X" ↔ "High churn"
  
NAIVE DECISION: "Delete the app! It causes churn!"
  → Spend $2M rebuilding
  → Roll out update removing app
  → Churn stays same (or worse)
  
WHY IT FAILED:
  Real causal graph:
    High Churn (already at risk)
      ↙           ↘
    Mobile app    Bad LTV
    (symptom)     (cause)
  
  Mobile app usage wasn't the cause, it was a symptom
  (Users churn anyway, so they stop using app before leaving)
```

**Scenario 2: Right Causation Works**
```
SCENARIO: Another team finds that:
  "Users who upgrade to premium" → "Higher engagement"
  
CORRECT THINKING:
  Is this causal or just correlation?
  → Run A/B test: Force upgrade vs no upgrade
  → Measure engagement for each group
  → If treated group has higher engagement: CAUSAL ✅
  → Decision: "Offer more premium upgrades"
  
RESULT: +15% engagement, +$3M ARR
```

**Why This Matters at MLE Level:**
```
As an MLE building causal systems:
- Wrong causation → Model predicts incorrectly
- Wrong causation → Policy recommendations backfire
- Wrong causation → Business metrics don't improve

Your job:
1. Identify real causal relationships (not correlations)
2. Build models that exploit those relationships
3. Validate in A/B tests (ground truth of causation)
4. Deploy with confidence that it works
```

---

### 🔍 HOW TO DETECT

**Test 1: Time Order (Necessary but Not Sufficient)**
```
Rule: Cause must come BEFORE effect

Example: Does coffee cause alertness?
✅ Time order OK: 
   1. Drink coffee (T=0)
   2. Wait 20 minutes (T=20)
   3. Measure alertness (T=20)
   Coffee came before alertness ✓

❌ Time order VIOLATED:
   Someone is alert, then they drink coffee
   (Alertness came first - can't be causal)
```

**Test 2: Plausible Mechanism (Necessary but Not Sufficient)**
```
Question: "Is there a believable chain of events from X to Y?"

Example: Does social media use cause depression?

Plausible mechanism ✅:
  Social media use
    ↓ (scrolling feeds, comparing to others)
    ↓ (FOMO, social comparison)
    ↓ (negative emotion)
    → Depression

So mechanism is plausible, but we need experiments to confirm

Counter-example: Does wearing shoes cause poverty?
  Time order: Shoes worn before poverty measured ✓
  But mechanism: How would shoes → poverty?
  No plausible mechanism ✗ (probably reverse: poor → can't afford shoes)
```

**Test 3: Experimental Manipulation (Gold Standard)**
```
The ONLY way to prove causation:
1. Randomly assign X (treatment)
2. Measure Y (outcome)
3. If treated group's Y ≠ control group's Y → CAUSAL ✓

Example: Does coffee cause alertness?
  Random assignment:
    - Group A: Given coffee
    - Group B: Given water (placebo)
    - Measure alertness after 20 min
    - If A_alertness > B_alertness → Coffee causes alertness ✓
```

**Test 4: Control for Confounders (Partial, Requires Knowledge)**
```
If you suspect a confounder (Z), measure it and control for it

Example: Coffee & productivity
  Suspected confounder: Sleep quality (Z)
  
  Method: 
    - Measure: Coffee use, Sleep quality, Productivity
    - Compare productivity within SAME sleep quality groups
    - If coffee still correlates with productivity: More likely causal
    - If coffee effect disappears: Was spurious (just sleep effect)
```

**Test 5: Sensitivity Analysis (For Observational Data)**
```
Question: "How strong would an unmeasured confounder need to be
          to explain away the observed correlation?"

If the answer is "extremely strong" → Likely causal
If the answer is "moderately weak" → Likely spurious

Advanced topic (later in course), but key principle:
  Stronger correlation + weaker confounder needed to explain
  = More confidence in causation
```

---

### 🌳 DECISION TREE: When Do You Have Causation?

```
START: You observe X ↔ Y correlated in data

│
├─ DID YOU RANDOMIZE X?
│  ├─ YES (Experiment/RCT)
│  │  └─ Check: Are groups comparable on everything except X?
│  │     ├─ YES → CAUSATION CONFIRMED ✅✅✅
│  │     └─ NO → Need to control for differences (later methods)
│  │
│  └─ NO (Observational data)
│     │
│     ├─ CAN YOU FIND A PLAUSIBLE MECHANISM? (X → Y chain?)
│     │  ├─ NO → SPURIOUS, likely confounding ❌
│     │  │
│     │  └─ YES → Maybe causal, but need more tests
│     │     │
│     │     ├─ CAN YOU MEASURE & CONTROL CONFOUNDERS?
│     │     │  ├─ YES → Do it, see if correlation remains
│     │     │  │  ├─ Correlation remains → Likely causal 🟡
│     │     │  │  └─ Correlation disappears → Spurious ❌
│     │     │  │
│     │     │  └─ NO → Use sensitivity analysis
│     │     │     ├─ Strong evidence needed to explain away?
│     │     │     │  ├─ YES → Likely causal 🟡
│     │     │     │  └─ NO → Likely spurious ❌
```

---

### 🏢 REAL COMPANY EXAMPLES

**Google: Search Ranking & Click-Through Rate**
```
OBSERVATION: Pages with more links have higher CTR
CORRELATION: Corr(backlinks, CTR) = 0.7

QUESTION: Do backlinks cause higher CTR?
OR: Does high-quality content cause both backlinks AND higher CTR?

GOOGLE'S APPROACH:
✅ Plausible mechanism: Good links → Higher ranking → Higher CTR
✅ Experimental: Randomized ranking changes → Measured CTR changes
✅ Mechanism: Backlinks → Ranking algorithm → Displayed higher → CTR ↑

CAUSATION: YES
Action: Use backlinks as ranking signal (PageRank algorithm)
Impact: Dominated search for 20 years
```

**Netflix: Watching Recommendations & Retention**
```
OBSERVATION: Users who follow recommendations watch 2.3x more
CORRELATION: Strong correlation between recommendations and retention

QUESTION: Do recommendations cause retention?
OR: Do engaged users just follow recommendations more?

NETFLIX'S APPROACH:
✅ Time order: Recommendations appear first, then users can click
✅ Experiment: A/B test "Show recommendations" vs "Hide recommendations"
  - Group A: See recommendations
  - Group B: See library only (no recommendations)
  - Measure: Watch time, retention
✅ Causal mechanism: Recommendations reduce friction → Users find shows → Watch more

CAUSATION: YES
Action: Invest heavily in recommendation systems
Impact: Reduced churn by 15%, +$500M ARR estimated
```

**Uber: Driver Acceptance & Acceptance Rate**
```
OBSERVATION: Drivers using app feature X have lower acceptance rate
CORRELATION: Corr(feature X, acceptance) = -0.4

QUESTION: Does feature X cause lower acceptance?
OR: Do lower-performing drivers use the feature as workaround?

UBER'S APPROACH:
✅ Mechanism: Feature X shows fewer requests, so fewer to accept?
❌ Wrong! Feature X is designed to INCREASE acceptance (smarter matching)

DEEP DIVE:
- Measure: Which drivers use feature X?
- Answer: Drivers already struggling with acceptance
- Real causal graph:
    Low skill
      ↙     ↘
  Feature X   Low acceptance
  (symptom)   (cause)

CAUSATION: NO, it's confounding by selection
  - Low-performing drivers use feature as workaround
  - Feature didn't cause low acceptance, low skill did

CORRECT SOLUTION:
- Control for driver skill (experience, historical acceptance)
- Then measure feature X's true effect
- Result: Feature X actually improves acceptance for any skill level
```

---

### ⚠️ COMMON PITFALLS

**Pitfall 1: Assuming Time Order = Causation**
```
WRONG: "Coffee drinkers wake up early → Coffee causes waking early"

REALITY: Early risers probably drink coffee, not the other way around
         Time order isn't the same as causation

FIX: Also check for:
  - Reverse causation
  - Confounders (something causes both)
  - Selection bias (type of people who do X)
```

**Pitfall 2: Mistaking Correlation Strength for Causation Strength**
```
WRONG: "Correlation is 0.85, therefore causation is strong"

REALITY: Correlation can be 0.95 but still be spurious!
         Strong correlation ≠ Proven causation

Example:
  Correlation(Nicolas Cage movies released, Swimming pool drownings) = 0.97
  Strongest correlation you'll see!
  But obviously not causal.

FIX: Correlation strength only matters after you confirm causation exists
     For causation, look for: Mechanism, time order, experiments
```

**Pitfall 3: Controlling for Colliders (Causes the Wrong Bias)**
```
WRONG: "If I control for Z, I'll adjust for confounding"

REALITY: Depends on what Z is!

If Z is a CONFOUNDER (common cause):
  Z ← X → Y
  Z → Y
  FIX: Control for Z ✅

If Z is a COLLIDER (common effect):
  X → Z ← Y
  FIX: DON'T control for Z! ❌
  (Controlling creates artificial correlation)

This is called "Collider Bias" (covered next)
```

**Pitfall 4: Selection Bias Masquerading as Confounding**
```
WRONG: "Adjust for measured variables and you're good"

REALITY: If subjects selected themselves into treatment based on
         unmeasured factors, correlation is biased

Example:
  "Take online course" vs "Don't take course"
  Observe: Course-takers earn 40% more
  
  Confounder story: Maybe they're motivated? Control for motivation...
  
  Selection bias story: 
    - Motivated people take courses
    - AND motivated people earn more anyway
    - You can measure "motivated" but it's hidden
    - Unmeasured motivation → Selection bias
    - No amount of adjusting helps

FIX: Recognize this is selection bias, not confounder problem
     Requires experimental design or instrumental variables (later)
```

---

### 💡 KEY PRINCIPLE

```
Your job as an MLE:

1. OBSERVE: X and Y are correlated in data
2. QUESTION: Is this correlation causal or spurious?
3. INVESTIGATE:
   - Mechanism plausible?
   - Time order correct?
   - Confounders measurable?
   - Can we experiment?
4. VALIDATE: A/B test in production (ground truth)
5. DEPLOY: Only if causation confirmed
```

---

### 🔗 CONNECTION TO NEXT CONCEPT

**Why we need Causal DAGs (next):**

After learning "Causation vs Correlation," you'll see that:
- Mechanism check = DAG drawing
- Confounder identification = DAG paths
- Confounding detection = Backdoor/frontdoor paths

DAGs are just a **formal language** to draw and analyze these causal structures.

---

## ✅ YOUR TURN: ACTIVE RECALL

Answer these to lock in understanding:

**Q1:** What's the difference between correlation and causation?
```
Your answer:
[Think before revealing]
```

**Q2:** Give an example from your work where X and Y are correlated but NOT causal
```
Your answer:
[Could be from Uber, Netflix, Expedia anything]
```

**Q3:** How would you test if a correlation is causal?
```
Your answer:
[Mechanism? Experiment? Confounders?]
```

**Q4:** Why is controlling for colliders a mistake?
```
Your answer:
[Hint: Creates bias instead of removing it]
```

After you answer, I'll validate and move to Concept 2: Causal DAGs.

