# Section 1: Potential Outcomes and A/B Testing Assumptions

## 📊 EXHAUSTIVE TOPIC CHECKLIST FOR SECTION 1

**Total Topics to Master**: 16 core concepts + 6 interview questions

---

## ✅ COMPLETED (1/16)

### Potential Outcomes Framework [DAY 1]
- [x] **Potential Outcomes (Y(1) vs Y(0))**
  - Y(1): Outcome if unit receives treatment
  - Y(0): Outcome if unit does NOT receive treatment  
  - Individual Treatment Effect (ITE): Y(1) - Y(0) (never observable)
  - **Key insight**: Fundamental Problem — we only see one outcome per person
  - **Your understanding**: ✅ CRYSTAL CLEAR
  - **Examples used**: Uber surge pricing scenario
  - **Related Q&A**: Q1, Q2, Q3, Q4, Q5, Q6 all reference this

---

## ⏳ TODO (15/16 remaining)

### Core Estimands (6 concepts) — [NEXT AFTER ASSUMPTIONS]
- [ ] **Average Treatment Effect (ATE)** — Population average
  - Formula: E[Y(1)] - E[Y(0)] for entire population
  - When to use: When you care about overall effect
  - Example: "Does surge pricing increase driver availability by Xmin on average?"
  
- [ ] **Average Treatment Effect on the Treated (ATT)** — Effect on treated units only
  - Formula: E[Y(1) - Y(0) | T=1]
  - When to use: When treatment effect differs by who gets treated
  - Example: "For drivers who actually accepted surge, how much did they benefit?"
  
- [ ] **Average Treatment Effect on the Control (ATC)** — Effect on untreated units
  - Formula: E[Y(1) - Y(0) | T=0]
  - When to use: Estimating counterfactual effect on never-treated units
  - Example: "If drivers who rejected surge HAD accepted, how much would they benefit?"

- [ ] **Conditional Average Treatment Effect (CATE)** — Heterogeneous effects by subgroup
  - Formula: τ(x) = E[Y(1) - Y(0) | X=x]
  - When to use: When effect varies by driver type (part-time vs full-time)
  - Tools: Causal forests, S-learner, X-learner, R-learner
  - **Q5 (Airbnb) likely tests this concept**

- [ ] **Intent to Treat (ITT)** — Effect of assignment (whether you complied or not)
  - Formula: E[Y_observed | assigned to treatment] - E[Y_observed | assigned to control]
  - When to use: When people don't follow randomization assignment
  - **Q2 (Google) tests this**
  - Difference: ITT ≠ ATE when compliance is imperfect

- [ ] **Local Average Treatment Effect (LATE)** — Effect on compliers only
  - Formula: E[Y(1) - Y(0) | complier]
  - When to use: Instrumental variables, encouragement designs
  - **Related to Q6 (LinkedIn) measurement assumptions**

---

### Key A/B Testing Assumptions (5 concepts) — [DAY 2-3]

- [ ] **SUTVA (Stable Unit Treatment Value Assumption)**
  - Two parts:
    1. **No interference**: Treating unit A doesn't affect unit B's outcome
    2. **No hidden treatment versions**: Treatment is well-defined (one version only)
  - Violations: 
    - Network effects (friend recommendations affecting each other)
    - Externalities (if you surge price drivers, does it affect rider demand?)
  - **Q1 (Meta) explicitly tests this — CRITICAL FOR Q1**
  - Impact if violated: Your effect estimates are wrong/biased

- [ ] **Randomization / Random Treatment Assignment** — RCT magic
  - What it does: T ⊥ (Y(0), Y(1))  [Treatment independent of potential outcomes]
  - Why it works: Breaks all confounding automatically
  - You DON'T need to measure all confounders
  - Impact: Unbiased ATE estimation (under SUTVA)
  - When it fails: Non-compliance, attrition, selection bias in measurement

- [ ] **Unconfoundedness / Conditional Independence / Exchangeability** — For observational data
  - Formal: T ⊥ (Y(0), Y(1)) | X  [Treatment independent of outcomes given observed covariates X]
  - Intuition: "After controlling for X, treatment is as-if random"
  - BIGGEST ASSUMPTION in observational causal inference
  - Problem: Unmeasured confounders (W) violate this
  - Methods that rely on it: Regression, matching, propensity score methods
  - **Q2 (Google) tests this under "Exchangeability"**
  - Weakness: Can't verify from data alone

- [ ] **Positivity / Common Support / Overlap** — Estimation feasibility
  - Formal: 0 < P(T=1 | X) < 1 for all X
  - Intuition: Every covariate combination must have BOTH treatment and control units
  - Violation: "Positivity violation" = you're trying to estimate effect in a region with no data
  - Example: If all high-income users get premium treatment, you can't estimate ATE for high-income
  - **Q5 (Airbnb) likely tests Positivity/Overlap**
  - Methods that struggle: Extreme propensity scores

