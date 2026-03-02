# CMS Migration Scoring Model
**Author:** Thomas Edmons, Platform and Digital Product Manager
**Context:** Enterprise CMS Platform Migration — FinTech (500+ pages)
**Last Updated:** February 2026

---

## Overview

This repository contains the scoring model used to prioritize the migration sequence of 500+ web pages from a legacy monolithic CMS to a modern composable architecture. Rather than migrating pages arbitrarily or purely by business request, a data-driven composite scoring framework was developed to objectively rank page groups across value, complexity, and momentum dimensions.

The model was built collaboratively — product partners, UX, engineering, and analytics each contributed scores within their domain of expertise. The output informed the official migration roadmap and wave sequencing plan.

---

## The Problem: How Do You Prioritize 500+ Pages?

Migrating a large-scale web platform is not just a technical exercise — it's a sequencing problem. With 500+ pages spanning 5 lines of business, competing stakeholder priorities, and finite engineering capacity, the team needed a principled framework to answer:

- Which pages should we migrate first to maximize business impact?
- Which pages carry the highest technical risk or complexity?
- Where can we build early momentum to demonstrate value and reduce organizational friction?

Ad hoc prioritization — driven by whoever was loudest in the room — would produce an inefficient, politically charged migration sequence. This model replaced that process with a transparent, data-backed methodology that all stakeholders could align to.

---

## Scoring Framework

Pages are scored across **8 individual dimensions**, grouped into **3 composite scores**, which roll up into a single **Migration Score**.

### Composite Score Groups

| Priority | Composite Score | Components | Weight |
|---|---|---|---|
| 1 | Overall Value Score | Traffic, Business, SEO | 40% |
| 2 | Overall Complexity Score | Complexity, Remediation | 25% |
| 3 | Overall Momentum Score | Tech Debt, Component, Lead-time | 35% |

### Individual Score Dimensions

| Priority | Qualifier | Description | Weight | Owner |
|---|---|---|---|---|
| 1 | Business Score | Intrinsic business value of the page | 20% | Product |
| 2 | Component Score | Degree to which components are commonly reused across the platform | 25% | Tech / Dev |
| 3 | Complexity Score | Page design and content complexity | 10% | UX |
| 4 | SEO Impact Score | Anticipated improvement to Web Core Vitals post-migration | 5% | SEO / Product |
| 5 | Remediation Score | Confidence in the remediation plan and estimated LOE | 5% | Tech / Dev |
| 6 | Tech Debt Score | Degree to which migration reduces existing tech debt | 10% | Tech / Dev |
| 7 | Traffic Score | Page view volume based on last 6 months of data | 15% | Analytics |
| 8 | Lead-time Score | External team dependency impact on migration timeline | 10% | Tech / Dev |

---

## Score Definitions

All dimensions use a **1–5 scale** (0 reserved for pages with no recorded traffic).

| Score | Label | Meaning |
|---|---|---|
| 5 | Highest | Migrate immediately — maximum business value, traffic, or momentum |
| 4 | High | Strong early-wave candidate |
| 3 | Medium | Mid-wave migration |
| 2 | Lower | Defer to later waves |
| 1 | Lowest | Migrate last — minimal value or high effort |
| 0 | No Traffic | No recorded traffic in 6 months — evaluate for deprecation |

### Traffic Score Detail

The Traffic Score is a **weighted composite of three sub-metrics** pulled from 6 months of analytics data:

| Sub-metric | Weight | Description |
|---|---|---|
| Visits | 50% | Total page visits — primary volume signal |
| Visitors | 30% | Unique visitors — reach signal |
| Pages | 20% | Number of pages in the group — breadth signal |

Traffic scores are calculated at both the **individual URL level** and the **page group level** (aggregated). The Pages tab in the workbook shows individual URL rows rolling up to group subtotals.

---

## Migration Score Formula

The Migration Score is a single weighted composite calculated as:

```
Migration Score =
  (Traffic Score    × 0.150) +
  (Business Score   × 0.200) +
  (SEO Score        × 0.050) +
  (Complexity Score × 0.167) +
  (Remediation Score× 0.083) +
  (Tech Debt Score  × 0.078) +
  (Component Score  × 0.194) +
  (Lead-time Score  × 0.078)
```

