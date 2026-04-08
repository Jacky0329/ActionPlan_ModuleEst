<!--
  Sync Impact Report
  ===================================================================
  Version change: N/A (template) → 1.0.0
  Modified principles: N/A (initial population)
  Added sections:
    - Core Principles (7 principles)
    - Cost Parameters & Formulas
    - Output Standards & Workflow
    - Governance
  Removed sections: None
  Templates requiring updates:
    - .specify/templates/plan-template.md — ✅ no update needed
      (Constitution Check section is dynamic; gates derived at
      plan-time from this file)
    - .specify/templates/spec-template.md — ✅ no update needed
      (user stories and requirements remain generic)
    - .specify/templates/tasks-template.md — ✅ no update needed
      (task phases remain generic; estimation principles apply at
      runtime)
  Follow-up TODOs: None
  ===================================================================
-->

# Pricing & Estimation Calculator Constitution

## Core Principles

### I. Standardized Billing Rates (NON-NEGOTIABLE)

All quotations MUST use the following daily billing rates:

- **Backend Developer (BE):** RM 300 / day
- **Frontend Developer (FE):** RM 250 / day
- **Project Manager / QA (PM/QA):** RM 200 / day

Rates MUST NOT be altered per-quote. Any rate revision MUST follow
the amendment procedure in the Governance section below.

### II. Structured Estimation Logic

- **Daily Unit:** 1 day = 8 working hours.
- **Resource Split:** BE and FE days MUST be estimated separately
  for every module.
- **PM/QA Overhead:** PM/QA days MUST be calculated as **15%** of
  the combined (BE + FE) days for each module, rounded to the
  nearest 0.25 day.
- **Contingency & QA Buffer:** A flat **20%** buffer MUST be added
  to the total estimated development days (sum of all modules)
  to account for bug fixing, testing, and unforeseen complexity.

### III. Complexity-Driven Scaling

Every module MUST be assigned exactly one complexity tier. The
complexity multiplier is applied to the module's raw day totals
(BE + FE + PM/QA) **before** cost calculation:

| Tier | Criteria | Multiplier |
| :--- | :--- | :---: |
| Simple | Basic CRUD, standard UI components | 1.0× |
| Medium | External API integrations, complex state management, standard auth | 1.5× |
| Hard | Custom algorithms, real-time websockets, payment gateways, advanced security | 2.0× |

If a module spans multiple tiers, the **highest applicable** tier
MUST be used.

### IV. Consistent Output Format (NON-NEGOTIABLE)

Every quotation MUST include **all four** sections in the
following order:

1. **A. Executive Summary** — duration, total price,
   infrastructure exclusions.
2. **B. Module Breakdown** — table with Module Name, Complexity,
   BE Days, FE Days, PM/QA Days, Subtotal Cost.
3. **C. Resource Capacity Note** — internal planning reminder
   about FE/BE balance.
4. **D. Next Steps for Client** — professional closing inviting
   approval.

No section may be omitted or reordered.

### V. Transparency & Exclusions

Every quote MUST explicitly state the following exclusions:

- Monthly cloud hosting costs (AWS / GCP / Azure).
- Domain registration fees.
- Paid third-party API subscription fees.
- Ongoing maintenance and support beyond the quoted scope.

Any additional assumption (e.g., "client provides design mockups")
MUST be listed in the Executive Summary or as a separate
Assumptions section.

### VI. Rounding & Precision

- Day estimates MUST be expressed in increments of **0.25 days**
  (i.e., 2-hour blocks).
- Monetary amounts MUST be rounded to the nearest whole RM
  (no sen).
- The Module Calculation Formula is:
  `(BE Days × BE Rate) + (FE Days × FE Rate) + (PM/QA Days × PM/QA Rate)`
  where days are the **complexity-adjusted** values.

### VII. Quote Validity & Revision Control

- Every quotation MUST display a **Quote Date** and a
  **Validity Period** (default: 30 calendar days from quote
  date).
- Revised quotes MUST carry a revision number (e.g., Rev 2) and
  a change summary noting what differs from the prior version.
- Expired quotes MUST be re-estimated; rates and buffer
  percentages may have changed per Governance amendments.

## Cost Parameters & Formulas

**Per-Module Cost (before buffer):**

$$
C_m = \bigl(D_{BE} \times 300\bigr)
    + \bigl(D_{FE} \times 250\bigr)
    + \bigl(D_{PM} \times 200\bigr)
$$

where each $D$ is the **complexity-adjusted** day count:

$$
D_{role}^{adj} = D_{role}^{raw} \times M_{complexity}
$$

and PM/QA raw days:

$$
D_{PM}^{raw} = 0.15 \times (D_{BE}^{raw} + D_{FE}^{raw})
$$

**Grand Total:**

$$
\text{Total} = \Bigl(\sum C_m\Bigr) \times 1.20
$$

(the 1.20 factor represents the 20% contingency buffer applied
to cost, not just days).

## Output Standards & Workflow

### Quotation Workflow

1. **Receive** project description from client or internal team.
2. **Decompose** into discrete modules (each with a clear scope).
3. **Classify** each module's complexity tier per Principle III.
4. **Estimate** BE and FE days independently; derive PM/QA days.
5. **Apply** complexity multiplier and calculate per-module cost.
6. **Sum** all modules; apply 20% contingency buffer.
7. **Generate** the four-section output per Principle IV.
8. **Review** internally for accuracy before delivery.

### Module Breakdown Table Format

| Module Name | Complexity | BE Days | FE Days | PM/QA Days | Subtotal Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| *e.g., User Auth* | Medium (1.5×) | 3 | 2.25 | 0.75 | RM 1,575 |
| *e.g., Dashboard* | Simple (1.0×) | 1 | 2 | 0.5 | RM 900 |

### Resource Capacity Note (template)

> *Reminder for internal planning:* Ensure frontend workload is
> balanced — the team operates with heavier backend capacity.
> Modules with heavy UI/UX requirements may become the schedule
> bottleneck.

## Governance

- This constitution supersedes all ad-hoc estimation practices.
- **Rate Changes:** Any billing rate adjustment MUST be proposed
  in writing, approved by the project lead, and documented as a
  MAJOR version amendment.
- **Formula Changes:** Modifications to buffer percentages,
  PM/QA overhead ratio, or complexity multipliers MUST be
  documented as a MINOR version amendment with before/after
  values.
- **Clarifications:** Wording, formatting, or non-semantic edits
  are PATCH amendments.
- **Compliance Review:** Every generated quotation MUST be
  checked against this constitution before client delivery. Any
  deviation MUST be justified and documented.
- **Amendment Procedure:** Propose change → review impact on
  open/active quotes → approve → update constitution version →
  update dependent templates if affected.

**Version**: 1.0.0 | **Ratified**: 2026-03-30 | **Last Amended**: 2026-03-30
