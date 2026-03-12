---
description: Verify a revision response memo against original reviewer requests and the revised manuscript
argument-hint: <response-memo.pdf> <revised-manuscript.pdf> [<original-comments.pdf>]
allowed-tools: ["Read", "Bash", "Task"]
model: sonnet
---

# Review Revision Response

Verify a revision response memo against the revised manuscript and (optionally) the original reviewer comments, checking for completeness, accuracy, and quotation integrity.

**Arguments:** $ARGUMENTS

## Instructions

### 1. Parse Arguments

Extract from `$ARGUMENTS` in order of appearance:
- **First `.pdf`** (required): the revision response memo
- **Second `.pdf`** (required): the revised manuscript
- **Third `.pdf`** (optional): the original reviewer comments / decision letter — enables quotation integrity checking

### 2. Read All PDFs in Sequence

First, ensure `pdftotext` is available. Use the `Bash` tool to check and install if needed:
```bash
which pdftotext || (brew install poppler 2>/dev/null || apt-get install -y poppler-utils 2>/dev/null)
```

Then extract each document in order using the `Bash` tool:

**Step 1 — Response memo:**
```bash
pdftotext "/path/to/memo.pdf" -
```
Note how many numbered items/responses it contains and any explicit references to the manuscript (page, section, line).

**Step 2 — Revised manuscript:**
```bash
pdftotext "/path/to/revised.pdf" -
```
Note section headings, page numbers, and any passages that appear newly added or substantially revised.

**Step 3 — Original comments (if provided):**
```bash
pdftotext "/path/to/comments.pdf" -
```
Note the exact wording of each reviewer concern — these will be checked against how they are quoted in the response memo.

### 3. Launch the Verifier Agent

Use the `Task` tool to launch the `response-verifier` agent. Pass it:
- Full text of all documents read
- Whether original comments were provided (enables quotation integrity mode)
- Structural notes: item count in memo, reviewer labeling in original comments, section map of revised manuscript

### 4. Present the Verification Report

Output the structured report returned by the agent directly to the user.

## Usage Examples

```
/academic-review:review-response response-memo.pdf revised-paper.pdf
/academic-review:review-response response-memo.pdf revised-paper.pdf original-decision-letter.pdf
```

## Notes

- The third argument (original comments) is optional but strongly recommended — it enables the quotation integrity check that catches misquotation, selective truncation, and reframing of reviewer concerns.
- All three PDFs are read fully before analysis begins, so the agent has the complete picture.
