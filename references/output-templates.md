# Output Templates

Copy the shape, not the wording. Compress to **Answer → Findings → Sources** for D0/D1.
Inline citation markers `[cite:id]` go wherever the runtime returned citation ids.

## Template A — standard answer (D0/D1)

```markdown
## Answer
<one or two sentences: the direct answer plus its most important qualification.>

## Findings
- **[Documented]** <claim> — <source [S1], full text, clause/page>.
- **[Supported]** <claim> — independent of the above: <why they are independent>.
- **[Inferred]** <claim> — from <premise>, assuming <assumption>.
- **[Sentiment]** <attitude> — reported in <community/source>; sample and method: <...>.
- **[Unverified]** <claim> — <what was searched, what was not found>.

## Method and confidence note
<engines used; what was cross-checked; single-sourced items; effective research cutoff;
overall confidence and its main reason; any tool gap or fallback.>

## Sources
- **[S1] [Title](URL)** — publisher; date; access level; what it supports.
```

## Template B — consequential answer (D2/D3)

```markdown
## Answer
<direct answer, main qualification up front.>

## Findings

### Established evidence
- **[Documented]** ...

### Interpretation and inference
- **[Inferred]** ...

### Competing explanations and counterevidence
- Alternative explanation A — supported by <...>; predicts <...>.
- Counterevidence sought: <queries, sources checked>. Result: <found / none found>.

### Conflicts and uncertainty
| Source | Claim | Origin / method | Why they differ |
| --- | --- | --- | --- |
| [S1] | ... | ... | ... |

### Computations (when numbers are material)
`formula`; inputs: <...>, each with source and vintage; result: <...>; assumptions: <...>.

### Limitations, single-origin items, and research cutoff
- Single-origin material claim: <claim> — only <origin> supports it.
- Searched, not found: <expected evidence>.
- Cutoff: research current to <date>.

### What would change this conclusion
<one line per major claim.>

## Method and confidence note
<tier D2/D3; adversarial pass delegated or self-run; single-sourced claims; confidence + reason.>

## Sources
- **[S1] ...** ...
```

## Template C — layered or esoteric topic

Keep the layers separate; never let one layer borrow authority from another.

```markdown
## Answer
<direct answer.>

## Empirical layer
- **[Documented] / [Supported] / [Disputed]** ... (documents, measurements, official records)

## Interpretive layer
- **[Inferred]** ... — whose interpretation, on what reading of the sources.

## Traditional / symbolic layer
- **[Traditional]** ... — the tradition as it describes itself; scholarly study of it: <...>.
  Non-empirical; not evaluated by empirical test.

## Sentiment and community reports
- **[Sentiment]** ...

## Limitations and research cutoff
...

## Sources
- **[S1] ...** ...
```

## Good and bad lines

| Instead of | Write |
| --- | --- |
| "Studies show that X is true." | Two independent origins, named, with design and period; or "one study reports…" |
| "Experts agree." | Which experts, from which institutions, on what evidence; or "the sources consulted do not agree." |
| "It is widely reported that…" | Who first reported it, and whether later coverage adds evidence. |
| "Approximately 40% (estimated)." | The dataset, population, period, and uncertainty — or label it `[Reported]`. |
| "Verified." | What was read, at what access level, and what would falsify it. |