- [ ] **Consistency / SUTVA part 2** — Treatment well-defined
  - Formal: If T=t, then Y(t) = Y_observed
  - Intuition: The treatment in your experiment matches the treatment in your potential outcomes
  - Problem: Hidden treatment versions (e.g., "discount" can be applied different ways)
  - **Q4 (Uber) tests Consistency under "Treatment Delivery"**

---

### Bias Sources & Related Concepts (3 concepts) — [DAY 2]

- [ ] **Selection Bias / Confounding Bias** — Why observational data is tricky
  - Definition: Non-random assignment to treatment/control due to observed/unobserved factors
  - Observable confounders: Income, user_type, region (can adjust)
  - Unobservable confounders: Motivation, risk appetite (can't adjust directly)
  - Why RCTs solve it: Randomization breaks selection mechanically
  - **Related to all Q&A pairs**

- [ ] **Observable vs Unobservable Confounders** — When to adjust
  - Observable: Can measure → use regression, matching, propensity score
  - Unobservable: Can't measure → need IV, difference-in-differences, synthetic control
  - MLE decision point: "Which method should I use?" depends on this
  - Example: Does user "motivation" confound effect? (unobservable, need IV)

- [ ] **Causal Graphs / DAGs (Directed Acyclic Graphs)** — Visual reasoning tool
  - Shows: Treatment (T) → Outcome (Y), with confounders (C)
  - Tells you: Which variables to control for (blocking backdoor paths)
  - Rules: d-separation, backdoor criterion
  - Use case: Justify which covariates to include in regression
  - **You'll need this for every Q&A pair to defend assumptions**

---

### Fundamental Concepts (1 concept) — [DAY 1, already covered]

- [x] **Fundamental Problem of Causal Inference** 
  - We never observe both Y(1) and Y(0) for same unit simultaneously
  - This is THE reason we need assumptions or randomization
  - Randomization "solves" it by averaging across many units

---

## 📋 MAPPED TO INTERVIEW QUESTIONS

| Topic | Q1 Meta | Q2 Google | Q3 Netflix | Q4 Uber | Q5 Airbnb | Q6 LinkedIn |
|-------|---------|-----------|-----------|---------|-----------|------------|
| Potential Outcomes | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| SUTVA | ✅ Hard | - | - | - | - | - |
| Randomization | - | ✅ | ✅ | - | - | - |
| Unconfoundedness | - | ✅ | - | - | - | - |
| Positivity | - | - | - | - | ✅ | - |
| Consistency | - | - | - | ✅ | - | - |
| ATE vs ATT | - | - | ✅ | - | - | - |
| ITT | - | ✅ | - | - | - | - |
| LATE | - | - | - | - | - | ✅ |
| CATE | - | - | - | - | ✅ | - |
| Measurement | - | - | - | - | - | ✅ |

---

## 🎯 ROADMAP FOR SECTION 1 COMPLETION

**Phase 1a: Assumptions Deep Dive (Today/Tomorrow)** — 90 mins
1. SUTVA (20 min) + Q1 scenario → You write response
2. Randomization (15 min) + Q2 scenario → You write response

**Phase 1b: More Assumptions (Day 3)** — 90 mins
3. Unconfoundedness (25 min) + Q2 continued
4. Positivity (20 min) + Q5 scenario setup
5. Consistency (20 min) + Q4 scenario setup

**Phase 1c: Estimands Deep Dive (Day 4)** — 120 mins
6. ATE/ATT/CATE/ITT/LATE explained
7. Decision tree: "When to report which estimand?"
8. Q3 + Q5 + Q6 scenarios

**Phase 1d: Polish & Active Recall (Day 5)** — 60 mins
9. All 6 questions answered in YOUR words
10. Spaced recall: Randomization vs Unconfoundedness vs Positivity
11. Handbook first draft pushed to GitHub

---

## ✅ PROGRESS METER

```
SECTION 1 COMPLETION PROGRESS
████░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ 6%

Topics: 1/16 ✅
Questions: 0/6 ready

Next: SUTVA Deep Dive
Estimated completion: 5-7 days with daily 1.5-2 hour sessions
```

---

## 🔗 CONNECTIONS TO OTHER SECTIONS

**Section 2** (Confounding & Propensity Scores) assumes crystal clear Unconfoundedness + Positivity
**Section 3** (DiD & Panel Data) assumes you know when these assumptions fail
**Section 4** (IV) assumes you know what unobserved confounders are
**Section 5** (RD) assumes you understand Positivity/Overlap violations

> **Core Truth**: Section 1 is the FOUNDATION. Rushing through it = struggling in Sections 2-5.

Your approach: Go SLOW, go DEEP, make sure each assumption is intuitive + formal + coded.

---

Ready to start SUTVA? 🚀

