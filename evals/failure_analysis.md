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
