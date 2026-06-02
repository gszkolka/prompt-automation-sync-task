# AI Prompt Engineering & Automation Portfolio

Welcome. This repository contains enterprise-grade prompt engineering frameworks designed to optimize costs, reduce operational friction, and automate workflows using Large Language Models (LLMs).

---

## Case Study 1: Production-Ready Customer Support Triage & Automation (B2B SaaS)

### 1. Business Problem & Context
SyncTask is a B2B project management SaaS platform ($49/month per user). The customer support department faced critical bottlenecks during service outages. Critical emails from high-value users requesting immediate cancellation (churn risk) were mixed into a generic support queue, causing significant response delays, violation of SLAs, and financial loss.

### 2. Solution Architecture
I designed an advanced, structured Megaprompt leveraging Markdown delimiters ([ROLE], [CONTEXT], [TASK]) to enforce deterministic outputs. The objective is to parse unstructured raw customer emails and force the LLM to output a clean, validated JSON object to be consumed directly by a production backend API or CRM system (e.g., HubSpot, SendGrid) without parsing errors.

#### The Prompt Framework:
[ROLE]
Act as a Senior Technical Support Engineer and Customer Retention Specialist for the software company "SyncTask" (project management SaaS). Your tone must be highly professional, empathetic, solution-oriented, and direct.

[COMPANY CONTEXT]
- SyncTask costs $49/month per user.
- Cancellation Policy: If a customer wants to cancel, offer one month free or a 1-on-1 consultation session before proceeding.
- Billing Policy: If there is a duplicate charge, escalate to finance and promise a resolution within 24 hours.

[TASK]
Analyze the attached customer email below and generate a structured output in JSON format with the following keys:
1. "category": Classify the email strictly into one of these options: [Technical Support, Billing, Cancellation, Feedback].
2. "urgency_level": Assign a level from 1 to 5 (where 5 is critical/imminent customer churn).
3. "customer_sentiment": Briefly describe the emotional state of the customer (e.g., Frustrated, Angry, Confused, Neutral).
4. "draft_response": Draft a response email in English applying de-escalation techniques. For billing or cancellation, apply company policies mentioned in the context.

[CUSTOMER EMAIL]
"Hi SyncTask team, I am extremely frustrated. Your platform has been down for the last two hours and my team couldn't access our project boards before a major client presentation. This is unacceptable for a service we pay $49/month for. I want a refund for this month, and honestly, if this happens again, I want to cancel my subscription immediately. Let me know how you will fix this."

---

### 3. Empirical Benchmarking (Gemini 1.5 Pro vs. Claude 3.5 Sonnet)

To ensure system reliability before deployment, I ran cross-model evaluation testing on the pipeline.

#### Model A: Gemini 1.5 Pro
- Output Structure: Flat JSON.
- Logic Evaluation: Gemini processed the query at high speed and delivered a highly natural response tone. However, it failed strict business conditional constraints by offering all compensation incentives simultaneously (refund + 1-on-1 consultation), instead of sequencing them according to company guidelines.

#### Model B: Claude 3.5 Sonnet (Winner)
- Output Structure: Nested JSON (Separating subject and body for API communication).
- Logic Evaluation: Claude showcased superior architectural understanding by automatically nesting the draft_response into subject and body keys. It handled the business logic flaws seamlessly, providing a corporate post-mortem framing (48-hour root-cause analysis promise) which matches enterprise software standards.

---

### 4. Production Recommendation & Technical Takeaways

- Format Determinism: Claude 3.5 Sonnet is recommended for production deployment due to its zero-fail adherence to complex JSON schemas, preventing system crashes during runtime backend extraction.
- Business ROI: This automated workflow reduces initial triage overhead by an estimated 70%, identifying critical churn risks instantly and generating production-ready email responses with zero human intervention.