Individual weights are derived from each dimension's raw weight normalized within its composite group, then scaled by the group's overall weight:

- **Value group** (40% total): Traffic 15%, Business 20%, SEO 5%
- **Complexity group** (25% total): Complexity 16.7%, Remediation 8.3%
- **Momentum group** (35% total): Tech Debt 7.8%, Component 19.4%, Lead-time 7.8%

All weights sum to **100%**.

---

## Workbook Structure

The scoring model is delivered as an Excel workbook (`cms_migration_score.xlsx`) with the following tabs:

### `Tables`
Two reference lookup tables:
1. **Individual score qualifiers** — all 8 dimensions with weights, composite group assignment, rollup weights, and score anchors (1 and 5 definitions)
2. **Composite score rollup** — the three composite groups with their overall weights and component descriptions

### `Pages`
Individual URL-level data with traffic sub-scores. Each page group has:
- A **bold group subtotal row** showing aggregated visits, visitors, and page count with a composite Traffic Score
- **Child URL rows** showing individual page traffic contributing to the group total
- Three calculated traffic sub-score columns (Visits, Visitors, Pages) and a weighted composite Traffic Score per row

### `Page Type Scores`
The primary scoring matrix — one row per page type + line of business combination. Contains:
- All 8 individual scores (entered collaboratively by domain owners)
- Calculated Overall Value, Overall Complexity, and Overall Momentum scores
- Final Migration Score with conditional color formatting (red → yellow → green)

### `Example Score Calculation`
A walkthrough of a single page group's score calculation, showing each dimension's score, weight, and composite contribution — designed for stakeholder communication and model transparency.

---

## How It Was Used

### Cross-Functional Input Process
Scores were not assigned unilaterally. Each dimension was owned by the team with the most relevant expertise:

- **Product partners** scored Business value
- **UX** scored page Complexity
- **Tech / Dev** scored Remediation confidence, Tech Debt reduction, Component reuse, and Lead-time risk
- **Analytics** provided Traffic data, which was converted to scores algorithmically

A scoring exercise was distributed to each stakeholder group with clear rubric definitions to ensure consistent interpretation of the 1–5 scale across teams.

### Output: Migration Wave Sequencing
The composite Migration Score was used to sort page groups into migration waves. Higher scores migrated earlier — capturing maximum business value and momentum while deferring complex, low-value pages to later waves when the team had more platform maturity and tooling in place.

### Model Transparency
Publishing the scoring methodology to stakeholders served a secondary purpose: it replaced political lobbying for migration priority with a transparent, agreed-upon framework. Teams could see exactly why their pages were sequenced where they were — and what would need to change for a page to move up in priority.

---

## Key Design Decisions

**Why weighted composite scores rather than a simple average?**
Not all dimensions contribute equally to migration priority. Component Score (25%) carries more weight than SEO Score (5%) because commonly reused components accelerate platform build-out and benefit more pages downstream. The weighting reflects these strategic tradeoffs explicitly.

**Why analyze page groups rather than individual pages?**
At 500+ pages, scoring individual URLs would be impractical and introduce noise. Pages are grouped by type and line of business — natural units that share content structure, ownership, and migration complexity. Individual URL data rolls up to the group level for traffic scoring.

**Why include Complexity with an inverted scale?**
Complexity Score uses 5 = least complex, 1 = most complex — an intentional inversion. This means highly complex pages score lower and migrate later, when the platform and team are more mature. It avoids the trap of tackling the hardest pages first and stalling early momentum.

**Why separate Momentum as a composite group?**
Momentum scores (Tech Debt, Component reuse, Lead-time) measure how much a page group accelerates the migration itself — not just its business value. Migrating high-momentum pages early builds shared infrastructure, reduces tech debt, and shortens the critical path for subsequent waves.

---

## Files

| File | Description |
|---|---|
| `cms_migration_score.xlsx` | Full scoring model with all tabs, formulas, and data |
| `README.md` | This methodology document |

---

## Related Portfolio Projects

- [PRD: Enterprise CMS Platform Migration](https://github.com/thedmons/prd-cms-platform-migration) — Full product requirements document for the same migration initiative
- [System Design: CMS Platform Architecture](https://github.com/thedmons/system-design) *(coming soon)*
