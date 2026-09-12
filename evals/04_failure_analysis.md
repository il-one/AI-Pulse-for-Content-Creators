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

### 3.2 Source Integrity Failures

The output incorrectly represents the authority, confidence, or relationship
between an output claim and its source.

Examples include:

- Presenting secondary reporting as an official announcement.
- Treating an unconfirmed report as a confirmed product release.
- Failing to prefer an official source when one is available.
- Citing a source that does not actually support the associated claim.

### 3.3 Recency Failures

The system incorrectly handles the requested time window.

Examples include:

- Surfacing an announcement outside the requested window.
- Treating the date of secondary coverage as the date of the underlying event.
- Omitting a qualifying recent update because of timestamp interpretation.
- Presenting stale information as a current update.

### 3.4 Market Relevance Failures

The system incorrectly estimates the significance of an update to the target AI
market.

Examples include:

- Assigning a high relevance score to an announcement with little practical
market impact.
- Overweighting publicity or popularity.
- Underestimating a less-publicized update with significant product or
competitive implications.
- Confusing broad AI interest with meaningful market significance.

### 3.5 Categorization Failures

The system assigns an incorrect primary category.

AI Pulse uses five categories:

Model
Feature
Funding
Viral
Other

Examples include:

- Classifying a model release as Feature.
- Using Other when the evidence supports a more specific category.

### 3.6 Summary Quality Failures

The system identifies the correct update but communicates it poorly.

Examples include:

- Excessive verbosity.
- Missing the primary development.
- Failing to communicate meaningful market implications.
- Including unnecessary background information.
- Producing a summary that is technically accurate but difficult to scan.

## 4. Failure Severity

Not every failure has the same product impact.

### Critical

A failure that materially undermines trust or causes the product to communicate false information.

**Examples:**

- Fabricated claims.
- Material factual contradictions.
- False representation of unconfirmed information as official.
- Systematic source or citation failures.

### High

A failure that can meaningfully distort the user's understanding of the AI market or significantly degrade feed quality.

**Examples:**

- Repeated high relevance scores for low-impact updates.
- Systematic inclusion of stale information.
- Major category misclassification across a recurring scenario.

### Medium

A noticeable quality issue that reduces usefulness but does not materially misrepresent the underlying information.

**Examples:**

- Moderate relevance-score errors.
- Minor category ambiguity.
- Incomplete but generally accurate summaries.

### Low

A minor presentation or interpretation issue with limited product impact.

**Examples:**

- Slightly verbose summaries.
- Minor wording imprecision that does not change meaning.
- Non-material formatting inconsistencies.
