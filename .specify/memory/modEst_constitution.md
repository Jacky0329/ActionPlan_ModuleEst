<!--
  Sync Impact Report
  ===================================================================
  Version change: 1.0.0 → 1.1.0 (MINOR — new principle added)
  Modified principles:
    - None renamed or removed
  Added sections:
    - Principle VIII — Reverse Estimation (Budget-to-Scope)
    - Cost Parameters: Reverse Estimation Formulas subsection
    - Output Standards: Reverse Estimation Workflow subsection
    - Output Standards: Reverse Quotation Output Format (Sections
      A–E) subsection
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
    - pricing_skill/SKILL.md — ✅ updated
      (Forward + reverse estimation procedures added)
    - pricing_skill/references/modEst_constitution.md — ✅ synced
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

### VIII. Reverse Estimation — Budget-to-Scope (NON-NEGOTIABLE)

When the user supplies a **target budget** instead of (or in
addition to) a project description, the estimator MUST work
**backwards** from the budget cap to determine feasible scope.

**Rules:**

1. **Budget Back-Calculation:** Strip the 20% contingency buffer
   first to derive the pre-buffer development budget:
   $$
   B_{dev} = \frac{B_{total}}{1.20}
   $$
2. **Scope Generation:** Using the project description (however
   vague), generate a prioritized list of essential modules that
   fit within $B_{dev}$.
3. **Complexity Prioritization:** Core business-critical modules
   (e.g., payments, SKU management, auth) MUST be assigned the
   correct complexity tier (Medium or Hard) even if that reduces
   the number of modules that fit. Do NOT under-tier a module to
   squeeze it into budget.
4. **Iterative Fit:** After estimating all candidate modules,
   if the sum exceeds $B_{dev}$, the estimator MUST:
   - Remove or defer lowest-priority modules first.
   - Clearly mark deferred modules in a "Deferred / Out-of-Scope"
     row at the bottom of the Module Breakdown table.
   - Never silently drop modules.
5. **Gap Analysis (MANDATORY for vague inputs):** When the project
   description lacks technical specifics, the output MUST include
   a **Section E — Missing Technical Clarifications** listing
   exactly what information is needed to move from an estimate to
   a fixed-price contract.
6. **All other principles still apply.** Rates (Principle I),
   PM/QA overhead (Principle II), complexity multipliers
   (Principle III), output format (Principle IV with Section E
   appended), exclusions (Principle V), rounding (Principle VI),
   and validity (Principle VII) MUST be followed identically.

## Cost Parameters & Formulas

### Forward Estimation (Description → Cost)

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

### Reverse Estimation (Budget → Scope)

**Step 1 — Derive development budget:**

$$
B_{dev} = \frac{B_{total}}{1.20}
$$

**Step 2 — Weighted average daily rate:**

For a module with $D_{BE}^{adj}$ BE days, $D_{FE}^{adj}$ FE days,
and $D_{PM}^{adj}$ PM/QA days, the blended cost is:

$$
C_m = (D_{BE}^{adj} \times 300)
    + (D_{FE}^{adj} \times 250)
    + (D_{PM}^{adj} \times 200)
$$

**Step 3 — Iterative budget allocation:**

1. List all candidate modules from the project description.
2. Assign complexity tiers honestly per Principle III.
3. Estimate raw days (BE, FE) per module; derive PM/QA days.
4. Calculate each module's cost.
5. Sort modules by business priority (highest first).
6. Accumulate costs top-down until $B_{dev}$ is exhausted.
7. Modules that exceed the remaining budget are marked
   **Deferred**.

**Step 4 — Validation:**

$$
\Bigl(\sum C_{m}^{included}\Bigr) \leq B_{dev}
$$

$$
\Bigl(\sum C_{m}^{included}\Bigr) \times 1.20 \leq B_{total}
$$

## Output Standards & Workflow

### Forward Quotation Workflow

1. **Receive** project description from client or internal team.
2. **Decompose** into discrete modules (each with a clear scope).
3. **Classify** each module's complexity tier per Principle III.
4. **Estimate** BE and FE days independently; derive PM/QA days.
5. **Apply** complexity multiplier and calculate per-module cost.
6. **Sum** all modules; apply 20% contingency buffer.
7. **Generate** the four-section output per Principle IV.
8. **Review** internally for accuracy before delivery.

### Reverse Estimation Workflow

1. **Receive** target budget and project description (may be
   vague).
2. **Back-calculate** development budget:
   $B_{dev} = B_{total} / 1.20$.
3. **Generate** candidate modules based on the project domain.
4. **Classify** each module's complexity per Principle III —
   do NOT under-tier to fit budget.
5. **Estimate** raw BE and FE days per module; derive PM/QA.
6. **Apply** complexity multipliers; calculate per-module cost.
7. **Rank** modules by business priority (core features first).
8. **Accumulate** costs top-down; mark modules that exceed
   $B_{dev}$ as **Deferred**.
9. **Generate** output with Sections A–D per Principle IV,
   plus **Section E — Missing Technical Clarifications**
   (mandatory when input is vague).
10. **Review** internally for accuracy before delivery.

### Module Breakdown Table Format

| Module Name | Complexity | BE Days | FE Days | PM/QA Days | Subtotal Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| *e.g., User Auth* | Medium (1.5×) | 3 | 2.25 | 0.75 | RM 1,575 |
| *e.g., Dashboard* | Simple (1.0×) | 1 | 2 | 0.5 | RM 900 |

For reverse estimates, append deferred modules at the bottom:

| Module Name | Complexity | BE Days | FE Days | PM/QA Days | Subtotal Cost |
| :--- | :--- | :--- | :--- | :--- | :--- |
| ~~*Deferred Module*~~ | Medium (1.5×) | 2 | 1.5 | 0.5 | ~~RM 975~~ |

### Reverse Quotation Output Format

When performing a reverse estimate, the output MUST include
**all five** sections in this order:

1. **A. Executive Summary** — as per Principle IV, plus:
   - **Target Budget:** RM [budget]
   - **Pre-Buffer Development Budget:** RM [B_dev]
   - **Budget Utilization:** [percentage of B_dev consumed]
2. **B. Module Breakdown** — as per Principle IV, with deferred
   modules clearly marked at the bottom.
3. **C. Resource Capacity Note** — as per Principle IV.
4. **D. Next Steps for Client** — as per Principle IV.
5. **E. Missing Technical Clarifications** — a numbered list of
   specific questions whose answers are required to convert the
   estimate into a fixed-price contract. Each item MUST identify
   the module(s) affected and the decision's cost impact.

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
- **Principle Additions:** New estimation modes (e.g., reverse
  estimation) MUST be documented as a MINOR version amendment
  with full workflow and formula definitions.
- **Clarifications:** Wording, formatting, or non-semantic edits
  are PATCH amendments.
- **Compliance Review:** Every generated quotation MUST be
  checked against this constitution before client delivery. Any
  deviation MUST be justified and documented.
- **Amendment Procedure:** Propose change → review impact on
  open/active quotes → approve → update constitution version →
  update dependent templates if affected.

**Version**: 1.1.0 | **Ratified**: 2026-03-30 | **Last Amended**: 2026-04-08
