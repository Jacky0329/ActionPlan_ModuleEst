---
name: module_est_by_price_skill
description: "Expert technical project estimator. Use when: generating project quotations, estimating development costs, breaking down project modules, pricing software projects, calculating BE/FE/PM days, producing client-facing quotes, OR reverse-estimating scope from a target budget. Follows strict billing rates, complexity multipliers, and output format from the modEst constitution."
argument-hint: "Paste project requirements to quote, OR provide a target budget + project type for reverse estimation"
---

# Project Pricing & Estimation Skill

## When to Use

- A client or internal team provides a project description that needs a cost quotation (**forward estimation**).
- A client provides a **target budget** and you need to determine what scope fits within it (**reverse estimation**).
- You need to break down a software project into modules with day estimates.
- You need a professional quotation document with Executive Summary, Module Breakdown, Resource Note, and Next Steps.

## Constraints (NON-NEGOTIABLE)

1. **Never guess prices.** Every number must be derived from the formulas in the [constitution](./references/modEst_constitution.md).
2. **Always output the exact markdown table** defined in the constitution (Section IV / Reverse Output Format).
3. **Flag capacity warnings.** If calculated FE days exceed BE days for the project, add a warning that the project may bottleneck on frontend — the team's capacity is currently weighted ~3:1 toward backend and PM resources.
4. **Never under-tier to fit budget.** In reverse estimation, complexity tiers MUST reflect real technical difficulty — do NOT downgrade a Hard module to Medium just to squeeze it into budget.
5. **Always include mandatory base modules.** Every quotation MUST include "User & Role Management" and "CRUD Content Management" as separate line items per Principle IX. These MUST NOT be omitted or merged into other modules.
6. **Always determine portal configuration.** Before estimating, determine if the system needs 1 portal (user only) or 2 portals (user + backoffice). Apply the FE Portal Multiplier (1.0× for single, 1.5× for dual) to FE days per Principle X.
7. **Validate mandatory module pricing.** User & Role Management (1-portal) MUST cost RM 2,500–3,000. CRUD Content Management (1-portal) MUST cost RM 2,000–3,000. If below these ranges, re-examine day estimates.
8. **Requirements & UI/UX are team-provided.** Requirements discussion with the client and all UI/UX design are performed by the team — NOT the client. Quotations MUST NOT assume "client provides design mockups" or similar. The Executive Summary MUST state that requirements discussion and UI/UX design are included in the quoted scope (per Principle XI).

## Procedure — Input Validation (ALWAYS RUN FIRST)

Before doing any estimation, check that the input contains the minimum required information. If anything is missing or too vague, **STOP and ask** — do not guess or proceed with assumptions.

### Required Inputs

| # | Required | Missing → Ask |
| :---: | :--- | :--- |
| 1 | **Project description** — what the system does, who uses it, and what core features are needed | "Could you describe the system? What does it do, who are the users, and what are the main features needed?" |
| 2 | **Portal configuration** — does it need a user-facing portal only, or also a backoffice/admin panel? | "Will this system need an admin/backoffice portal in addition to the user-facing portal, or just one portal?" |
| 3 | **Budget (reverse mode only)** — a specific target budget in RM | "What is your target budget in RM for this project?" |

### Input Quality Check

Before proceeding, verify:

- [ ] **Project description is present** — at least 2–3 sentences describing what the system does.
  - ❌ Too vague: *"e-commerce app"*, *"school system"*, *"HR tool"*
  - ✅ Sufficient: *"An e-commerce platform for a local bakery — customers browse products, add to cart, checkout, and track orders. Admin can manage products, orders, and view sales reports."*
- [ ] **Portal configuration is clear** — either stated or clearly inferable from the description.
- [ ] **Budget is present (reverse mode)** — a specific RM figure, not a range like "under RM 30k" (if a range, use the lower bound and state so).

### If Input Is Insufficient

Ask all missing questions in a **single reply** using a numbered list. Do NOT ask one at a time.

**Example clarification request:**

> To prepare an accurate quotation, I need a few more details:
>
> 1. **Project description:** Could you describe the system in more detail? What does it do, who are the users, and what are the key features?
> 2. **Portal setup:** Will this system have a separate admin/backoffice panel, or is there only a single user-facing portal?
> 3. *(if reverse mode)* **Target budget:** What is the specific RM budget you want to work within?

Only proceed to estimation once **all required inputs** are confirmed.

---

## Procedure — Mode Detection

Read the user's input and determine the estimation mode:

