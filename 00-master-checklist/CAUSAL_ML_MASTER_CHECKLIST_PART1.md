# 🎓 MASTER CAUSAL ML CHECKLIST - COMPREHENSIVE & EXHAUSTIVE

**Goal**: Cover ALL causal ML topics. Learn concepts section-by-section. Track progress with checkboxes.  
**Structure**: Organized by TIER (foundational to advanced). No section silos - topics can be learned across sections.

---

## 📊 PROGRESS TRACKER

Total Topics: 80+ concepts  
Current Progress: 0%  
Master Status: 🟢 Ready to learn

---

# TIER 1: FOUNDATIONS (13 concepts)

## 1.1 Potential Outcomes Framework
- [ ] **Y(1) vs Y(0) notation** - Potential outcomes under treatment/control
- [ ] **Individual Treatment Effect (ITE)** - Y(1) - Y(0) per unit (unobservable)
- [ ] **Counterfactual thinking** - "What would have happened if..."
- [ ] **Fundamental Problem of Causal Inference** - Can't observe both outcomes for one unit

## 1.2 Causal Graphs & DAGs
- [ ] **Directed Acyclic Graphs (DAGs)** - Visual representation of causal structure
- [ ] **Nodes & Arrows** - Variables and causal relationships
- [ ] **Backdoor paths** - Non-causal associations through confounders
- [ ] **Frontdoor paths** - Causal chains through mediators
- [ ] **d-separation** - When paths are blocked (conditional independence)
- [ ] **Backdoor criterion** - Which variables to control for
- [ ] **Frontdoor criterion** - Identification through mediators
- [ ] **Path diagrams** - Drawing & interpreting DAGs for real scenarios

## 1.3 Core Causal Concepts
- [ ] **Causation vs Correlation** - Why correlation alone isn't sufficient
- [ ] **Confounding** - Common cause affecting both T and Y
- [ ] **Mediation** - Indirect path T → M → Y
- [ ] **Collider bias** - Conditioning on common effect creates bias
- [ ] **Selection bias** - Non-random assignment to treatment
- [ ] **Observational vs Experimental data** - Data collection method matters

---

# TIER 2: ESTIMANDS (7 concepts)

## 2.1 Treatment Effect Targets
- [ ] **Average Treatment Effect (ATE)** - E[Y(1)-Y(0)] for entire population
- [ ] **Average Treatment Effect on Treated (ATT)** - E[Y(1)-Y(0)|T=1]
- [ ] **Average Treatment Effect on Control (ATC)** - E[Y(1)-Y(0)|T=0]
- [ ] **Conditional Average Treatment Effect (CATE)** - τ(x) = E[Y(1)-Y(0)|X=x] (heterogeneous)
- [ ] **Intent to Treat (ITT)** - Effect of assignment (not actual treatment)
- [ ] **Local Average Treatment Effect (LATE)** - Effect on compliers (with IV)
- [ ] **Policy Value** - Expected outcome under optimal treatment allocation

---

# TIER 3: IDENTIFICATION ASSUMPTIONS (10 concepts)

## 3.1 Core Assumptions (SUTVA + Consistency + Unconfoundedness + Positivity)
- [ ] **SUTVA (Stable Unit Treatment Value Assumption)** - Part 1: No interference between units
- [ ] **SUTVA - No hidden versions** - Part 2: Treatment is well-defined (one version only)
- [ ] **SUTVA violations** - Network effects, externalities, general equilibrium
- [ ] **Consistency** - Y(t) observed = Y in potential outcomes when T=t
- [ ] **Consistency violations** - Hidden treatment versions, dose variation
- [ ] **Unconfoundedness (Exchangeability)** - T ⊥ (Y(0),Y(1)) | X after controlling for X
- [ ] **Strong Ignorability** - Synonym for unconfoundedness
- [ ] **Conditional Independence** - Formal notation & interpretation
- [ ] **Overlap / Positivity** - 0 < P(T=1|X) < 1 for all X (common support)
- [ ] **Positivity violations** - Extrapolation warnings, insufficient data regions

## 3.2 Randomization
- [ ] **Randomization / Random Assignment** - T ⊥ (Y(0),Y(1)) mechanically
- [ ] **RCT Design** - How randomization works in practice
- [ ] **Compliance issues** - Non-compliance, intent-to-treat complications
- [ ] **Perfect vs imperfect compliance** - Effect on ATT vs ATE interpretation

---

# TIER 4: ESTIMATION METHODS - RANDOMIZED DATA (12 concepts)

## 4.1 Basic RCT Analysis
- [ ] **Difference in means** - Simple Y_treatment - Y_control
- [ ] **Regression for RCT** - Controlling for baseline covariates
- [ ] **Blocking & Stratification** - Pre-treatment group assignment
- [ ] **Clustered randomization** - Unit of randomization ≠ unit of analysis

