---
description: Parse and itemize reviewer revision requests from a decision letter PDF
argument-hint: <reviewer-comments.pdf> [--journal <name>]
allowed-tools: ["Read", "Bash", "Task"]
model: sonnet
---

# Review Revision Requests

Parse, itemize, and assess the revision demands in a journal decision letter or reviewer comments PDF.

**Arguments:** $ARGUMENTS

## Instructions

### 1. Parse Arguments

Extract from `$ARGUMENTS`:
- **PDF path** (required): the reviewer comments or decision letter file
- **`--journal <name>`** (optional): the journal name, for context on typical editorial expectations

### 2. Read the PDF

First, ensure `pdftotext` is available. Use the `Bash` tool to check and install if needed:
```bash
which pdftotext || (brew install poppler 2>/dev/null || apt-get install -y poppler-utils 2>/dev/null)
```

Then extract the full text using the `Bash` tool:
```bash
pdftotext "/path/to/comments.pdf" -
```

- Note reviewer labels (Reviewer 1, Reviewer 2, Editor, etc.) as you read
- Note any structural markers (numbered concerns, section breaks) that will anchor the itemization

### 3. Launch the Analyzer Agent

Use the `Task` tool to launch the `revision-analyzer` agent. Pass it:
- The full text content you have read
- The journal name (or "unspecified" if not provided)
- Any structural notes on reviewer numbering and page references

### 4. Present the Analysis

Output the structured itemization returned by the agent.

After presenting the output, advise the user:

> **Tip:** Save this itemized output — you can supply the original comments PDF as the third argument to `/academic-review:review-response` to enable quotation integrity checking when you later verify your revision response memo.

## Usage Examples

```
/academic-review:review-revisions decision-letter.pdf
/academic-review:review-revisions reviewer-comments.pdf --journal "American Journal of Sociology"
```