- **Forward mode:** User provides a project description with NO budget cap → go to **[Forward Estimation (Steps 1–10)](#forward-estimation)**.
- **Reverse mode:** User provides a **target budget** (with or without a project description) → go to **[Reverse Estimation (Steps R1–R11)](#reverse-estimation)**.

If both a description AND a budget are provided, use **Reverse mode**.

---

## Forward Estimation

### Step 1 — Load the Constitution

Read the pricing constitution to get the current rates, formulas, and output format:

- [modEst_constitution.md](./references/modEst_constitution.md)

If the constitution file is missing or rates have changed, **STOP** and inform the user before proceeding.

### Step 2 — Determine Portal Configuration

Based on the project description, determine the portal configuration:

- **Single Portal (1.0×):** The system has only one user-facing frontend (e.g., customer app, public website).
- **Dual Portal (1.5×):** The system requires both a user-facing portal AND a backoffice/admin portal.

State the portal configuration in the Executive Summary.

### Step 2b — Confirm Service Scope

Per Principle XI, confirm and state in the Executive Summary that:

- **Requirements discussion** with the client is conducted by the team.
- **UI/UX design** (wireframes, mockups) is provided by the team.

Do NOT list "client provides design mockups" as an assumption.

### Step 3 — Decompose into Modules

Read the user's project description and break it into discrete technical modules. Each module must have:

- A clear, descriptive name (e.g., "User Authentication", "Payment Gateway Integration").
- A single complexity tier: **Simple** (1.0×), **Medium** (1.5×), or **Hard** (2.0×).
- If a module spans multiple tiers, assign the **highest applicable** tier.

**Mandatory modules (MUST always be included):**
1. **User & Role Management** — auth, RBAC, user profile CRUD, session management. Minimum Medium (1.5×).
2. **CRUD Content Management** — core business entity CRUD for the system's primary domain objects. Minimum Medium (1.5×).

### Step 4 — Estimate Days per Module

For each module, estimate independently:

| Field | Rule |
| :--- | :--- |
| **BE Days** | Backend effort in 0.25-day increments |
| **FE Days** | Frontend effort in 0.25-day increments |
| **PM/QA Days** | `0.15 × (BE Days + FE Days × Portal Multiplier)`, rounded to nearest 0.25 |

### Step 5 — Apply Complexity & Portal Multipliers

Multiply each role's raw days by the module's complexity multiplier,
and apply the portal multiplier to FE days:

```
Adjusted BE Days = Raw BE Days × Complexity Multiplier
Adjusted FE Days = Raw FE Days × Complexity Multiplier × Portal Multiplier
Adjusted PM/QA Days = Raw PM/QA Days × Complexity Multiplier
```

### Step 6 — Calculate Per-Module Cost

```
Module Cost = (Adjusted BE Days × 360) + (Adjusted FE Days × 300) + (Adjusted PM/QA Days × 200)
```

**Mandatory module validation:**
- User & Role Management (1-portal): MUST be RM 2,500–3,000. If below, re-examine days.
- CRUD Content Management (1-portal): MUST be RM 2,000–3,000. If below, re-examine days.

### Step 7 — Calculate Grand Total

```
Grand Total = Sum of all Module Costs × 1.20   (20% contingency buffer)
```

### Step 8 — Generate Output

Produce the quotation in **exactly** this structure (do not omit or reorder sections):

#### A. Executive Summary

- **Quote Date:** [today's date]
- **Validity:** 30 calendar days
- **Portal Configuration:** [Single Portal / Dual Portal (User + BO)]
- **Estimated Project Duration:** [Total adjusted days including 20% buffer] Days
- **Total Estimated Price:** RM [Grand Total]
- **Infrastructure Constraints:** *This quote does not include monthly cloud hosting (AWS/GCP/Azure), domain registration, paid third-party API subscriptions, or ongoing maintenance beyond the quoted scope.*
- **Included Services:** *Requirements discussion and gathering with the client, and all UI/UX design (wireframes, mockups) are included in the quoted scope.*

#### B. Module Breakdown

| Module Name | Complexity | BE Days | FE Days | PM/QA Days | Subtotal Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |

#### C. Resource Capacity Note

> *Reminder for internal planning:* Ensure frontend workload is balanced — the team operates with heavier backend capacity. Modules with heavy UI/UX requirements may become the schedule bottleneck.

If total FE days > total BE days, add:

> ⚠️ **Capacity Warning:** This project's frontend workload (X days) exceeds backend (Y days). Given the team's ~3:1 BE-to-FE capacity ratio, frontend delivery is the likely bottleneck. Consider augmenting FE resources or phasing UI-heavy modules.

#### D. Next Steps for Client

A brief, professional closing sentence inviting the client to approve the quote so development can begin.

### Step 9 — Self-Check

Before delivering, verify:

- [ ] All rates match the constitution (BE=360, FE=300, PM/QA=200).
- [ ] PM/QA days = 15% of (BE + FE × Portal Multiplier) per module.
- [ ] Complexity multiplier applied correctly per tier.
- [ ] Portal multiplier applied to FE days (1.0× single / 1.5× dual).
- [ ] 20% buffer applied to grand total.
- [ ] All four sections (A–D) present and in order.
- [ ] Portal configuration stated in Executive Summary.
- [ ] Service scope stated in Executive Summary (requirements & UI/UX included).
- [ ] Mandatory modules (User & Role Management, CRUD Content) present.
- [ ] Mandatory module costs within expected ranges.
- [ ] Day values in 0.25-day increments; costs in whole RM.
- [ ] Capacity warning included if FE days > BE days.

### Step 10 — Save Output to File

After passing self-check, save the quotation to the workspace `quotes/` folder:

**File naming convention:**
```
quotes/[QUOTE-REF]-[Client-Name-Kebab].md
```

**Examples:**
```
quotes/ATS-2026-001-SF-Global-Express.md
quotes/ECOM-2026-002-Acme-Corp.md
quotes/CRM-2026-003-Contoso-Ltd.md
```

**Rules:**
- `[QUOTE-REF]` = project type abbreviation + year + 3-digit sequential number (e.g., `ATS-2026-001`).
- `[Client-Name-Kebab]` = client/company name in kebab-case.
- The file MUST be saved inside the `quotes/` folder at the workspace root.
- Add a footer line to every saved file:
  `*Generated by /pricing_skill on [date] | Constitution v[X.Y.Z] | Rates: BE=RM360, FE=RM300, PM/QA=RM200*`
- If the `quotes/` folder does not exist, create it.

---

## Reverse Estimation

### Step R1 — Load the Constitution

Read the pricing constitution to get the current rates, formulas, and reverse estimation rules:

- [modEst_constitution.md](./references/modEst_constitution.md)

If the constitution file is missing or rates have changed, **STOP** and inform the user before proceeding.

### Step R2 — Back-Calculate Development Budget

Strip the 20% contingency buffer from the target budget:

```
Development Budget (B_dev) = Target Budget / 1.20
```

Example: RM 20,000 target → B_dev = RM 16,667.

### Step R3 — Determine Portal Configuration

Based on the project description, determine the portal configuration:

- **Single Portal (1.0×):** Only one user-facing frontend.
- **Dual Portal (1.5×):** User-facing portal + backoffice/admin portal.

### Step R3b — Confirm Service Scope

Per Principle XI, confirm and state in the Executive Summary that:

- **Requirements discussion** with the client is conducted by the team.
- **UI/UX design** (wireframes, mockups) is provided by the team.

Do NOT list "client provides design mockups" as an assumption.

### Step R4 — Generate Candidate Modules

Based on the project description (however vague), generate a **prioritized** list of all essential modules. For each module, assign:

- A clear, descriptive name.
- A business priority rank (1 = most critical, highest number = nice-to-have).
- A single complexity tier: **Simple** (1.0×), **Medium** (1.5×), or **Hard** (2.0×).

**Critical rule:** Core business modules (payments, auth, SKU management) MUST receive their honest complexity tier. Do NOT downgrade tiers to fit the budget.

**Mandatory modules (MUST be included as P1):**
1. **User & Role Management** — Minimum Medium (1.5×).
2. **CRUD Content Management** — Minimum Medium (1.5×).

### Step R5 — Estimate Days per Module

For each candidate module, estimate independently:

| Field | Rule |
| :--- | :--- |
| **BE Days** | Backend effort in 0.25-day increments |
| **FE Days** | Frontend effort in 0.25-day increments |
| **PM/QA Days** | `0.15 × (BE Days + FE Days × Portal Multiplier)`, rounded to nearest 0.25 |

### Step R6 — Apply Complexity & Portal Multipliers

```
Adjusted BE Days = Raw BE Days × Complexity Multiplier
Adjusted FE Days = Raw FE Days × Complexity Multiplier × Portal Multiplier
Adjusted PM/QA Days = Raw PM/QA Days × Complexity Multiplier
```

### Step R7 — Calculate Per-Module Cost

```
Module Cost = (Adjusted BE Days × 360) + (Adjusted FE Days × 300) + (Adjusted PM/QA Days × 200)
```

### Step R8 — Iterative Budget Fit

1. Sort modules by business priority (highest first).
2. Mandatory modules (User & Role Management, CRUD Content) MUST always be included — they cannot be deferred.
3. Accumulate costs top-down.
4. When the running total exceeds `B_dev`, mark remaining modules as **Deferred / Out-of-Scope**.
5. Never silently drop modules — all candidates must appear in the table.

### Step R9 — Generate Output

Produce the quotation in **exactly** this structure (all five sections, do not omit or reorder):

#### A. Executive Summary

- **Quote Date:** [today's date]
- **Validity:** 30 calendar days
- **Portal Configuration:** [Single Portal / Dual Portal (User + BO)]
- **Target Budget:** RM [target budget]
- **Pre-Buffer Development Budget:** RM [B_dev]
- **Budget Utilization:** [percentage of B_dev consumed by included modules]%
- **Estimated Project Duration:** [Total adjusted days of included modules] Days
- **Total Estimated Price:** RM [Sum of included modules × 1.20]
- **Infrastructure Constraints:** *This quote does not include monthly cloud hosting (AWS/GCP/Azure), domain registration, paid third-party API subscriptions, or ongoing maintenance beyond the quoted scope.*
- **Included Services:** *Requirements discussion and gathering with the client, and all UI/UX design (wireframes, mockups) are included in the quoted scope.*

#### B. Module Breakdown

| Module Name | Priority | Complexity | BE Days | FE Days | PM/QA Days | Subtotal Cost | Status |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| *included modules* | | | | | | | ✅ Included |
| ~~*deferred modules*~~ | | | | | | ~~RM X~~ | ⛔ Deferred |

#### C. Resource Capacity Note

> *Reminder for internal planning:* Ensure frontend workload is balanced — the team operates with heavier backend capacity. Modules with heavy UI/UX requirements may become the schedule bottleneck.

If total FE days > total BE days, add the capacity warning.

#### D. Next Steps for Client

A brief, professional closing sentence inviting the client to approve the quote so development can begin. Mention that deferred modules can be quoted separately as Phase 2.

#### E. Missing Technical Clarifications

A numbered list of specific questions whose answers are required to convert this estimate into a fixed-price contract. Each item MUST:

- Identify the module(s) affected.
- Describe the missing information.
- State the potential cost impact if the answer changes scope.

### Step R10 — Self-Check

Before delivering, verify:

- [ ] All rates match the constitution (BE=360, FE=300, PM/QA=200).
- [ ] PM/QA days = 15% of (BE + FE × Portal Multiplier) per module.
- [ ] Complexity multiplier applied correctly per tier — no under-tiering.
- [ ] Portal multiplier applied to FE days (1.0× single / 1.5× dual).
- [ ] Portal configuration stated in Executive Summary.
- [ ] Service scope stated in Executive Summary (requirements & UI/UX included).
- [ ] Mandatory modules (User & Role Management, CRUD Content) present and not deferred.
- [ ] Mandatory module costs within expected ranges.
- [ ] B_dev = Target Budget / 1.20.
- [ ] Sum of included module costs ≤ B_dev.
- [ ] Grand total (included × 1.20) ≤ target budget.
- [ ] All five sections (A–E) present and in order.
- [ ] Deferred modules clearly marked, not silently dropped.
- [ ] Day values in 0.25-day increments; costs in whole RM.
- [ ] Capacity warning included if FE days > BE days.
- [ ] Section E present with actionable clarification questions.

### Step R11 — Save Output to File

Same rules as Step 10 (forward), but append `-REV` to the quote reference:

```
quotes/[QUOTE-REF]-REV-[Client-Name-Kebab].md
```

**Examples:**
```
quotes/ECOM-2026-001-REV-Acme-Corp.md
```

Footer line:
`*Generated by /pricing_skill (reverse) on [date] | Constitution v[X.Y.Z] | Rates: BE=RM360, FE=RM300, PM/QA=RM200 | Budget cap: RM [target]*`

---

## Billing Rates Quick Reference

| Role | Daily Rate |
| :--- | :--- |
| Backend Developer (BE) | RM 360 |
| Frontend Developer (FE) | RM 300 |
| Project Manager / QA (PM/QA) | RM 200 |

## Complexity Tiers Quick Reference

| Tier | Multiplier | Examples |
| :--- | :---: | :--- |
| Simple | 1.0× | Basic CRUD, standard UI |
| Medium | 1.5× | External APIs, complex state, standard auth |
| Hard | 2.0× | Custom algorithms, websockets, payments, advanced security |