## 4.2 Dealing with Non-Compliance
- [ ] **Intent-to-treat (ITT)** - Analyze as assigned, not as treated
- [ ] **As-treated analysis** - Biased when compliance is endogenous
- [ ] **Complier Average Causal Effect (CACE)** - Effect on those who comply
- [ ] **2SLS (Two-Stage Least Squares)** - IV method for non-compliance
- [ ] **DRIV Learner** - Doubly robust IV with non-compliance
- [ ] **Randomized encouragement design** - Assignment as instrument

## 4.3 RCT Pitfalls
- [ ] **Attrition bias** - Differential dropout between groups
- [ ] **Multiple testing** - p-hacking, false discoveries
- [ ] **Spillovers / Interference** - SUTVA violations in RCTs
- [ ] **Measurement error** - Outcome measurement varies by group

---

# TIER 5: ESTIMATION METHODS - OBSERVATIONAL DATA (18 concepts)

## 5.1 Regression-Based Methods
- [ ] **Regression adjustment** - Control for confounders via covariates
- [ ] **Linear regression for CATE** - β varies by X (interactions)
- [ ] **Polynomial regression** - Non-linear effects
- [ ] **Causal forests / Random forests** - Non-parametric estimation of CATE

## 5.2 Matching Methods
- [ ] **Exact matching** - Match on all confounders
- [ ] **Nearest neighbor matching** - Closest unit in control group
- [ ] **Caliper matching** - Limit distance to nearest neighbor
- [ ] **Mahalanobis distance** - Multivariate distance metric
- [ ] **Covariate balance** - Check if matched groups are comparable
- [ ] **Matching with replacement** - Allow one unit to be matched multiple times
- [ ] **Entropy balancing** - Reweight to achieve exact balance

## 5.3 Propensity Score Methods
- [ ] **Propensity score** - P(T=1|X), probability of treatment given X
- [ ] **Propensity score estimation** - Logistic regression, gradient boosting
- [ ] **Propensity score matching** - Match on PS instead of all X
- [ ] **Inverse Probability of Treatment Weighting (IPTW)** - Weight by 1/P(T|X)
- [ ] **Doubly Robust (DR) estimation** - Regression + propensity score
- [ ] **Augmented IPW (AIPW)** - DR with better bias properties
- [ ] **Trimming extreme propensity scores** - Handle positivity violations
- [ ] **Overlap / Common support** - Exclude regions with no treated/control

## 5.4 Meta-Learners (for Heterogeneous Effects)
- [ ] **S-Learner (Single model)** - One model with treatment as covariate
- [ ] **T-Learner (Two model)** - Separate models for T=0 and T=1
- [ ] **X-Learner** - Residualization + cross-fitting for asymptotic efficiency
- [ ] **R-Learner** - Orthogonalized/Riesz representation approach
- [ ] **DR-Learner** - Doubly robust combination

## 5.5 Tree-Based Methods for CATE
- [ ] **Causal trees** - Recursive partitioning optimized for treatment effects
- [ ] **Causal random forests** - Ensemble of causal trees
- [ ] **Generalized random forests** - Flexible heterogeneity estimation
- [ ] **Honest splitting** - Use separate data for splitting vs estimation

---

# TIER 6: IDENTIFICATION WITH UNOBSERVED CONFOUNDERS (10 concepts)

## 6.1 Instrumental Variables (IV)
- [ ] **Instrumental Variables (IV)** - Z affects Y only through T
- [ ] **IV assumptions** - Relevance (Z→T), Exclusion (Z⊥Y|T)
- [ ] **2SLS estimation** - Stage 1: T ~ Z; Stage 2: Y ~ T_predicted
- [ ] **IV diagnostics** - First-stage F-stat, weak instruments
- [ ] **LATE interpretation** - Effect on compliers, not ATE
- [ ] **Heterogeneous IV effects** - Different effects by compliance type

## 6.2 Difference in Differences (DiD)
- [ ] **Parallel trends assumption** - Treated & control would follow same trajectory
- [ ] **Before-after design** - Compare T_after - T_before to C_after - C_before
- [ ] **DiD estimator** - (T_after - T_before) - (C_after - C_before)
- [ ] **Event study** - Timeline of treatment effects
- [ ] **Dynamic treatment effects** - Effects vary over time post-treatment
- [ ] **Multiple time periods** - Generalized DiD with many periods
- [ ] **Multiple treated groups** - Varying treatment timing (staggered)
- [ ] **Violations** - Parallel trends breaks down, policy feedback

## 6.3 Regression Discontinuity (RD)
- [ ] **Regression Discontinuity Design** - Treatment based on threshold of running variable
- [ ] **Sharp RD** - Deterministic treatment assignment at cutoff
- [ ] **Fuzzy RD** - Probabilistic treatment at cutoff (use as IV)
- [ ] **Bandwidth selection** - How wide to look on each side of cutoff
- [ ] **Local linear regression** - RD estimation method
- [ ] **Discontinuity at cutoff** - Treatment effect identified at threshold
- [ ] **Internal validity** - Effect is local, not generalizable

---

# TIER 7: ADVANCED METHODS & SPECIAL CASES (15 concepts)

