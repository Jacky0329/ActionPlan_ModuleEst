---
name: pricing_skill
description: "Expert technical project estimator. Use when: generating project quotations, estimating development costs, breaking down project modules, pricing software projects, calculating BE/FE/PM days, producing client-facing quotes. Follows strict billing rates, complexity multipliers, and output format from the pricing constitution."
argument-hint: "Paste or describe the project requirements to quote"
---

# Project Pricing & Estimation Skill

## When to Use

- A client or internal team provides a project description that needs a cost quotation.
- You need to break down a software project into modules with day estimates.
- You need a professional quotation document with Executive Summary, Module Breakdown, Resource Note, and Next Steps.

## Constraints (NON-NEGOTIABLE)

1. **Never guess prices.** Every number must be derived from the formulas in the [constitution](./references/prcing_constitution.md).
2. **Always output the exact markdown table** defined in the constitution (Section IV).
3. **Flag capacity warnings.** If calculated FE days exceed BE days for the project, add a warning that the project may bottleneck on frontend — the team's capacity is currently weighted ~3:1 toward backend and PM resources.

## Procedure

### Step 1 — Load the Constitution

Read the pricing constitution to get the current rates, formulas, and output format:

- [prcing_constitution.md](./references/prcing_constitution.md)

If the constitution file is missing or rates have changed, **STOP** and inform the user before proceeding.

> **Skill location note:** This skill lives at `.github/skills/pricing_skill/`.

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
