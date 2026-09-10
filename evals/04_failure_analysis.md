# AI Pulse Failure Analysis

## 1. Purpose

This document records and analyzes meaningful failures identified during AI Pulse
evaluation cycles.

The purpose of failure analysis is not simply to document incorrect outputs. It
is to determine **why** a failure occurred, assess its product impact, and identify
whether the appropriate intervention belongs in the prompt, evaluation design,
data, model configuration, or product experience.

Failure analysis provides the bridge between evaluation results and subsequent
product decisions.

**Evaluation results answer:**

> **What happened?**

**Failure analysis answers:**

> **Why did it happen, why does it matter, and what should we change?**

Detailed evaluation scores and iteration-level comparisons are maintained in
[`evaluation_results.md`](evals/03_evaluation_results.md).

The underlying test cases are maintained in
[`golden_dataset.json`](evals/01_golden_dataset.json), and scoring criteria are defined
in [`evaluation_rubric.md`](evals/02_evaluation_rubric.md).

---

## 2. Failure Analysis Method

Each significant failure should be analyzed using the following sequence:

```text
Observed Behavior
       ↓
Expected Behavior
       ↓
Evidence
       ↓
Failure Classification
       ↓
Root Cause Hypothesis
       ↓
Product Impact
       ↓
Intervention
       ↓
Re-evaluation
       ↓
Residual Risk
```
The analysis should distinguish between an observed failure and a
hypothesized root cause.

A failure can be directly observed from an evaluation output. Its underlying
cause may require additional testing.

Therefore:

- Observed Behavior should describe what actually happened.
- Evidence should identify the test case, source material, or evaluation
result supporting the finding.
- Root Cause Hypothesis should identify the proposed explanation and should
not be presented as proven without supporting evidence.
- Intervention should describe the change made in response.
- Result should only contain measured evidence from a subsequent evaluation.

---

## 3. Failure Taxonomy

Failures should be classified according to the primary capability that broke.

### 3.1 Factual Accuracy Failures

The output contains incorrect, distorted, incomplete, or unsupported factual
claims relative to the available source evidence.

Examples include:

- Claiming a feature exists when the source does not state this.
- Misstating what a newly released model can do.
- Adding unsupported product capabilities.
- Turning speculation into a factual statement.