## 7.1 Handling Hidden Confounders
- [ ] **Sensitivity analysis** - How much hidden confounder needed to flip conclusion?
- [ ] **Rosenbaum bounds** - Quantify robustness to unmeasured confounding
- [ ] **Proxy variable approach** - Use proxy for hidden confounder
- [ ] **CEVAE (Causal Variational Autoencoder)** - Learn latent confounder
- [ ] **Negative controls** - Test for unmeasured confounding

## 7.2 Heterogeneous Treatment Effects & CATE
- [ ] **Heterogeneous treatment effects (HTE)** - Effects vary by subgroup
- [ ] **Subgroup analysis** - Estimate effects within groups
- [ ] **Treatment-effect modification** - Which X values change effect?
- [ ] **Policy learning** - Optimal treatment allocation given CATE
- [ ] **Doubly-Learned approach** - Cross-fit nuisance parameters

## 7.3 Time & Dynamics
- [ ] **Temporal treatment effects** - Effect changes over time
- [ ] **Dynamic treatment regimes** - Sequential decisions based on history
- [ ] **Causal pathways** - Direct + indirect effects
- [ ] **Mediation analysis** - T → M → Y decomposition

## 7.4 Complex Treatment Structures
- [ ] **Multiple treatments** - More than 2 treatment arms
- [ ] **Continuous treatments** - Dose-response relationships
- [ ] **Network/Interference** - Spillover effects between units
- [ ] **Attribution modeling** - Multi-touch journeys, last-click bias

## 7.5 Validation & Model Selection
- [ ] **Validation losses** - ATE vs CATE vs ranking metrics
- [ ] **Causal forest variance** - Out-of-bag error estimates
- [ ] **Cross-validation for CATE** - Can't use standard CV (Y not observed for Y(1-T))
- [ ] **Benchmarking** - Compare methods on ground-truth simulated data

---

# TIER 8: MACHINE LEARNING & CAUSAL ML INTERFACE (8 concepts)

## 8.1 Debiasing & Orthogonalization
- [ ] **Neyman orthogonality** - Gradient wrt nuisance param = 0 at truth
- [ ] **Debiased machine learning** - Residualization to reduce bias
- [ ] **Riesz representation** - Theoretical foundation for R-Learner
- [ ] **Cross-fitting** - Train on one fold, test on another to reduce overfitting

## 8.2 Neural Networks for Causal Inference
- [ ] **DragonNet** - Neural network architecture for CATE
- [ ] **TARNet** - Tailored Regression Network
- [ ] **Representation learning** - Learn shared feature space
- [ ] **CEVAE** - Variational autoencoder for latent confounders

---

# TIER 9: BUSINESS & PRODUCTION APPLICATIONS (12 concepts)

## 9.1 Common Business Scenarios
- [ ] **A/B testing** - Online experiments, conversion, revenue
- [ ] **Pricing experiments** - Price elasticity via causal inference
- [ ] **Recommendation systems** - Causal effect of recommendation
- [ ] **Marketing attribution** - Multi-touch, channel interactions
- [ ] **Supply-side interventions** - Seller/provider side effects
- [ ] **Network effects** - Viral growth, SUTVA violations

## 9.2 Implementation Patterns
- [ ] **Production causal pipeline** - ETL → estimation → decision
- [ ] **Real-time scoring** - Apply estimated CATE to serve decisions
- [ ] **Monitoring & SLA** - Track when assumptions break
- [ ] **A/A testing** - Verify randomization worked
- [ ] **Sensitivity testing** - Robustness to assumption violations
- [ ] **Documentation** - Causal assumptions, limitations, interpretability

---

# TIER 10: INTERVIEW PREP & DECISION TREES (7 concepts)

## 10.1 Interview Question Patterns
- [ ] **"Design an experiment"** - Identify treatment, confounders, estimand
- [ ] **"How would you measure X?"** - Which causal method, which assumptions
- [ ] **"What if [assumption violated]?"** - Robustness, alternatives
- [ ] **"Estimate effect of Y on Z"** - Identify if observational/experimental
- [ ] **"SUTVA broken - what now?"** - Spillovers, interference
- [ ] **"Is this causal?"** - Identify confounders, check assumptions
- [ ] **Decision tree: "Which method to use?"** - Flow chart for method selection

---

## 🔗 TIER DEPENDENCIES

```
Tier 1 (Foundations) ──┐
                       ├─→ Tier 3 (Assumptions) ──┐
Tier 2 (Estimands)  ───┘                           ├─→ Tier 5 (Observational)
                                                   ├─→ Tier 6 (Unobserved)
Tier 1 (DAGs)  ────────────────────────────────────┘
                       
Tier 5 + Tier 6 ──→ Tier 7 (Advanced)
Tier 5 + Tier 7 ──→ Tier 8 (ML Interface)
All Tiers ─→ Tier 9 (Production)
All Tiers ─→ Tier 10 (Interviews)
```

**Next**: Create PART 2 with section-specific mappings and Q&A pairing.

