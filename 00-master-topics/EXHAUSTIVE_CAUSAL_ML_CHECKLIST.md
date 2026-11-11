# MASTER CAUSAL ML INTERVIEW PREPARATION CHECKLIST

**Goal**: Comprehensive coverage of ALL causal ML concepts across the entire domain.
**Format**: Organized by logical topic areas (not interview sections).
**Usage**: Tick off topics as you learn them through sections 1-5. Any uncovered topics = bonus deep dives.

---

## TIER 1: FOUNDATIONS & CORE THEORY (15 concepts)

### Potential Outcomes Framework
- [ ] Potential Outcomes notation (Y(1), Y(0), Y(t))
- [ ] Individual Treatment Effect (ITE = Y(1) - Y(0))
- [ ] Counterfactual reasoning
- [ ] Fundamental Problem of Causal Inference (unobservability)
- [ ] Causal vs Statistical relationships

### Causal Models & Representation
- [ ] Causal Directed Acyclic Graphs (DAGs)
  - [ ] Nodes, edges, direction
  - [ ] d-separation / Markov properties
  - [ ] Backdoor paths vs frontdoor paths
- [ ] Structural Causal Models (SCMs)
- [ ] Causal mechanisms vs associations
- [ ] Confounders vs mediators vs colliders

### Treatment & Outcomes
- [ ] Well-defined treatment / Consistency assumption
- [ ] Treatment versions / Hidden variations
- [ ] Outcome measurement / Proxy outcomes
- [ ] Compliance vs adherence issues

---

## TIER 2: KEY ASSUMPTIONS (12 concepts)

### SUTVA & Interference
- [ ] Stable Unit Treatment Value Assumption (SUTVA)
  - [ ] No interference (spillover) between units
  - [ ] No hidden treatment versions
- [ ] Network interference / Peer effects
- [ ] Spatial spillovers / Geographic interference
- [ ] General Equilibrium effects
- [ ] Exclusion restrictions

### Identification Assumptions (Core)
- [ ] Unconfoundedness / Conditional Independence / Exchangeability
  - [ ] T ⊥ (Y(0), Y(1)) | X (formal definition)
  - [ ] Observable vs unobservable confounding
  - [ ] When it's reasonable vs when it's not
- [ ] Positivity / Common Support / Overlap
  - [ ] 0 < P(T=1|X) < 1 definition
  - [ ] Positivity violations in practice
  - [ ] Extrapolation warnings
- [ ] Consistency / SUTVA Part 2
  - [ ] Treatment is well-defined
  - [ ] No interference between Y(t) and actual Y_observed
- [ ] Randomization / Random Assignment
  - [ ] Makes all assumptions hold simultaneously
  - [ ] Why RCTs are powerful

### Special Assumptions
- [ ] Ignorability (same as unconfoundedness)
- [ ] No unmeasured confounding
- [ ] Overlap / Common support (alternative name)
- [ ] Stable treatment unit value (alternative name)

---

## TIER 3: ESTIMANDS & CAUSAL QUANTITIES (8 concepts)

### Population-Level Estimands
- [ ] Average Treatment Effect (ATE = E[Y(1)] - E[Y(0)])
  - [ ] What it estimates
  - [ ] When to use it
  - [ ] Interpretation
- [ ] Average Treatment Effect on Treated (ATT = E[Y(1)-Y(0)|T=1])
  - [ ] Difference from ATE
  - [ ] When effect is heterogeneous
- [ ] Average Treatment Effect on Control (ATC = E[Y(1)-Y(0)|T=0])
  - [ ] Counterfactual for untreated units

### Heterogeneous Effects
- [ ] Conditional Average Treatment Effect (CATE / HTE)
  - [ ] τ(x) = E[Y(1)-Y(0)|X=x]
  - [ ] Subgroup analysis / Treatment heterogeneity
  - [ ] How to estimate: matching by subgroup
- [ ] Optimal treatment regimes / Dynamic treatments
- [ ] Treatment effect on compliers

### Compliance & Assignment Effects
- [ ] Intent to Treat (ITT)
  - [ ] Effect of assignment (whether you comply or not)
  - [ ] When compliance is imperfect
- [ ] Local Average Treatment Effect (LATE)
  - [ ] Effect on compliers only
  - [ ] Used with instrumental variables
