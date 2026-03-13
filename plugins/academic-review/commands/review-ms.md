---
description: Review a manuscript PDF as an academic peer reviewer
argument-hint: <manuscript.pdf> [--discipline <field>] [--focus <aspect>]
allowed-tools: ["Read", "Bash", "Task"]
model: sonnet
---

# Review Manuscript

Perform a full academic peer review of the manuscript PDF provided.

**Arguments:** $ARGUMENTS

## Instructions

### 1. Parse Arguments

Extract from `$ARGUMENTS`:
- **PDF path** (required): the manuscript file to review
- **`--discipline <field>`** (optional): one of `economics`, `sociology`, `political science`.
- **`--focus <aspect>`** (optional): a specific aspect to emphasize (e.g., "methods", "theory", "contribution")

### 2. Read the Manuscript

First, ensure `pdftotext` is available. Use the `Bash` tool to check and install if needed:
```bash
which pdftotext || (brew install poppler 2>/dev/null || apt-get install -y poppler-utils 2>/dev/null)
```

Then extract the full manuscript text using the `Bash` tool:
```bash
pdftotext "/path/to/manuscript.pdf" -
```

- Extract the full text in one pass — `pdftotext` handles the entire document
- Note section headings and approximate page positions as you read — these will be used for citations in the review
- If the text appears truncated or garbled, the PDF may be image-based; note this for the agent

### 3. Launch the Reviewer Agent

Use the `Task` tool to launch the `manuscript-reviewer` agent. Pass it:
- The full text content you have read
- The discipline flag value (or none if not provided)
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

- `economics`
- `sociology`
- `political science`
