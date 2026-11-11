# SECTION-BY-SECTION MAPPING & COMPANY INTERVIEW QUESTIONS

---

## SECTION 1: Potential Outcomes & A/B Testing Assumptions (6 Questions)

**Topics Covered**: Tier 1, Tier 2, Tier 3, Tier 4

### Q1: Meta - SUTVA Violations & Network Interference ⭐ HARD
**What they test**: SUTVA assumption breaking down in marketplace

Topics needed:
- [Tier 1] SUTVA, SUTVA violations, network effects
- [Tier 2] ATE vs estimands
- [Tier 3] Randomization pitfalls
- [Tier 4] Spillover detection, interference modeling

**Key concepts**: No interference assumption, general equilibrium, equilibrium treatment effects

---

### Q2: Google - Randomization, Exchangeability, ITT ⭐ HARD
**What they test**: Understanding compliance, assignment vs treatment, measurement

Topics needed:
- [Tier 3] Randomization, unconfoundedness, overlap
- [Tier 2] ITT definition
- [Tier 4] Non-compliance handling, 2SLS

**Key concepts**: ITT ≠ ATE, LATE, treatment assignment vs treatment received

---

### Q3: Netflix - Estimand Choice (ATE vs ATT)
**What they test**: Choosing right estimand for business context

Topics needed:
- [Tier 2] ATE, ATT, CATE, LATE definitions
- [Tier 4] Regression for RCT
- [Tier 8] Decision tree for estimand

**Key concepts**: When to report ATE vs ATT, heterogeneous effects

---

### Q4: Uber - Consistency & Treatment Delivery ⭐ HARD
**What they test**: Well-defined treatment, dose variation

Topics needed:
- [Tier 1] Causal concepts, causation vs correlation
- [Tier 3] Consistency assumption
- [Tier 4] RCT design issues

**Key concepts**: Hidden treatment versions, dose-response, delivery mechanism

---

### Q5: Airbnb - Positivity, Overlap, CATE ⭐ HARD
**What they test**: Heterogeneous effects, common support issues

Topics needed:
- [Tier 2] CATE, policy value
- [Tier 3] Overlap/Positivity violations
- [Tier 5] Meta-learners (S/T/X/R), causal forests
- [Tier 7] Policy learning, CATE estimation

**Key concepts**: When you can't estimate effect (no overlap), segmentation, heterogeneity

---

### Q6: LinkedIn - LATE, Measurement, Proxy Variables ⭐ HARD
**What they test**: IV with unmeasured confounders, proxy approach

Topics needed:
- [Tier 2] LATE, CACE
- [Tier 6] Instrumental variables, relevance/exclusion assumptions
- [Tier 7] Proxy variables, sensitivity analysis

**Key concepts**: LATE interpretation, using assignment as instrument, measurement error

---

## SECTION 2: Confounding & Propensity Score Methods (4 Questions)

**Topics Covered**: Tier 3, Tier 5.2, Tier 5.3

### Topics to Learn:
- [ ] Propensity score methods (matching, IPTW, DR)
- [ ] Covariate balance
- [ ] Observational vs confounders
- [ ] Selection bias

### Questions Map:
- Meta Q: "Adjust for confounders - which approach?"
- Google Q: "Propensity score or matching?"
- Netflix Q: "Balance check & sensitivity analysis"
- Uber Q: "Entropy balancing vs covariate matching"

---

## SECTION 3: Difference in Differences & Panel Data (4 Questions)

**Topics Covered**: Tier 6.2, Tier 3, Tier 5

### Topics to Learn:
- [ ] Parallel trends assumption
- [ ] Staggered DiD
- [ ] Event study design
- [ ] Panel data issues

### Questions Map:
- Amazon Q: "Policy rollout across regions"
- Google Q: "Multiple cohorts, timing issues"
- Netflix Q: "When parallel trends fails"
- Airbnb Q: "Seasonal confounding in panels"

---

## SECTION 4: Instrumental Variables & Encouragement (4 Questions)

**Topics Covered**: Tier 6.1, Tier 2, Tier 3

### Topics to Learn:
- [ ] IV assumptions (relevance, exclusion)
- [ ] 2SLS
- [ ] LATE vs ATE
- [ ] Weak instruments

### Questions Map:
- Meta Q: "Natural experiment - is it valid?"
- LinkedIn Q: "Randomized encouragement design"
- Uber Q: "LATE vs causal effect interpretation"
- Google Q: "Multiple instruments, which to use?"

---

## SECTION 5: Regression Discontinuity & Threshold Policies (4 Questions)

**Topics Covered**: Tier 6.3, Tier 3, Tier 5

### Topics to Learn:
- [ ] Sharp vs Fuzzy RD
- [ ] Bandwidth selection
- [ ] Local vs global effects
- [ ] Graphical analysis

