# Academic Review Plugin

A full suite of academic peer-review tools that mirror the real revision lifecycle: initial peer review → parsing revision demands → verifying a revision response.

## Commands

### `/academic-review:review-ms <manuscript.pdf> [--discipline <field>] [--focus <aspect>]`

Performs a full academic peer review of a manuscript PDF.

**Discipline flags** (optional):
- `economics` — identification strategy, external validity, contribution framing
- `sociology` — theoretical framing, reflexivity, generalizability
- `political science` — causal inference, case selection, policy relevance
- `psychology` — pre-registration, effect sizes, measurement validity
- `history` — archival depth, source criticism, interpretive plausibility
- `methods` — technical correctness, reproducibility, benchmarking

**Output:** Summary → Significance → Theory → Methods → Literature → Writing → Decision Recommendation → Prioritized Action Items

---

### `/academic-review:review-revisions <reviewer-comments.pdf> [--journal <name>]`

Parses and itemizes all reviewer revision demands from a decision letter or reviewer comments PDF.

**Output:** Overview table → Per-reviewer itemization (with demandingness/reasonableness ratings) → Editor framing → Cross-reviewer contradictions → Strategic assessment → Must/Should/Can-push-back action list

---

### `/academic-review:review-response <response-memo.pdf> <revised-manuscript.pdf> [<original-comments.pdf>]`

Verifies a revision response memo against the revised manuscript and (optionally) the original reviewer comments.

Supplying the third argument (original comments PDF) activates quotation integrity checking.

**Output:** Coverage check → Per-response assessment blocks → Quotation integrity section → Pattern analysis → Summary scorecard → Overall assessment

---

## Workflow

```
1. /academic-review:review-ms paper.pdf [--discipline sociology]
   → Initial peer review report

2. /academic-review:review-revisions decision-letter.pdf
   → Itemized, prioritized revision demands

3. /academic-review:review-response response-memo.pdf revised-paper.pdf decision-letter.pdf
   → Line-by-line verification of responses against demands and revised text
```

Commands work independently; step 3 is most powerful when the original comments PDF is supplied as the third argument.

## PDF Handling

All commands read PDFs in 20-page chunks, continuing until the document is fully read before launching the analysis agent. Page and section references are noted during reading and cited in the output.
