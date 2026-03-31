# GSoC 2026 Application
## The Mifos Initiative - Intelligent Loan Amortization & What-if Simulator Service
**Applicant:** Wanjing Yang | wanjingyang29@gmail.com
**Slack:** Wanjing Yang 
**Timezone:** PST (UTC-7)
**GitHub:** https://github.com/Niuniu-Li-229/2026-GSoC-Mifos/tree/main/Loan%20Simulator

---

## 1. Project idea:
Intelligent Loan Amortization & What-if Simulator Service (Small, 90 hours)

---

## 2. Briefly cover what you expect to complete in this project and when, including a detailed description and project plan:

### 2.1 Problem Statement

Loan officers and clients regularly need to understand how different loan structures — or changes to an existing loan — affect repayment obligations. Questions like "what happens if I miss a payment?" or "can we restructure this loan with a 2-month moratorium?" currently require manual calculation or reliance on expert staff. There is no standalone, API-accessible simulation tool in the Mifos ecosystem to answer these questions instantly and accurately.

This creates friction at two critical moments: loan origination (clients cannot easily compare terms) and loan servicing (officers cannot quickly model restructuring options for distressed borrowers).

### 2.2 Proposed Solution

A lightweight Python microservice that provides accurate loan amortization calculations and interactive what-if scenario analysis, exposed via a clean REST API callable from the Mifos X web app or mobile apps.

### 2.3 Tech Stack

| Layer | Technology | Rationale |
|---|---|---|
| Backend service       | Python 3.11, FastAPI      | Lightweight, async, industry standard for ML/financial services |
| Financial arithmetic  | Python `decimal` module   | Prevents floating-point rounding errors across multi-period schedules |
| API documentation     | FastAPI OpenAPI/Swagger   | Auto-generated, always current |
| Testing               | pytest, pytest-asyncio    | Unit and integration coverage |
| Version control       | Git / GitHub              | Aligns with Mifos contribution workflow |
| Containerization      | Docker                    | Consistent deployment across environments |

### 2.4 System Architecture

