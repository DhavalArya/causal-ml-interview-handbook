# 🎓 TEACHING METHODOLOGY - PRODUCTION-GRADE CAUSAL ML

## Commitment: NOT Theory, but Production Mastery

For **EVERY method/model**, I teach 8 essential components:

### 1️⃣ INTUITION FIRST (No Math)
- Real-world analogy
- Mental model building
- Why this method exists

Example (Propensity Score Matching):
> "You want to find twins in observational data. One sibling gets treatment, one doesn't. But you can't match on 100 characteristics. So you score each person's likelihood of getting treated (propensity), then match on that score instead. This reduces dimensionality."

### 2️⃣ FORMAL DEFINITION (Math + Notation)
- Mathematical formulation
- Notation explanation
- Assumptions embedded

Example (IPW Formula):
```
τ_IPW = 1/n Σ [Y_i * T_i / p_i] - [Y_i * (1-T_i) / (1-p_i)]
where p_i = P(T_i = 1 | X_i) is the propensity score
```

### 3️⃣ DESIGN & IMPLEMENTATION (How to Build)
- Configuration decisions
- Parameter tuning
- Base learner selection
- Hyperparameter choices

**Example (Causal Tree Configuration):**

```python
# DECISION 1: Base Learner
→ Tree-based if non-linear heterogeneity
→ Linear if small data + interpretability critical

# DECISION 2: Honest Splitting
→ 60% for node splitting, 40% for parameter estimation
→ Prevents overfitting to spurious patterns

# DECISION 3: Tree Depth (min_samples_leaf)
→ Start with 50, tune via cross-validated MSE
→ Higher = smoother but misses real effects
→ Lower = noisy estimates with high variance

# DECISION 4: Number of Trees
→ 500 for < 100K rows
→ Check OOB error stabilization
→ Diminishing returns after 500-1000
```

### 4️⃣ WHEN TO USE (Decision Tree vs Alternatives)
- Comparison matrix (pros/cons)
- Data size thresholds
- Business context (interpretability vs accuracy)
- Speed/compute tradeoffs

**Example (Causal Trees vs X-Learner):**

```
Is data size < 10K?
├─ YES → Use Causal Trees (simple, interpretable, no overfitting)
└─ NO (> 10K):
   Is interpretability critical (C-suite presentation)?
   ├─ YES → Use Causal Trees (visualizable splits)
   └─ NO → Is accuracy top priority?
      ├─ YES → Use X-Learner or Causal Forest
      └─ NO → Use T-Learner (balance of both)
```

### 5️⃣ PROS & CONS (Detailed Comparison)

**Causal Trees:**
- ✅ Interpretable (see which X values change effect)
- ✅ Handles non-linearity naturally
- ✅ Honest splitting prevents overfitting
- ✅ Fast to train
- ✅ No propensity score needed
- ❌ Single tree is unstable (high variance)
- ❌ Only binary splits (limited expressiveness)
- ❌ Can't easily update model
- ❌ Variance estimates unreliable

**vs X-Learner:**
- ✅ Better variance (cross-fitting)
- ✅ Works with any base learner
- ✅ Asymptotically efficient
- ✅ Can use neural networks
- ❌ Black box (less interpretable)
- ❌ Requires tuning multiple models
- ❌ Slower (trains 2-3 models)
- ❌ Propensity score needed

### 6️⃣ REAL COMPANY SCENARIOS
- Where Meta uses this method
- Where Google uses this method
- How Uber/Airbnb/Netflix apply it
- Real business impact

**Example:**
- **Meta**: Causal trees to identify which ad creatives affect which user segments
- **Uber**: X-Learner to personalize surge pricing thresholds by driver type
- **Airbnb**: Causal Forest for optimal discount targeting by host type

### 7️⃣ PRODUCTION MLOps (Not Just Theory)
- Data splitting strategy (honest vs standard)
- Assumption validation (before training)
- Evaluation metrics (different from standard ML)
- Monitoring patterns (assumption drift vs accuracy drift)
- Retraining strategy (weekly/monthly vs daily)

**Example (Causal Model Checklist):**
```
✅ Assumptions verified (SUTVA, Overlap, Unconfoundedness)
✅ Data split honestly (60-40 structure-params)
✅ Propensity score well-calibrated
✅ Covariate balance checked post-weighting
✅ CATE evaluated on held-out A/B test (ground truth)
✅ Monitoring: Drift detection for each assumption
✅ Documentation: Which assumptions, which data, which limitations
```

