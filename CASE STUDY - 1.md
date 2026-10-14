# Experiment 1: Case Study on the Analysis of SDLC Models Applied to a Real-World Software Application

## 1. Aim

To analyze popular Software Development Life Cycle (SDLC) models and evaluate which model best suits a real-world software application.

## 2. Objectives

- Understand the phases of the SDLC.
- Compare Waterfall, V-Model, Iterative, Spiral, and Agile (Scrum) models.
- Apply the analysis to a real-world application and justify a model choice.

## 3. Requirements

- Reference material on SDLC models (textbook or online documentation)
- A chosen real-world application (example used here: an **online food delivery application**)
- Word processor or Markdown editor

## 4. Theory

### 4.1 SDLC Phases

| Phase | Description |
|---|---|
| Requirement analysis | Gather and document what the system must do |
| Design | Architecture, database, and UI design |
| Implementation | Coding the system |
| Testing | Verify that the system meets requirements |
| Deployment | Release to users |
| Maintenance | Fix defects, adapt and enhance after release |

### 4.2 Overview of Models

| Model | Key Idea | Strengths | Weaknesses | Suitable When |
|---|---|---|---|---|
| Waterfall | Sequential phases, no overlap | Simple, well documented, easy to manage | Inflexible, late testing, costly changes | Requirements are fixed and well understood |
| V-Model | Each development phase has a matching test phase | Early test planning, high quality | Rigid, little tolerance for change | Safety-critical or regulated systems |
| Iterative / Incremental | Build in repeated cycles, each adding features | Early working software, easier change | Needs good planning and design | Requirements partly known, phased delivery |
| Spiral | Iterations driven by risk analysis | Strong risk management | Complex, costly, needs risk expertise | Large, high-risk projects |
| Agile (Scrum) | Short sprints, continuous feedback | Adaptable, customer involvement, fast delivery | Less documentation, scope creep risk | Changing requirements, fast time to market |
| DevOps (extension) | Continuous integration and delivery with operations | Rapid, reliable releases | Needs automation culture and tooling | Continuously evolving web/cloud products |

## 5. Case Study: Online Food Delivery Application

### 5.1 Background

A start-up plans a mobile and web application where customers browse restaurants, order food, pay online, and track delivery. Restaurants manage menus and orders; delivery partners accept and complete deliveries.

### 5.2 Key Project Characteristics

| Characteristic | Observation |
|---|---|
| Requirements stability | Evolving; features change with user feedback and competition |
| Time to market | Critical |
| Risk level | Medium (payments, location data, availability) |
| User involvement | High; feedback needed continuously |
| Release frequency | Frequent (weekly or bi-weekly) |
| Team size | Small to medium, cross-functional |

### 5.3 Evaluation Matrix

Score each model from 1 (poor) to 5 (excellent) for this project.

| Criterion | Weight | Waterfall | V-Model | Iterative | Spiral | Agile |
|---|---|---|---|---|---|---|
| Handles changing requirements | 5 | 1 | 1 | 4 | 4 | 5 |
| Speed of delivery | 4 | 2 | 2 | 4 | 3 | 5 |
| Risk management | 3 | 2 | 3 | 3 | 5 | 3 |
| Customer feedback | 4 | 1 | 1 | 4 | 3 | 5 |
| Documentation and traceability | 2 | 5 | 5 | 3 | 4 | 2 |
| Cost predictability | 2 | 4 | 4 | 3 | 2 | 3 |
| **Weighted total** | | **41** | **44** | **73** | **71** | **84** |

*Calculation example (Agile): 5×5 + 4×5 + 3×3 + 4×5 + 2×2 + 2×3 = 25 + 20 + 9 + 20 + 4 + 6 = 84. Recompute the totals if you change any score or weight.*

### 5.4 Recommended Model

**Agile (Scrum)**, supported by DevOps practices (CI/CD), is the best fit because requirements evolve, rapid releases are essential, and customer feedback drives priorities. A short risk-assessment activity (borrowed from the Spiral model) can be added for payment and security components.

### 5.5 Sample Mapping to Scrum

| Scrum Element | Application in Case Study |
|---|---|
| Product owner | Business lead of the start-up |
| Scrum master | Team facilitator |
| Development team | Developers, tester, UI designer |
| Product backlog | Registration, restaurant listing, cart, payment, tracking, ratings |
| Sprint length | 2 weeks |
| Sprint 1 goal | User registration, login, restaurant listing |
| Sprint 2 goal | Cart and checkout |
| Sprint 3 goal | Payment integration and order tracking |
| Ceremonies | Planning, daily stand-up, review, retrospective |

## 6. Procedure

1. Select a real-world application (use the example or choose your own).
2. List its characteristics (requirements stability, time, risk, size).
3. Study each SDLC model and note strengths and weaknesses.
4. Build the evaluation matrix with weights suited to your application.
5. Compute weighted scores and identify the best-fit model.
6. Justify the choice and outline how it would be applied.

## 7. Observations

| Item | Your Observation |
|---|---|
| Application chosen | |
| Highest-scoring model | |
| Second-best model | |
| Reason for selection | |

## 8. Result

The SDLC models were compared against the characteristics of the chosen application, and the most suitable model was selected with justification.

## 9. Conclusion

No single SDLC model suits every project. The selection depends on requirement stability, risk, delivery speed, and stakeholder involvement. For fast-changing consumer applications, Agile with DevOps is usually most effective.

## 10. Viva Questions

1. What are the phases of the SDLC?
2. Why is Waterfall unsuitable for projects with changing requirements?
3. How does the V-Model differ from Waterfall?
4. What is the role of risk analysis in the Spiral model?
5. What are the main roles in Scrum?
6. When would you choose the V-Model over Agile?

## 11. References

- Pressman, R. S., *Software Engineering: A Practitioner's Approach*
- Sommerville, I., *Software Engineering*
- The Scrum Guide: https://scrumguides.org
