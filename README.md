# Causal ML Interview Handbook

**Personal learning handbook for mastering causal inference concepts for top-tier MLE interviews.**

## Goal
Achieve 70-85% retention of causal ML concepts through active recall, spaced repetition, and practical implementation. Interview-ready depth for Google, Uber, Meta, Airbnb, Netflix, LinkedIn.

## Structure

### 1. Potential Outcomes & A/B Testing Assumptions
Core framework for understanding causal estimation.

- [SUTVA (Stable Unit Treatment Value Assumption)](./01-potential-outcomes/01-sutva.md)
- [Unconfoundedness / Exchangeability](./01-potential-outcomes/02-unconfoundedness.md)
- [Positivity / Overlap](./01-potential-outcomes/03-positivity.md)
- [Consistency](./01-potential-outcomes/04-consistency.md)
- [Estimands: ATE, ATT, CATE, ITT, LATE](./01-potential-outcomes/05-estimands.md)

### 2. Interview Q&A
Real company questions with deep analysis.

- [Q1: Meta - SUTVA & Interference](./02-interview-qa/q1-meta-sutva.md)
- [Q2: Google - ITT & Non-Compliance](./02-interview-qa/q2-google-itt.md)
- [Q3: Netflix - ATE vs ATT](./02-interview-qa/q3-netflix-ate-att.md)
- [Q4: Uber - Consistency & Treatment Delivery](./02-interview-qa/q4-uber-consistency.md)
- [Q5: Airbnb - Positivity & Overlap Issues](./02-interview-qa/q5-airbnb-positivity.md)
- [Q6: LinkedIn - Measurement Assumptions](./02-interview-qa/q6-linkedin-measurement.md)

### 3. Code & Implementation
PySpark/Python examples for production.

- [Potential Outcomes Framework](./03-code/01-potential-outcomes-framework.py)
- [ATE Estimation](./03-code/02-ate-estimation.py)
- [SUTVA Violation Detection](./03-code/03-sutva-check.py)
- [Propensity Score Basics](./03-code/04-propensity-scores.py)

### 4. Decision Trees
Practical decision-making guides.

- [When to Use Which Method](./04-decision-trees/method-selection.md)
- [Assumption Violation Checklist](./04-decision-trees/assumption-checks.md)
- [Debugging Failed Experiments](./04-decision-trees/experiment-debugging.md)

### 5. Real Scenarios
Your personal case studies.

- [Scenarios Solved](./05-scenarios/README.md)

## Learning Progression

**Week 1:**
- Day 1-2: Learn SUTVA + Unconfoundedness
- Day 3: Learn Positivity + Consistency  
- Day 4: Learn Estimands
- Day 5: Practice Q1-Q4

**Week 2:**
- Mock interviews
- Deep dives into alternatives
- Code implementation

**Ongoing:**
- Weekly 10-min handbook review
- Monthly mock interview
- Before real interviews: Full day review

## Key Retention Strategies

✅ **Active Recall** - You answer questions, not just read  
✅ **Spaced Repetition** - Review on Day 1, 2, 3, 5, 7, 14, 30  
✅ **Elaboration** - Connect to existing knowledge  
✅ **Teaching Others** - Explain concepts in your own words  
✅ **Code Implementation** - Write PySpark examples  

## References

- Source: https://www.datainterview.com/blog/causal-inference-interview-questions
- Research: Ebbinghaus forgetting curve + Modern cognitive science
- Framework: Rubin Causal Model

---

**Status:** In progress (created Nov 11, 2026)  
**Target Completion:** Knowledge solidified by end of month  
**Interview Ready:** Yes