![System Architecture Diagram](https://raw.githubusercontent.com/Niuniu-Li-229/2026-GSoC-Mifos/main/Loan%20Simulator/Loan%20Amortization%20and%20What-if%20Scenarios.drawio.svg)


### 2.5 Deliverables

- A **core calculation engine** in Python implementing all repayment methods supported by Mifos X: flat rate, declining balance, and equal principal payment schedules. All monetary calculations use Python's `decimal` module — floating-point errors are unacceptable in financial software.
- **What-if scenario support** for five scenarios, returning updated amortization schedules and revised totals:

| Scenario | Description |
|---|---|
| Prepayment       | Client pays extra; recalculate remaining schedule |
| Missed payment   | Simulate arrears accumulation and revised payoff |
| Rate change      | Restructuring with new interest rate from period N |
| Moratorium       | Grace period with interest-only or full deferral |
| Tenure extension | Reduce EMI by extending loan term |

### 2.6 Calculation Example

**Input:**
```json
{
  "principal": 20000,
  "annual_rate": 0.24,
  "tenure_months": 12,
  "method": "declining_balance"
}
```

**Output (first 3 periods):**
```json
{
  "schedule": [
    {"period": 1, "payment": 1893.11, "principal": 1493.11, "interest": 400.00, "balance": 18506.89},
    {"period": 2, "payment": 1893.11, "principal": 1523.01, "interest": 370.14, "balance": 16983.88},
    {"period": 3, "payment": 1893.11, "principal": 1553.52, "interest": 339.68, "balance": 15430.36}
  ],
  "total_interest": 2717.32,
  "total_cost": 22717.32
}
```

### 2.7 Project Timeline

| Period | Milestone | Deliverables |
|---|---|---|
| Community bonding (May 1–26)  | Setup & planning      | Study Mifos X loan product configurations, confirm repayment methods with mentors, set up repo |
| Weeks 1–2 (May 27–June 9)     | Calculation engine    | Flat rate, declining balance, equal principal; unit tests using `decimal` arithmetic |
| Weeks 3–4 (June 10–23)        | API & scenarios       | What-if scenario engine; `POST /amortize`, `POST /simulate`; OpenAPI documentation |
| Weeks 5–6 (June 24–July 7)    | Integration & SDK     | Mifos X live loan endpoint; Python client SDK; final testing and documentation |
| Week 7 (July 8–14)            | Wrap-up               | Code cleanup, final docs, GSoC report, demo |

### 2.8 Expected Outcomes & Impact

#### Technical Outcomes
- Working open-source Python microservice deployable by any Mifos X instance
- Five what-if scenarios with accurate `decimal`-based calculations
- `POST /amortize` and `POST /simulate` REST endpoints ready for Mifos X integration
- Python client SDK for easy adoption by other Mifos developers
- Full OpenAPI/Swagger documentation

#### Social Impact
- Loan officers can instantly show clients the true cost of a loan under different structures — supporting informed borrowing decisions
- Restructuring scenarios (moratorium, rate change) help officers serve distressed borrowers faster without manual calculation
- Smaller MFIs without specialist financial staff gain a reliable calculation tool previously requiring Excel expertise
- Reusable across all Mifos X deployments globally with no additional cost

### 2.9 Challenges & Mitigations

| Challenge | Mitigation |
|---|---|
| Floating-point rounding errors                    | Use Python `decimal` throughout; validate against known reference schedules in tests |
| Rounding accumulates across long schedules        | Implement standard "last payment adjustment" to absorb rounding difference |
| Mifos X API authentication for live loan endpoint | Study Fineract API auth during community bonding; scope as optional endpoint with graceful fallback |
| Edge cases: zero-interest loans, balloon payments | Explicitly test boundary conditions in unit test suite |
| Moratorium interest treatment varies by MFI       | Make moratorium type (interest-only vs. full deferral) a configurable parameter |

### 2.10 Testing, Documentation & Deployment

#### Testing Strategy
- **Unit tests (pytest):** each repayment method tested against manually verified reference schedules; all five what-if scenarios tested with known correct outputs
- **Precision tests:** verify `decimal` results match expected totals to 2 decimal places across 12, 24, and 36-month schedules
- **Integration tests:** FastAPI TestClient end-to-end tests for all endpoints
- **Target:** 100% accuracy on reference schedule test suite; all edge cases covered

#### Documentation
- README with quickstart, API reference, and usage examples
- OpenAPI/Swagger interface auto-generated by FastAPI
- Inline code documentation for all calculation functions

#### Deployment
- Dockerfile for containerized deployment
- Environment variable configuration for Mifos X API connection
- Supports local development and Docker-based production

---

### 2.11 Future Scope & Scalability

- **Direct Mifos X integration:** endpoints designed to be called from the loan origination workflow in the Mifos X web app or Android client with minimal frontend changes
- **Interactive UI:** a Streamlit front-end could give loan officers a visual amortization chart and what-if sliders — a natural follow-on project
- **Group loan support:** extend calculation engine to handle joint liability group loans with individual member tracking
- **Connection to LLM summarization:** the amortization output could feed directly into the loan agreement summarization project, auto-populating the repayment schedule field with calculated values rather than parsed text

---

## 3. Any resources you will need to undertake the project:

- Local Python environment — no cost
- Mifos X demo environment (sandbox.mifos.community) for testing the live loan integration endpoint

---

## 4. Why are you the right person for this project?

Loan amortization is not an abstract concept for me and I have done the work professionally. At IFC (World Bank Group), I built and maintained financial projection models that included loan portfolio modeling, interest calculation under different methodologies, and scenario analysis for capital adequacy purposes. At Citigroup, I automated risk reporting pipelines in Python and SQL.

Specifically relevant to this project:

- I have built declining-balance and flat-rate models in Excel and Python for production use at IFC. I understand the edge cases: how rounding accumulates across a schedule, how a moratorium affects total interest, why floating-point arithmetic produces incorrect results in financial calculations and must be replaced with decimal. 
- I have direct experience with the "what-if" use case. At IFC, I ran restructuring scenarios for management: what happens to capital ratios if a portfolio of loans is rescheduled? That analytical instinct transfers directly to designing the scenario simulation feature.
- I hold an FRM certification, which required deep study of fixed income mathematics and loan pricing which are the theoretical foundation underlying this project.

---

## 5. Current area of study:

Master of Science in Computer Science (CS Align program), Khoury College of Computer Science, Northeastern University — Spring 2026, first year. Previously: MS in Finance (STEM-certified), Simon Business School, University of Rochester (2020).

---

## 6. Contact information and preferred method of contact:

- Email: wanjingyang29@gmail.com
- Slack: Wanjing Yang — preferred for day-to-day communication
- LinkedIn: linkedin.com/in/wyang37
- Timezone: PST (UTC-7)

---

## 7. Career goals:

I am transitioning from financial risk management into software engineering and ML/AI, with a focus on applied AI in fintech and data science. My goal is to leverage my finance domain expertise alongside emerging CS skills to work on real-world problems at the intersection of AI and financial services — ideally in roles that have measurable social or economic impact. GSoC with Mifos is a pivotal step: it would give me my first open source contribution, hands-on LLM engineering experience, and a concrete project that bridges both worlds.

---

## 8. Links to source code or websites:

GitHub: https://github.com/Niuniu-Li-229/2026-GSoC-Mifos/tree/main/Loan%20Simulator

---

## 9. Slack nickname:

Wanjing Yang — introduced myself in #wg-ai-for-all and received a personal response from Priyanshu Tiwari.

---

## 10. Contributions to other open source projects outside of Mifos:

No prior contributions. Built a local prototype at github.com/Niuniu-Li-229/2026-GSoC-Mifos and will submit first formal PR during community bonding period.

---

## 11. Have you interacted with any of our mentors?

Yes — Priyanshu Tiwari responded to my introduction in the #wg-ai-for-all Slack channel and invited me to share my proposal for review via DM.

---

## 12. Previous experience with Angular/Java/Spring/Hibernate/MySQL/Android/DevOps:

- **Java:** Basic level — currently studying in NEU CS Align program
- **MySQL/SQL:** Proficient — used extensively at IFC and Citigroup for data pipelines and reporting
- **Angular/Spring/Hibernate/Android/DevOps:** Limited exposure — not directly required for this project, which is Python-based

---

## 13. Other commitments this summer:

Full-time GSoC commitment. I am enrolled in the NEU CS Align program and may take one course during the summer term, which would not conflict with GSoC hours. No internship or employment commitments planned.

---

## 14. Which Mifos open source projects have you deployed?

- **Mifos X:** In progress — currently setting up local development environment following the Getting Started Guide.
- Payment Hub EE: N/A
- Mifos Gazelle: N/A
- Mobile Applications: N/A

---

### 15. Detail how you installed them and provide a screenshot:

Deployed Apache Fineract and MySQL 8.0 via Docker on macOS Apple Silicon. Encountered a database connection issue (known Apple Silicon networking issue with latest Fineract image). Will resolve during community bonding period.
![Docker setup](https://raw.githubusercontent.com/Niuniu-Li-229/2026-GSoC-Mifos/main/Mifos%20X%20Setup/Mifos%20X%20Setup.png)

---

### 16. Patches or source code submitted to Mifos Projects:

No prior contributions. Built a local prototype at github.com/Niuniu-Li-229/2026-GSoC-Mifos and will submit first formal PR during community bonding period.

---

### 17. What motivates you most about working with the Mifos Initiative?

At IFC, one of my responsibilities was helping financial institutions understand the real cost of their lending portfolios — making sure the numbers were transparent and honest. This project does the same thing at the individual borrower level: it makes the math visible at the moment of origination and servicing, when it matters most. A loan officer being able to show a client "if you miss one payment, here is what your schedule looks like" is a small thing technically but significant for financial inclusion. Being able to contribute a reusable tool to the Mifos ecosystem that field officers across multiple countries can use is a meaningful application of the skills I have built over years.

---

### 18. Previously participated in Google Summer of Code?

No — this is my first GSoC application.

---

### 19. Applying to multiple organizations this year?

No — Mifos is my only application.

---

### 20. First choice organization:

N/A — applying only to Mifos.

---

### 21. Previously participated in any other internship programme with Mifos?

No.
