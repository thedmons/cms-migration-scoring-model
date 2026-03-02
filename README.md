# CMS Migration Scoring Model
### Enterprise FinTech Platform Migration — Page Prioritization Framework

---

## Overview

This repository contains the scoring model used to prioritize the migration sequence of 500+ web pages from a legacy monolithic CMS to a modern composable architecture.

Rather than migrating pages arbitrarily — or by whoever lobbied loudest — a data-driven composite scoring framework was built to objectively rank page groups across value, complexity, and momentum dimensions. The model was built collaboratively: product, UX, engineering, and analytics each contributed scores within their domain, and the output drove the official migration wave sequencing plan.

📄 **[Read the full methodology →](./cms-migration-scoring-model.md)**
📊 **[Download the scoring model →](./cms_migration_score.xlsx)**

---

## What This Demonstrates

**Quantitative prioritization under complexity** — With 500+ pages, 5 lines of business, and competing stakeholder priorities, "gut feel" sequencing would have produced a politically charged, inefficient migration order. This model replaced that process with a transparent, agreed-upon framework — and shows how I approach prioritization problems that can't be solved with a simple 2×2.

**Weighted composite scoring design** — The model scores pages across 8 dimensions grouped into 3 composite scores (Value, Complexity, Momentum), each with explicit weights reflecting strategic tradeoffs. Component Score (25%) outweighs SEO Score (5%) because reusable components accelerate the broader migration — not just the pages they appear on. The weighting choices are documented and defensible, not arbitrary.

**Intentional inversion: Complexity scoring** — Complexity uses an inverted scale (5 = least complex, 1 = most complex), so highly complex pages score lower and migrate later. This prevents the team from tackling the hardest pages first and stalling early momentum. It's a small design choice with significant sequencing implications.

**Cross-functional input as a process design problem** — Getting consistent 1–5 scores from product, UX, engineering, and analytics requires clear rubric definitions and a structured scoring exercise. The methodology documents how that was operationalized — ensuring scores were comparable across teams, not just collected independently.

**Transparency as a stakeholder management tool** — Publishing the scoring methodology replaced political lobbying with a shared framework. Teams could see exactly why their pages were sequenced where they were — and what would need to change for a page to move up in priority. This is prioritization as communication, not just calculation.

---

## Document Metadata

| | |
|---|---|
| **Product** | Enterprise CMS Platform Migration (500+ pages) |
| **Document Type** | Prioritization Scoring Model |
| **Status** | Completed |
| **Context** | FinTech — Legacy Monolithic CMS → Modern Composable Stack |

---

## Related Artifacts

| Artifact | Description |
|---|---|
| [PRD: Enterprise CMS Platform Migration](https://github.com/thedmons/prd-cms-platform-migration) | Full PRD for the migration initiative this model supported |
