---
description: Review a manuscript PDF as an academic peer reviewer
argument-hint: <manuscript.pdf> [--discipline <field>] [--focus <aspect>]
allowed-tools: ["Read", "Task"]
model: sonnet
---

# Review Manuscript

Perform a full academic peer review of the manuscript PDF provided.

**Arguments:** $ARGUMENTS

## Instructions

### 1. Parse Arguments

Extract from `$ARGUMENTS`:
- **PDF path** (required): the manuscript file to review
- **`--discipline <field>`** (optional): one of `economics`, `sociology`, `political science`, `psychology`, `history`, `methods`. If not provided, use default rubric.
- **`--focus <aspect>`** (optional): a specific aspect to emphasize (e.g., "methods", "theory", "contribution")

### 2. Read the Manuscript

Use the `Read` tool to read the PDF in chunks:
- Start with pages 1–20
- Assess whether the content is complete (does it cover abstract through conclusion/references?)
- If clearly incomplete, continue reading in 20-page chunks until the full manuscript is read
- Note page numbers and section headings as you read — these will be used for citations in the review

### 3. Launch the Reviewer Agent

Use the `Task` tool to launch the `manuscript-reviewer` agent. Pass it:
- The full text content you have read
- The discipline flag value (or "default" if none provided)
- The focus flag value (or "none" if not provided)
- All page/section references noted during reading

### 4. Present the Review

Output the structured review returned by the agent directly to the user.

## Usage Examples

```
/academic-review:review-ms paper.pdf
/academic-review:review-ms paper.pdf --discipline sociology
/academic-review:review-ms paper.pdf --discipline economics --focus identification-strategy
/academic-review:review-ms paper.pdf --focus contribution
```

## Supported Disciplines

- `economics` — emphasizes identification strategy, external validity, contribution framing
- `sociology` — emphasizes theoretical framing, reflexivity, generalizability
- `political science` — emphasizes causal inference, case selection, policy relevance
- `psychology` — emphasizes pre-registration, effect sizes, measurement validity
- `history` — emphasizes archival depth, source criticism, interpretive plausibility
- `methods` — emphasizes technical correctness, reproducibility, benchmarking
- *(default)* — argument clarity, evidence-claim alignment, methodological transparency, contribution
