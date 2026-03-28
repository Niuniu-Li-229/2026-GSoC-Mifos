# GSoC 2026 Application
## The Mifos Initiative - Intelligent Loan Amortisation & What-if Simulator Servic
**Applicant:** Wanjing Yang | wanjingyang29@gmail.com
**Slack:** Wanjing Yang 
**Timezone:** PST (UTC-7)
**GitHub:** https://github.com/Niuniu-Li-229/2026-GSoC-Mifos/tree/main/Loan%20Simulator

---

### 1. Project idea:
Intelligent Loan Amortisation & What-if Simulator Servic (Small, 90 hours)

---

### 2. Briefly cover what you expect to complete in this project and when, including a detailed description and project plan:

Loan officers and clients often need to understand how different loan structures affect repayment — but currently there is no standalone, API-accessible simulation tool in the Mifos ecosystem. This project builds a lightweight Python microservice that provides accurate loan amortization calculations and interactive "what-if" scenario analysis, exposed via a clean REST API that can be called from the Mifos X web app or mobile apps.

**What I will build:**
- A **core calculation engine** in Python implementing all repayment methods supported by Mifos X: flat rate, declining balance, and equal principal payment schedules. All monetary calculations will use Python's (`decimal`) module for precision - floating point errors are unacceptable in financial software.
- **What-if scenario support** for prepayment, missed payments, interest rate changes (e.g. loan restructuring), and moratorium periods - returning updated amortization schedules and revised totals.
- A **FastAPI REST service** exposing a clean APT that accepts loan parameters and returns detailed amortization tables, period-by-period principal/interest breakdowns, and summary totals.
- A **Mifos X integration endpoint** that fetches live loan details from Mifos X via its API, allowing loan officers to run simulations directly on existing loans (e.g. "what if we restructure this loan with a 2-month moratorium?").
- Full **API documentation** via FastAPI's built-in OpenAPI/Swagger interface, plus a Python client SDK for easy integration by other Mifos developers.

**What-if Scenario Supported:**
| Scenario | Description |
|---|---|
| Prepayment        |  Client pays extra; recalculate remaining schedule |
| Missed Payment    |  Simulate arrears accumulation and revised payoffs |
| Rate change       |  Restructing with new interest rate from period N  |
| Suspension        |  Grace period with interest-only or full deferral  |
| Tenure extension  |  Reduce each payments by extending loan term       |

**Project Plan:**

| Period | Deliverables |
|---|---|
| Community bonding (May 1–26) | Study Mifos X loan product configurations, confirm supported repayment methods with mentors, set up repo and local environment |
| Weeks 1–2 (May 27–June 9) | Core calculation engine: flat rate, declining balance, equal principal; unit tests for all methods using (`decimal`) arithmetic |
| Weeks 3–4 (June 10–23) | What-if scenario engine; FastAPI endpoints (`POST /amortize, POST /simulate`); OpenAPI documentation |
| Weeks 5–6 (June 24–July 7) | Mifos X live loan integration (optional endpoint); Python client SDK; final testing and documentation |
| Weeks 7–8 (July 8–14) | Code cleanup, final documentation, GSoC report, demo |

---

### 3. Any resources you will need to undertake the project:

- Local Python environment — no cost
- Mifos X demo environment (sandbox.mifos.community) for testing the live loan integration endpoint
- No VMs or paid AI APIs required for this project

---

### 4. Why are you the right person for this project?

Loan amortization is not an abstract concept for me and I have done the work professionally. At IFC (World Bank Group), I built and maintained financial projection models that included loan portfolio modeling, interest calculation under different methodologies, and scenario analysis for capital adequacy purposes. At Citigroup, I automated risk reporting pipelines in Python and SQL.

Specifically relevant to this project:

- I have built declining-balance and flat-rate models in Excel and Python for production use at IFC. I understand the edge cases: how rounding accumulates across a schedule, how a moratorium affects total interest, why floating-point arithmetic produces incorrect results in financial calculations and must be replaced with decimal. 
- I have direct experience with the "what-if" use case. At IFC, I ran restructuring scenarios for management: what happens to capital ratios if a portfolio of loans is rescheduled? That analytical instinct transfers directly to designing the scenario simulation feature.
- I hold an FRM certification, which required deep study of fixed income mathematics and loan pricing which are the theoretical foundation underlying this project.

---

### 5. Current area of study:

Master of Science in Computer Science (CS Align program), Khoury College of Computer Science, Northeastern University — Spring 2026, first year. Previously: MS in Finance (STEM-certified), Simon Business School, University of Rochester (2020).

---

### 6. Contact information and preferred method of contact:

- Email: wanjingyang29@gmail.com
- Slack: Wanjing Yang — preferred for day-to-day communication
- LinkedIn: linkedin.com/in/wyang37
- Timezone: PST (UTC-7)

---

### 7. Career goals:

I am transitioning from financial risk management into software engineering and ML/AI, with a focus on applied AI in fintech and data science. My goal is to leverage my finance domain expertise alongside emerging CS skills to work on real-world problems at the intersection of AI and financial services — ideally in roles that have measurable social or economic impact. GSoC with Mifos is a pivotal step: it would give me my first open source contribution, hands-on LLM engineering experience, and a concrete project that bridges both worlds.

---

### 8. Links to source code or websites:

GitHub: https://github.com/Niuniu-Li-229/2026-GSoC-Mifos/tree/main/Loan%20Simulator

---

### 9. Slack nickname:

Wanjing Yang — introduced myself in #wg-ai-for-all and received a personal response from Priyanshu Tiwari.

---

### 10. Contributions to other open source projects outside of Mifos:

No prior open source contributions. This is my first cycle. I am actively working to make my first contribution to the relevant Mifos repository before the deadline.

---

### 11. Have you interacted with any of our mentors?

Yes — Priyanshu Tiwari responded to my introduction in the #wg-ai-for-all Slack channel and invited me to share my proposal for review via DM.

---

### 12. Previous experience with Angular/Java/Spring/Hibernate/MySQL/Android/DevOps:

- **Java:** Basic level — currently studying in NEU CS Align program
- **MySQL/SQL:** Proficient — used extensively at IFC and Citigroup for data pipelines and reporting
- **Angular/Spring/Hibernate/Android/DevOps:** Limited exposure — not directly required for this project, which is Python-based

---

### 13. Other commitments this summer:

Full-time GSoC commitment. I am enrolled in the NEU CS Align program and may take one course during the summer term, which would not conflict with GSoC hours. No internship or employment commitments planned.

---

### 14. Which Mifos open source projects have you deployed?

- **Mifos X:** In progress — currently setting up local development environment following the Getting Started Guide. Will update the screenshot before final submission.
- Payment Hub EE: N/A
- Mifos Gazelle: N/A
- Mobile Applications: N/A

---

### 15. Detail how you installed them and provide a screenshot:

Currently setting up Mifos X locally using Docker following the Apache Fineract Getting Started Guide. Will include screenshot of running environment before final submission.

---

### 16. Patches or source code submitted to Mifos Projects:

No submissions yet. I am actively working on a first contribution to the community-ai repository, which is directly relevant to this proposal. I will update this before the March 31 deadline.

---

### 17. What motivates you most about working with the Mifos Initiative?

At IFC, I worked on financial sustainability projects for institutions serving clients in developing economies. I saw firsthand that the barrier between a borrower and a fair loan often comes down to whether they can understand the document in front of them. Mifos is building the infrastructure to serve the world's 2 billion unbanked — and this project addresses one of the most human parts of that challenge: whether a client actually understands what they are agreeing to. That specificity of impact, applied through open-source software, is what makes Mifos different from any other GSoC organization I considered.

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