### Questions Map:
- Airbnb Q: "Revenue thresholds trigger treatment"
- LinkedIn Q: "User level cutoff for feature rollout"
- Netflix Q: "Subscription tier changes"
- Uber Q: "Rating-based driver incentives"

---

## SECTION 6: Other Topics & Advanced (5 Questions)

**Topics Covered**: Tier 7, Tier 8, Tier 9, Tier 10

### Topics to Learn:
- [ ] Heterogeneous effects
- [ ] Multi-armed bandits
- [ ] Machine learning + causal
- [ ] Production systems

### Questions Map:
- Meta Q: "Personalization via CATE"
- Google Q: "Bandit algorithms & exploration"
- Netflix Q: "Real-time ML + causality"
- Airbnb Q: "Multi-treatment policies"
- LinkedIn Q: "Attribution + incrementality"

---

# WHICH TIER EACH INTERVIEW QUESTION REQUIRES

| Company | Question | Primary Tier | Secondary Tiers | Difficulty |
|---------|----------|--------------|-----------------|------------|
| Meta | Q1 SUTVA | Tier 3 | Tier 1, 7 | ⭐⭐⭐ HARD |
| Google | Q2 ITT | Tier 4 | Tier 3, 2 | ⭐⭐⭐ HARD |
| Netflix | Q3 ATE vs ATT | Tier 2 | Tier 4, 7 | ⭐⭐ MEDIUM |
| Uber | Q4 Consistency | Tier 3 | Tier 1 | ⭐⭐⭐ HARD |
| Airbnb | Q5 CATE | Tier 5,7 | Tier 2, 3 | ⭐⭐⭐ HARD |
| LinkedIn | Q6 LATE | Tier 6 | Tier 2, 7 | ⭐⭐⭐ HARD |
| Amazon | DiD Section | Tier 6 | Tier 3, 5 | ⭐⭐ MEDIUM |
| Microsoft | A/A Testing | Tier 4 | Tier 1 | ⭐⭐ MEDIUM |

---

# 🎯 HOW TO USE THIS MASTER CHECKLIST

## Step 1: Pick a Section (1-6)
Example: "Section 1: Potential Outcomes"

## Step 2: Learn Tier-by-Tier (don't skip tiers!)
Example: 
1. Learn Tier 1 Foundations (DAGs, causation vs correlation)
2. Learn Tier 2 Estimands (ATE, ATT, CATE)
3. Learn Tier 3 Assumptions (SUTVA, Randomization, Unconfoundedness)

## Step 3: As You Learn, CHECK OFF topics in this master list
✅ Instead of section-specific list, mark here

## Step 4: After Each Q&A in Section, Review Tier Topics
Q1 (Meta) → Did you understand: SUTVA (Tier 3)? Network effects (Tier 7)? 
If not, go back to that tier.

## Step 5: End of Section - Check if any Tier topics missed
After Section 1 complete: Did you learn all of Tier 1? Tier 2? Tier 3?
Missing topics → Learn them NOW before moving to Section 2.

## Step 6: End of Course - Final Gaps
Any Tier 1-10 topics still unchecked? 
Examples: "Never learned DragonNet (Tier 8)"
Fill gaps with deep dives.

---

# 📈 COMPLETION STRATEGY

**Hybrid Approach** (Recommended):

**Week 1**: 
- Learn Tier 1 (Foundations) - 4 hours
- Learn Tier 2 (Estimands) - 3 hours
- Teach Q1+Q2 from Section 1 - 4 hours
- Check marks on: Tier 1 (100%), Tier 2 (100%), Tier 3 (40% from Q&A)

**Week 2**:
- Learn Tier 3 (Assumptions) - 5 hours
- Learn Tier 4 (RCT methods) - 4 hours
- Teach Q3+Q4+Q5+Q6 from Section 1 - 6 hours
- Check marks on: Tier 3 (100%), Tier 4 (100%)

**Week 3**:
- Learn Tier 5 (Observational methods) - 8 hours
- Teach Section 2 (Propensity Scores) - 4 hours
- Check marks on: Tier 5 (100%)

**Week 4**:
- Learn Tier 6 (Unobserved confounders) - 6 hours
- Teach Section 3,4,5 (DiD, IV, RD) - 6 hours
- Check marks on: Tier 6 (100%)

**Week 5**:
- Learn Tier 7 (Advanced) - 6 hours
- Learn Tier 8 (ML Interface) - 4 hours
- Teach Section 6 - 4 hours
- Check marks on: Tier 7 (100%), Tier 8 (100%)

**Week 6**:
- Learn Tier 9 (Production) - 4 hours
- Learn Tier 10 (Interviews) - 6 hours
- Mock interviews - 8 hours
- Check marks on: Tier 9 (100%), Tier 10 (100%)

**Total: ~5-6 weeks, 80+ hours → Interview-ready mastery**

---

**Next Step**: Use this master checklist for your learning journey!  
As each section is taught, mark ✅ corresponding tier topics.  
At the end, you'll have complete mastery of causal ML.

