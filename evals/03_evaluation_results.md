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
|:---|:---|
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
|:---|---|---|---|
| Factual Accuracy | 5 | 5 | 0 |
| Source Integrity | 3 | 3 | 0 |
| Recency | 5 | 5 | 0 |
| Market Relevance | N/A | N/A | N/A |
| Categorization | N/A | N/A | N/A |
| Summary Quality | 5 | 5 | 0 |
| **Overall AI Quality Score** | 4 | 4 | 0 |

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
|:---|---|---|---|
| Factual Accuracy | 5 | 5 | 0 |
| Source Integrity | 3 | 3 | 0 |
| Recency | 5 | 5 | 0 |
| Market Relevance | 4 | 4 | 0 |
| Categorization | 5 | 5 | 0 |
| Summary Quality | 5 | 5 | 0 |
| **Overall AI Quality Score** | 4 | 4 | 0 |

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

## 4. Cross-Iteration Comparison

This table provides the primary view of whether the system is improving
over time.

| Iteration | Factual Accuracy | Source Integrity | Recency | Market Relevance | Categorization | Summary Quality | Overall |
|:---|---:|---:|---:|---:|---:|---:|---:|
| Iteration 0 | 5 | 3 | 5 | N/A | N/A | 5 | 4 |
| Iteration 1 | 5 | 3 | 5 | 4 | 5 | 5 | 4 |
| Iteration 2 |  |  |  |  |  |  |  |
| Iteration 3 |  |  |  |  |  |  |  |

### Interpretation

Evaluation should focus on both:

- **Aggregate improvement:** whether overall AI Quality Score improves.
- **Dimension-level improvement:** whether the specific capability targeted by
  each intervention improves.

An increase in the overall score should not be treated as sufficient evidence
of improvement when a material trust-related failure becomes worse.

---

## 5. Failure Summary

Detailed failure analysis is maintained in
[`failure_analysis.md`](./failure_analysis.md).

| Failure Pattern | First Observed | Severity | Affected Dimension | Resolution |
|:---|:---|:---|:---|:---|
| Source hallucinations | 9/3/2026 | High | Source Integrity | Corrected fallback output.  |
| TBD | TBD | TBD | TBD | TBD |
| TBD | TBD | TBD | TBD | TBD |

### Critical Failure Types

Particular attention should be given to:

- Unsupported factual claims
- Misrepresented or weakly sourced information
- Stale updates incorrectly presented as recent
- Low-relevance updates receiving high relevance scores
- Incorrect category assignments
- Unsupported market-impact claims
- Duplicate representations of the same underlying update

A system should not be considered improved solely because its aggregate score
increased if critical failure modes remain unresolved.

---

## 6. Product Decision

### Current Status

**Assessing root cause of failing updates.**

### Decision Criteria

The evaluation should inform one of three outcomes:

**Advance**

The system demonstrates sufficient improvement against the evaluation criteria
and no unresolved critical failure prevents the next stage.

**Iterate**

The system shows meaningful progress but has recurring weaknesses that should
be addressed through another prompt, data, model, or product intervention.

**Reconsider**

The evaluation reveals fundamental limitations that require a material change
to the system or product approach.

### Decision Rationale

[Document the evidence supporting the decision.]

---