### 8️⃣ CODE IMPLEMENTATION
- Python examples (scikit-learn, causalml, statsmodels)
- PySpark examples (when data > 100GB)
- Production patterns
- Error handling

---

## MLOps Differences: Causal ML vs Standard ML

| Aspect | Standard ML | Causal ML |
|--------|------------|-----------|
| Data splitting | Random 80-20 | Honest 60-40 (structure-params) |
| Objective | Maximize accuracy | Minimize causal bias |
| Cross-validation | Standard k-fold | Can't use (Y not observed for all) |
| Evaluation | Test accuracy | Held-out A/B test (ground truth) |
| Monitoring | Prediction drift | Assumption drift (overlap, balance) |
| Retraining | Daily/continuous | Weekly/monthly (causal assumptions stable) |
| Feature scaling | Often needed | Interpretability first |
| Deployment validation | A/B test results | CATE accuracy on A/B segment tests |

---

## Causal Model Production Pipeline

```
┌────────────────────────────────────────┐
│ 1. DATA INGESTION                      │
│    ├─ Treatment T                      │
│    ├─ Outcome Y                        │
│    └─ Covariates X                     │
└────────────────────────────────────────┘
                  ↓
┌────────────────────────────────────────┐
│ 2. VALIDATION (Causal-specific!)       │
│    ├─ Overlap: P(T=1|X) ∈ (0.1, 0.9)   │
│    ├─ Balance: |mean(X|T=1) - mean(X|T=0)| < 0.1 │
│    ├─ SUTVA: No spillovers detected   │
│    └─ Consistency: Treatment defined   │
└────────────────────────────────────────┘
                  ↓
┌────────────────────────────────────────┐
│ 3. MODEL TRAINING (Honest splitting)   │
│    ├─ 60%: Structure learning          │
│    └─ 40%: Parameter estimation        │
└────────────────────────────────────────┘
                  ↓
┌────────────────────────────────────────┐
│ 4. EVALUATION (Can't use standard CV!) │
│    ├─ ATE: Compare to A/B test         │
│    ├─ CATE: Ranking vs segment tests   │
│    └─ Variance: Bootstrap CIs          │
└────────────────────────────────────────┘
                  ↓
┌────────────────────────────────────────┐
│ 5. DECISION LOGIC                      │
│    ├─ Get CATE: τ̂(x) for new user     │
│    ├─ Apply policy: Treat if τ̂ > thresh│
│    └─ Log decisions (monitoring)       │
└────────────────────────────────────────┘
                  ↓
┌────────────────────────────────────────┐
│ 6. MONITORING (Ongoing assumption checks) │
│    ├─ Overlap still OK?                │
│    ├─ Balance still maintained?        │
│    ├─ CATE predictions still good?     │
│    └─ Any demographic disparities?     │
└────────────────────────────────────────┘
```

---

## Your Learning Guarantee

After completing this class, you will:

✅ **Master 50+ causal ML methods**
  - Know the theory, the practice, and the limitations
  
✅ **Make the RIGHT choice for ANY problem**
  - Decision trees embedded in each lesson
  - Know when to use X vs Y (with evidence)
  
✅ **Implement production-grade systems**
  - Honest data splitting, assumption validation, monitoring
  - MLOps patterns specific to causal ML
  
✅ **Explain to any audience**
  - C-suite: "Here's the causal effect"
  - Data team: "Here's how I validated assumptions"
  - Peers: "Here's why I chose X-Learner over Causal Forest"
  
✅ **Pass interviews at top companies**
  - Meta, Google, Netflix, Uber, Airbnb, LinkedIn
  - Handle follow-up questions with depth and nuance
  
✅ **Solve any problem thrown at you**
  - "Measure incrementality of ads" → You know the approach
  - "Pricing experiment broke SUTVA" → You know the fix
  - "Predict who should get discount?" → You know CATE + policy learning

---

## Spaced Repetition Strategy

Each concept is reinforced multiple times:

1. **First encounter**: Learn in tier-based sequence
2. **Q&A pairs**: Apply to company interview scenarios
3. **Decision trees**: Reference when choosing methods
4. **Code implementation**: Hands-on practice
5. **Production MLOps**: See it in real systems
6. **Mock interviews**: Defend your choices

Result: 70-85% retention after 6 weeks (vs 20-30% with traditional lecture)

---

## Ready to Start?

Pick one:

✅ **YES** → Begin Section 1, Tier 1 (Foundations) today
  
❓ **Questions?** → Ask anything before we begin
  
🚀 **Let's build causal ML mastery together**

