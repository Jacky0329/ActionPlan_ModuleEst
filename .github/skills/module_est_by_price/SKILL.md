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

## Procedure — Mode Detection

Read the user's input and determine the estimation mode:

- **Forward mode:** User provides a project description/requirements with NO budget cap → go to **[Forward Estimation (Steps 1–9)](#forward-estimation)**.
- **Reverse mode:** User provides a **target budget** (with or without a project description) → go to **[Reverse Estimation (Steps R1–R10)](#reverse-estimation)**.

If both a description AND a budget are provided, use **Reverse mode**.

---

## Forward Estimation

### Step 1 — Load the Constitution

Read the pricing constitution to get the current rates, formulas, and output format:

- [modEst_constitution.md](./references/modEst_constitution.md)

If the constitution file is missing or rates have changed, **STOP** and inform the user before proceeding.

### Step 2 — Decompose into Modules

Read the user's project description and break it into discrete technical modules. Each module must have:

- A clear, descriptive name (e.g., "User Authentication", "Payment Gateway Integration").
- A single complexity tier: **Simple** (1.0×), **Medium** (1.5×), or **Hard** (2.0×).
- If a module spans multiple tiers, assign the **highest applicable** tier.

### Step 3 — Estimate Days per Module

For each module, estimate independently:

| Field | Rule |
| :--- | :--- |
| **BE Days** | Backend effort in 0.25-day increments |
| **FE Days** | Frontend effort in 0.25-day increments |
| **PM/QA Days** | `0.15 × (BE Days + FE Days)`, rounded to nearest 0.25 |

### Step 4 — Apply Complexity Multiplier

Multiply each role's raw days by the module's complexity multiplier:

```
Adjusted Days = Raw Days × Multiplier
```

### Step 5 — Calculate Per-Module Cost

```
Module Cost = (Adjusted BE Days × 300) + (Adjusted FE Days × 250) + (Adjusted PM/QA Days × 200)
```

### Step 6 — Calculate Grand Total

```
Grand Total = Sum of all Module Costs × 1.20   (20% contingency buffer)
```

### Step 7 — Generate Output

Produce the quotation in **exactly** this structure (do not omit or reorder sections):

#### A. Executive Summary

- **Quote Date:** [today's date]
- **Validity:** 30 calendar days
- **Estimated Project Duration:** [Total adjusted days including 20% buffer] Days
- **Total Estimated Price:** RM [Grand Total]
- **Infrastructure Constraints:** *This quote does not include monthly cloud hosting (AWS/GCP/Azure), domain registration, paid third-party API subscriptions, or ongoing maintenance beyond the quoted scope.*

#### B. Module Breakdown

| Module Name | Complexity | BE Days | FE Days | PM/QA Days | Subtotal Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |

#### C. Resource Capacity Note

> *Reminder for internal planning:* Ensure frontend workload is balanced — the team operates with heavier backend capacity. Modules with heavy UI/UX requirements may become the schedule bottleneck.

If total FE days > total BE days, add:

> ⚠️ **Capacity Warning:** This project's frontend workload (X days) exceeds backend (Y days). Given the team's ~3:1 BE-to-FE capacity ratio, frontend delivery is the likely bottleneck. Consider augmenting FE resources or phasing UI-heavy modules.

#### D. Next Steps for Client

A brief, professional closing sentence inviting the client to approve the quote so development can begin.

### Step 8 — Self-Check

Before delivering, verify:

- [ ] All rates match the constitution (BE=300, FE=250, PM/QA=200).
- [ ] PM/QA days = 15% of (BE + FE) per module.
- [ ] Complexity multiplier applied correctly per tier.
- [ ] 20% buffer applied to grand total.
- [ ] All four sections (A–D) present and in order.
- [ ] Day values in 0.25-day increments; costs in whole RM.
- [ ] Capacity warning included if FE days > BE days.

### Step 9 — Save Output to File

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
  `*Generated by /pricing_skill on [date] | Constitution v[X.Y.Z] | Rates: BE=RM300, FE=RM250, PM/QA=RM200*`
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

### Step R3 — Generate Candidate Modules

Based on the project description (however vague), generate a **prioritized** list of all essential modules. For each module, assign:

- A clear, descriptive name.
- A business priority rank (1 = most critical, highest number = nice-to-have).
- A single complexity tier: **Simple** (1.0×), **Medium** (1.5×), or **Hard** (2.0×).

**Critical rule:** Core business modules (payments, auth, SKU management) MUST receive their honest complexity tier. Do NOT downgrade tiers to fit the budget.

### Step R4 — Estimate Days per Module

For each candidate module, estimate independently:

| Field | Rule |
| :--- | :--- |
| **BE Days** | Backend effort in 0.25-day increments |
| **FE Days** | Frontend effort in 0.25-day increments |
| **PM/QA Days** | `0.15 × (BE Days + FE Days)`, rounded to nearest 0.25 |

### Step R5 — Apply Complexity Multiplier

```
Adjusted Days = Raw Days × Multiplier
```

### Step R6 — Calculate Per-Module Cost

```
Module Cost = (Adjusted BE Days × 300) + (Adjusted FE Days × 250) + (Adjusted PM/QA Days × 200)
```

### Step R7 — Iterative Budget Fit

1. Sort modules by business priority (highest first).
2. Accumulate costs top-down.
3. When the running total exceeds `B_dev`, mark remaining modules as **Deferred / Out-of-Scope**.
4. Never silently drop modules — all candidates must appear in the table.

### Step R8 — Generate Output

Produce the quotation in **exactly** this structure (all five sections, do not omit or reorder):

#### A. Executive Summary

- **Quote Date:** [today's date]
- **Validity:** 30 calendar days
- **Target Budget:** RM [target budget]
- **Pre-Buffer Development Budget:** RM [B_dev]
- **Budget Utilization:** [percentage of B_dev consumed by included modules]%
- **Estimated Project Duration:** [Total adjusted days of included modules] Days
- **Total Estimated Price:** RM [Sum of included modules × 1.20]
- **Infrastructure Constraints:** *This quote does not include monthly cloud hosting (AWS/GCP/Azure), domain registration, paid third-party API subscriptions, or ongoing maintenance beyond the quoted scope.*

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

### Step R9 — Self-Check

Before delivering, verify:

- [ ] All rates match the constitution (BE=300, FE=250, PM/QA=200).
- [ ] PM/QA days = 15% of (BE + FE) per module.
- [ ] Complexity multiplier applied correctly per tier — no under-tiering.
- [ ] B_dev = Target Budget / 1.20.
- [ ] Sum of included module costs ≤ B_dev.
- [ ] Grand total (included × 1.20) ≤ target budget.
- [ ] All five sections (A–E) present and in order.
- [ ] Deferred modules clearly marked, not silently dropped.
- [ ] Day values in 0.25-day increments; costs in whole RM.
- [ ] Capacity warning included if FE days > BE days.
- [ ] Section E present with actionable clarification questions.

### Step R10 — Save Output to File

Same rules as Step 9 (forward), but append `-REV` to the quote reference:

```
quotes/[QUOTE-REF]-REV-[Client-Name-Kebab].md
```

**Examples:**
```
quotes/ECOM-2026-001-REV-Acme-Corp.md
```

Footer line:
`*Generated by /pricing_skill (reverse) on [date] | Constitution v[X.Y.Z] | Rates: BE=RM300, FE=RM250, PM/QA=RM200 | Budget cap: RM [target]*`

---

## Billing Rates Quick Reference

| Role | Daily Rate |
| :--- | :--- |
| Backend Developer (BE) | RM 300 |
| Frontend Developer (FE) | RM 250 |
| Project Manager / QA (PM/QA) | RM 200 |

## Complexity Tiers Quick Reference

| Tier | Multiplier | Examples |
| :--- | :---: | :--- |
| Simple | 1.0× | Basic CRUD, standard UI |
| Medium | 1.5× | External APIs, complex state, standard auth |
| Hard | 2.0× | Custom algorithms, websockets, payments, advanced security |
