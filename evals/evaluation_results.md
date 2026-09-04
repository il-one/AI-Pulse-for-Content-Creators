# AI Pulse Evaluation Results

## 1. Evaluation Overview

This document defines the requirements for AI Pulse evaluations across prompt,
model, and system iterations.

The purpose of the evaluation is to determine whether AI Pulse can reliably:

- Identify meaningful recent AI market updates.
- Exclude updates that do not meet the product's relevance or recency requirements.
- Accurately represent source material.
- Preserve source integrity and attribution.
- Categorize updates consistently.
- Assign appropriate market relevance.
- Produce concise, useful summaries.

Evaluation results are generated against the fixed golden dataset defined in
[`golden_dataset.json`](./golden_dataset.json) and scored using the criteria
defined in [`evaluation_rubric.md`](./evaluation_rubric.md).

> **Important:** Scores in this document should represent measured evaluation
> results only. Example or projected scores must not be presented as observed
> system performance.

---

## 2. Evaluation Configuration

| Field | Value |
|---|---|
| Golden dataset | [`golden_dataset.json`](./golden_dataset.json) |
| Evaluation rubric | [`evaluation_rubric.md`](./evaluation_rubric.md) |
| Dataset version | 1.0.0 |
| Model | Gemini 3.1 |
| Prompt / system version | TBD |
| Evaluation date | TBD |
| Number of test cases | 10 |
| Evaluator | IL |

### Evaluation Method

Each configuration is evaluated against the same golden dataset to allow
comparison across iterations.

For each test case, the evaluator assesses:

1. Factual Accuracy
2. Source Integrity
3. Recency
4. Market Relevance
5. Categorization
6. Summary Quality

Each dimension is scored using the five-point rubric defined in
[`evaluation_rubric.md`](./evaluation_rubric.md).

The weighted AI Quality Score is calculated using the rubric's defined weights.

---

## 3. Iteration Results

### 3.1 Iteration 0 — Cold-Start Baseline

**Objective**

Establish a baseline for AI Pulse using the initial cold-start prompt before
introducing additional evaluation controls or structured output requirements.

**Configuration**

Note the prompt instructions and details for the baseline, including 
- Prompt
- Requested time window
- Market segments
- Expected categories
- Evaluation status

Record the results for the criteria in the [`Evaluation Method`](https://github.com/il-one/AI-Pulse-for-Content-Creators/edit/main/evals/evaluation_results.md#1-evaluation-overview).

**Observed Behavior**

Document only behaviors observed during the actual evaluation.

**Example placeholders:**

- `[Observed issue]`
- `[Observed issue]`
- `[Observed strength]`

**Evaluation Decision**

Note the decision based on observed behavior.

---

### 3.2 Iteration 1 — Recency Controls & Refresh UX

**Objective**

Improve the update experience by making the refresh action easier to access
and allowing users to switch between 24-hour and 48-hour views.

**Product Intervention**

- Moved the Refresh control to a more prominent location.
- Added a 24-hour / 48-hour toggle.
- Preserved the 48-hour retrieval set while using the toggle as a filter.

**Evaluation Status**

Note status.

**Results Table Template**

| Dimension | Before | After | Change |
|---|---:|---:|---:|
| Factual Accuracy |  |  |  |
| Source Integrity |  |  |  |
| Recency |  |  |  |
| Market Relevance |  |  |  |
| Categorization |  |  |  |
| Summary Quality |  |  |  |
| **Overall AI Quality Score** |  |  |  |

**Product Interpretation**

The UI intervention should only be credited with an evaluation improvement
where the measured results demonstrate a corresponding change.

---

### 3.3 Iteration 2 — Relevance Scoring & Update Categorization

**Objective**

Improve the prioritization and scanability of AI market updates by adding
structured relevance scoring and standardized update categories.

**Product Intervention**

- Added a relevance score from 0–100.
- Added standardized categories:
  - Model
  - Feature
  - Funding
  - Viral
  - Other
- Defined relevance in terms of market significance rather than popularity alone.

**Evaluation Status**

Note status.

**Results Table Template**

| Dimension | Before | After | Change |
|---|---:|---:|---:|
| Factual Accuracy |  |  |  |
| Source Integrity |  |  |  |
| Recency |  |  |  |
| Market Relevance |  |  |  |
| Categorization |  |  |  |
| Summary Quality |  |  |  |
| **Overall AI Quality Score** |  |  |  |

**Product Interpretation**

The primary hypotheses for this iteration:

1. Structured categorization should improve classification consistency.
2. Explicit relevance scoring should improve prioritization of meaningful
   market developments.
3. Defining market relevance independently from popularity should reduce
   high-noise, low-impact updates.

These hypotheses must be validated through evaluation results rather than
assumed to be true.

---