- [ ] Complier Average Causal Effect (CACE)
- [ ] Per-Protocol Effect (PPE)

---

## TIER 4: IDENTIFICATION & CAUSAL DIAGRAMS (9 concepts)

### Graphical Identification
- [ ] Backdoor criterion
  - [ ] Identifying backdoor paths
  - [ ] Which variables block paths
  - [ ] When to include/exclude in regression
- [ ] Frontdoor criterion
  - [ ] When backdoor criterion doesn't apply
  - [ ] Alternative path for identification
- [ ] Do-calculus (Pearl's calculus)
  - [ ] Three rules of do-calculus
  - [ ] When to apply each rule
- [ ] Causal effect identification from DAGs
- [ ] Selection diagrams / Z-graphs

### Identifiability Concepts
- [ ] Point identification vs set identification
- [ ] Non-parametric identification
- [ ] Sensitivity analysis / Bias bounds
- [ ] When effects are NOT identifiable

---

## TIER 5: RANDOMIZATION & A/B TESTING (11 concepts)

### Experimental Design
- [ ] Randomized Controlled Trials (RCTs) / Gold standard
- [ ] Random assignment mechanisms
  - [ ] Complete randomization
  - [ ] Stratified randomization
  - [ ] Matched pairs randomization
- [ ] Blocked experiments
- [ ] Sequential experimentation / Peeking
- [ ] Multiple testing / Multiple comparisons problem

### RCT Challenges & Issues
- [ ] Non-compliance / Imperfect treatment adherence
- [ ] Attrition / Missing data in experiments
- [ ] Selection into treatment
- [ ] Experimenter bias / Hawthorne effects
- [ ] Spillover / Interference in RCTs

### Experiment Validity
- [ ] Internal validity (causal estimates correct)
- [ ] External validity (generalizability)
- [ ] Construct validity (measure right thing)
- [ ] Statistical validity (correct statistical methods)

---

## TIER 6: PROPENSITY SCORE & MATCHING METHODS (13 concepts)

### Propensity Score Framework
- [ ] Propensity score definition
  - [ ] P(T=1|X) = probability of treatment given covariates
  - [ ] Why it works for balancing
  - [ ] Rosenbaum & Rubin theorem
- [ ] Propensity score estimation
  - [ ] Logistic regression
  - [ ] Machine learning methods
  - [ ] Specification sensitivity
- [ ] Propensity score diagnostics
  - [ ] Checking overlap / common support
  - [ ] Covariate balance testing
  - [ ] Love plot / standardized differences

### Propensity Score Applications
- [ ] Propensity Score Matching (PSM)
  - [ ] 1-to-1 nearest neighbor matching
  - [ ] Caliper matching
  - [ ] Radius matching
  - [ ] Pros vs cons
- [ ] Inverse Probability Weighting (IPW)
  - [ ] Weighting by 1/propensity score
  - [ ] Stabilized weights
  - [ ] Trimming extreme weights
- [ ] Stratification / Subclassification on propensity score

### Matching Methods (Beyond Propensity Score)
- [ ] Exact matching
- [ ] Nearest neighbor matching (Mahalanobis distance)
- [ ] Covariate matching
- [ ] Entropy balancing
- [ ] Genetic matching / Optimization-based matching

---

## TIER 7: REGRESSION & ADJUSTMENT METHODS (9 concepts)

### Linear Regression for Causal Inference
- [ ] Regression adjustment
  - [ ] Why controlling for confounders works
  - [ ] Regression coefficient interpretation
  - [ ] When regression fails
- [ ] Multiple regression / Multiple confounders
- [ ] Interaction terms / Effect modification
- [ ] Nonlinear regression / Logistic regression
- [ ] Regression with interaction (treatment × covariate)

### Advanced Regression Methods
- [ ] Doubly Robust Estimation (DML)
  - [ ] Combining regression + propensity score
  - [ ] Two-stage approach
  - [ ] Semiparametric efficiency
- [ ] Augmented IPW (AIPW)
- [ ] Targeted Maximum Likelihood Estimation (TMLE)

---

## TIER 8: QUASI-EXPERIMENTAL DESIGNS (15 concepts)

### Difference-in-Differences (DiD)
- [ ] DiD logic / Parallel trends assumption
  - [ ] Before/after + treatment/control groups
  - [ ] Why it works: Trends must be parallel
- [ ] Two-way fixed effects regression
- [ ] Event study design / Event study regression
- [ ] Staggered DiD / Rollout analysis
- [ ] DiD violations & robustness checks
  - [ ] Pre-trends testing
  - [ ] Placebo tests
  - [ ] Effect heterogeneity over time
- [ ] Synthetic control method
  - [ ] Creating counterfactual comparison group
  - [ ] Weighted combination of control units
  - [ ] When to use vs DiD

### Instrumental Variables (IV)
- [ ] IV Framework
  - [ ] Instrument definition
  - [ ] Relevance & Exclusion restriction
  - [ ] Two-stage least squares (2SLS)
- [ ] IV assumptions
  - [ ] Relevance: Instrument affects treatment
  - [ ] Exclusion: Instrument affects outcome ONLY through treatment
  - [ ] Exogeneity: Instrument is exogenous
- [ ] LATE / Complier Average Causal Effect
- [ ] Weak instruments problem
- [ ] Multiple instruments / Overidentification tests
- [ ] IV interpretation & local effects
- [ ] Natural experiments / Quasi-random assignment

### Regression Discontinuity (RD)
- [ ] RD Concept / Discontinuity at threshold
  - [ ] Sharp RD vs Fuzzy RD
  - [ ] Bandwidth selection
  - [ ] Polynomial order choice
- [ ] RD identification assumption (continuity)
- [ ] Local Linear Regression (LLR)
- [ ] McCrary test / Manipulation testing
- [ ] Robustness checks in RD

---

## TIER 9: METALEARNERS & CAUSAL ML MODELS (11 concepts)

### Causal Forests & Tree-Based Methods
- [ ] Causal Forests (Athey & Wager)
  - [ ] How they estimate CATE
  - [ ] Honest splitting
  - [ ] Variable importance for treatment effects
- [ ] Generalized Random Forests (GRF)
- [ ] Bayesian Causal Forests
- [ ] Tree-based heterogeneity estimation

### Metalearners for CATE
- [ ] S-learner (Single model)
- [ ] T-learner (Two models)
- [ ] X-learner (Cross-fitting)
- [ ] R-learner (Residual learner)
- [ ] DR-learner (Doubly robust learner)
- [ ] M-learner (Moment-based)

### Double Machine Learning (DML)
- [ ] DML Concept / Debiased ML
- [ ] Nuisance parameter estimation
- [ ] Cross-fitting / Sample splitting
- [ ] Neyman orthogonality
- [ ] When to use DML vs traditional methods

---

## TIER 10: IDENTIFICATION IN COMPLEX SETTINGS (9 concepts)

### Mediation Analysis
- [ ] Direct effects vs Indirect effects
- [ ] Natural direct effects (NDE)
- [ ] Natural indirect effects (NIE)
- [ ] Controlled direct effects (CDE)
- [ ] Sequential ignorability assumption
- [ ] Mediation decomposition

### Causal Graphs for Complex Settings
- [ ] Time-varying confounding
- [ ] Post-treatment bias / Collider stratification
- [ ] Measurement error & latent variables
- [ ] Proxy variables & causal inference
- [ ] Selection bias / Handling missing data

---

## TIER 11: ROBUSTNESS & SENSITIVITY (8 concepts)

### Sensitivity Analysis
- [ ] Rosenbaum bounds
  - [ ] Measuring robustness to unobserved confounding
  - [ ] Gamma parameter interpretation
- [ ] E-values / E-value interpretation
- [ ] Bounds on causal effects
- [ ] Bias adjustment formulas
- [ ] Contour plots / Sensitivity tables

### Robustness Checks & Diagnostics
- [ ] Covariate balance testing (standardized differences)
- [ ] Love plot visualization
- [ ] Overlap checking / Positivity violations
- [ ] Specification robustness (multiple models)
- [ ] Falsification tests / Placebo outcomes

---

## TIER 12: APPLICATIONS & DOMAINS (10 concepts)

### A/B Testing & Online Experiments
- [ ] Randomization implementation
- [ ] User-level vs event-level randomization
- [ ] Carryover effects / Washout periods
- [ ] Sample size calculation
- [ ] Power analysis for causal inference
- [ ] Sequential testing / Always-valid inference

### Marketing & Attribution
- [ ] Incrementality testing
- [ ] Multi-touch attribution
- [ ] Marketing mix modeling (MMM)
- [ ] Econometric modeling
- [ ] Geo-experiments / Geo-randomized tests

### Economics & Policy Evaluation
- [ ] Program evaluation / Policy impact
- [ ] Labor economics applications
- [ ] Development economics / RCTs
- [ ] Public policy analysis
- [ ] Welfare analysis / Heterogeneous policy effects

### Other Domains
- [ ] Healthcare / Clinical trials
- [ ] Education outcomes
- [ ] Environmental impacts
- [ ] Social networks
- [ ] Supply chain / Operational decisions

---

## TIER 13: IMPLEMENTATION & TOOLS (12 concepts)

### Python Libraries & Tools
- [ ] scikit-learn
  - [ ] Logistic regression for propensity scores
  - [ ] Linear regression for adjustment
- [ ] EconML (Microsoft)
  - [ ] Causal forests
  - [ ] DML
  - [ ] Metalearners (S/T/X/R-learner)
- [ ] CausalML (Uber)
  - [ ] Propensity score methods
  - [ ] Metalearners
- [ ] DoWhy (Microsoft)
  - [ ] Causal graph specification
  - [ ] Identification & estimation
  - [ ] Sensitivity analysis
- [ ] Causal (Google)
- [ ] pymc / Bayesian causal inference

### PySpark / Big Data Causal ML
- [ ] Distributed propensity score estimation
- [ ] Large-scale matching on Spark
- [ ] DiD with big panel data
- [ ] Causal forests on distributed data
- [ ] Scaling out sensitivity analysis

### Code Implementation Patterns
- [ ] Loading & preparing data
- [ ] Building causal DAG/graphs
- [ ] Estimating propensity scores
- [ ] Balance checking & diagnostics
- [ ] Causal effect estimation
- [ ] Robustness checks
- [ ] Visualization & reporting

---

## TIER 14: DECISION-MAKING & MLE JUDGMENT (8 concepts)

### When to Use Which Method
- [ ] Flowchart: "Which method should I use?"
  - [ ] Do I have RCT data? → Analyze as-is
  - [ ] Observational data + SUTVA + Unconfoundedness? → Propensity score or regression
  - [ ] Observational + parallel trends? → DiD
  - [ ] Natural experiment? → IV or RD
  - [ ] Need heterogeneous effects? → Causal forests or DML
- [ ] Tradeoffs: Bias vs variance vs interpretability
- [ ] Method selection checklist
- [ ] Common pitfalls & when methods fail

### Real-World Problem Solving
- [ ] Diagnosing causal inference problems from business scenarios
- [ ] Building causal hypotheses from data
- [ ] Choosing estimands (ATE vs ATT vs CATE)
- [ ] Communicating assumptions to non-technical stakeholders
- [ ] Presenting results & making recommendations

---

## TIER 15: ADVANCED TOPICS (10 concepts)

### Advanced Methods & Theory
- [ ] Orthogonal machine learning
- [ ] Neural network causal models
- [ ] Causal discovery algorithms
  - [ ] PC algorithm
  - [ ] FCI algorithm
  - [ ] Score-based methods
- [ ] Identifiability theory (advanced)
- [ ] Causal inference with high-dimensional data

### Dynamic Treatment Regimes
- [ ] Optimal dynamic treatment regimes
- [ ] Sequential decision making
- [ ] Q-learning / Value iteration
- [ ] Reinforcement learning for causal effects
- [ ] Adaptive interventions

### Frontier Topics
- [ ] Causal inference from images/text (emerging)
- [ ] Causal inference in reinforcement learning
- [ ] Transfer learning & causal generalization
- [ ] Offline reinforcement learning
- [ ] Causal discovery from time series

---

## TIER 16: COMMON PITFALLS & RED FLAGS (10 concepts)

### Statistical Mistakes
- [ ] Collider bias / Conditioning on bad variables
- [ ] Post-treatment bias / Controlling for mediators
- [ ] Reverse causality / Simultaneity bias
- [ ] Survivorship bias
- [ ] Looking at proportions without denominators

### Methodological Mistakes
- [ ] Ignoring unobserved confounders
- [ ] Positivity violations without realizing
- [ ] Overfitting in propensity score models
- [ ] Not checking assumptions (parallel trends, etc.)
- [ ] Multiple testing without correction

### Communication Mistakes
- [ ] Claiming causation without sufficient assumptions
- [ ] Overstating effect sizes
- [ ] Ignoring heterogeneous effects
- [ ] Not discussing limitations / alternative explanations
- [ ] Forgetting to mention unobserved confounders

### Practical Mistakes
- [ ] Using wrong unit of randomization
- [ ] Peeking at results mid-experiment
- [ ] Running experiments with insufficient power
- [ ] Not accounting for compliance
- [ ] Ignoring network interference

---

## TIER 17: INTERVIEW PATTERNS & COMPANY-SPECIFIC FOCUS (6 categories)

### Meta / Facebook Focus
- [ ] Network effects & interference (SUTVA violations)
- [ ] Large-scale experimentation
- [ ] Social network causal inference
- [ ] User engagement metrics
- [ ] Feed/ranking causality

### Google Focus
- [ ] Ad auction & attribution
- [ ] Search relevance experimentation
- [ ] Measurement challenges
- [ ] Unconfoundedness in observational data
- [ ] Complex experiment designs

### Uber Focus
- [ ] Marketplace two-sided effects
- [ ] Driver vs rider heterogeneous effects
- [ ] Consistency assumptions (treatment delivery)
- [ ] Geospatial interference
- [ ] Real-time decision making

### Netflix Focus
- [ ] Recommendation system causality
- [ ] Churn prediction & retention
- [ ] Estimand choice (ATE vs ATT)
- [ ] Long-term vs short-term effects
- [ ] Compliance with recommendations

### Airbnb Focus
- [ ] Pricing & demand elasticity
- [ ] Positivity/overlap issues (high-price segments)
- [ ] Heterogeneous effects by property type
- [ ] Supply-side causal inference
- [ ] Network effects (booking patterns)

### LinkedIn Focus
- [ ] Measurement assumptions
- [ ] LATE / Local treatment effects
- [ ] Job search causality
- [ ] Engagement metrics
- [ ] Econometric modeling

---

## 🎯 MASTER PROGRESS TRACKER

Total Concepts: **200+**

Progress by Tier:
- [ ] Tier 1: Foundations (15 concepts)
- [ ] Tier 2: Assumptions (12 concepts)
- [ ] Tier 3: Estimands (8 concepts)
- [ ] Tier 4: Identification (9 concepts)
- [ ] Tier 5: Randomization (11 concepts)
- [ ] Tier 6: Propensity Score (13 concepts)
- [ ] Tier 7: Regression (9 concepts)
- [ ] Tier 8: Quasi-Experimental (15 concepts)
- [ ] Tier 9: Metalearners (11 concepts)
- [ ] Tier 10: Complex Settings (9 concepts)
- [ ] Tier 11: Robustness (8 concepts)
- [ ] Tier 12: Applications (10 concepts)
- [ ] Tier 13: Implementation (12 concepts)
- [ ] Tier 14: Decision-Making (8 concepts)
- [ ] Tier 15: Advanced Topics (10 concepts)
- [ ] Tier 16: Common Pitfalls (10 concepts)
- [ ] Tier 17: Company Focus (6 categories)

**Estimated Time to Master**: 80-100 hours of deep learning

---

## 📌 HOW TO USE THIS CHECKLIST

1. **As you learn each concept** through Sections 1-5, tick it off here
2. **At the end of each section**, check: "Did I cover all relevant concepts?"
3. **After Section 5**, scan for uncovered concepts (Tier 15-16 advanced topics)
4. **Bonus deep dives**: Master any gaps in Tier 15 (Advanced), Tier 16 (Pitfalls), Tier 17 (Company focus)
5. **Interview prep**: Use Tier 14 (Decision-Making) as your final cheat sheet

---

## 🎓 Learning Path Through Sections

**Section 1** → Tiers 1, 2, 3, 4
**Section 2** → Tiers 5, 6, 7
**Section 3** → Tier 8 (DiD & Synthetic Control)
**Section 4** → Tier 8 (IV & RD)
**Section 5** → Tier 9 (Metalearners & DML)
**Bonus** → Tiers 10, 11, 13, 14, 15, 16, 17

