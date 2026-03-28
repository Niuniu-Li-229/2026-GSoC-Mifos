# GSoC 2026 Application
## The Mifos Initiative - Mifos X Smart Contract & Loan Agreement Summarization with LLMs
**Applicant:** Wanjing Yang | wanjingyang29@gmail.com
**Slack:** Wanjing Yang 
**Timezone:** PST (UTC-7)
**GitHub:** https://github.com/Niuniu-Li-229/2026-GSoC-Mifos

---

### 1. Project idea:
Mifos X Smart Contract & Loan Agreement Summarization with LLMs (Medium, 175 hours)

---

### 2. Briefly cover what you expect to complete in this project and when, including a detailed description and project plan:

Loan agreements in microfinance are often written in dense legal language that is inaccessible to low-literacy borrowers — creating real over-indebtedness risk at the point of loan origination. This project builds a proof-of-concept Python service that uses an LLM to automatically generate plain-language summaries of loan agreements, making key terms transparent and understandable for clients.

**What I will build:**
- A lightweight **Streamlit web interface** where a loan officer can paste or upload a loan agreement or select a Mifos X product template
- A **Python/FastAPI backend service** that sends the agreement text to an LLM (OpenAI GPT-4o, Claude, or Ollama for on-premise) with a carefully engineered prompt
- Prompts designed to extract and explain six key fields: loan amount, interest rate and type (flat vs. declining balance), repayment schedule, total cost of credit, late fee structure, and consequences of default
- **SMS/WhatsApp-formatted output** for easy sharing in the field
- A **systematic evaluation** comparing multiple LLMs and prompts on accuracy, completeness, and readability — with a final recommendation report
- A **REST API endpoint** (`POST /summarize`) for future integration into Mifos X web or mobile apps
- Some **research** if time allowed: previous research have shown improvement of the AI summarization with RAG, Multi-agent etc, if sophiscated prompt engineering is not enough, try to explore RAG/Multi-agent way to improve.

**Project Plan:**

| Period | Deliverables |
|---|---|
| Community bonding (May 1–26) | Set up Mifos X locally, collect sample loan agreements for evaluation, finalize prompt strategy with mentors |
| Weeks 1–2 (May 27–June 9) | Streamlit UI, text parsing, OpenAI + Anthropic API integration |
| Weeks 3–4 (June 10–23) | Core prompting service, structured JSON output, initial testing |
| Weeks 5–6 (June 24–July 7) | Ollama local inference integration, begin LLM comparison |
| Weeks 7–8 (July 8–21) | SMS/WhatsApp formatter, multilingual exploration, midterm deliverables |
| Weeks 9–10 (July 22–Aug 4) | Research phase: evaluate prompt engineering ceiling; explore RAG pipeline and/or multi-agent verification if needed; document findings | 
| Weeks 11–12 (Aug 5–18) | Full evaluation across models and prompt variants, and reseach approaces; REST API finalization |
| Week 13 (Aug 19–26) | Documentation, error handling polish, final report, demo, submission |

---

### 3. Any resources you will need to undertake the project:

- OpenAI API access — already have an active account
- Anthropic (Claude) API access — already have an active account
- Ollama for local model inference — free, runs locally, no cost
- No VMs required; all development will run locally or on free-tier cloud

---

### 4. Why are you the right person for this project?

Most applicants will need to learn what loan agreements contain and what matters to borrowers. I already know this from years of professional practice.

At IFC (World Bank Group), I spent two years reading, modeling, and summarizing complex financial risk documents for non-specialist audiences — capital adequacy reports, stress test results, risk disclosures. Writing clear summaries of dense financial documents for senior management is directly the skill this project requires at a prompt engineering level.

I have used Python professionally for data pipelines and reporting automation at Citigroup, and I have immediate access to both OpenAI and Anthropic APIs. I can begin substantive work on the evaluation framework from day one.

Working at IFC also gave me direct exposure to the financial inclusion challenge Mifos is solving. I have seen how inaccessible financial language creates real barriers for underserved borrowers, which makes this project personally meaningful beyond the technical challenge.

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

GitHub: https://github.com/Niuniu-Li-229/2026-GSoC-Mifos

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

- **Mifos X:** In progress — currently setting up local development environment following the Getting Started Guide. [Update with screenshot before submitting]
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
