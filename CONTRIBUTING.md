# Contributing

Corrections and additions are welcome. These notes get better when people who sat the exam, or who work with the platform daily, push back on what is written here.

Before you open a pull request, read the two hard rules. Everything else is style.

---

## The Two Hard Rules

### 1. No verbatim course material

Do not paste text, slides, transcripts, images, or diagrams from the Anthropic Partner Academy courses, or from any other paid or gated training material. Rephrase the concept in your own words, or cite [Anthropic's public documentation](https://docs.claude.com) instead.

### 2. No real exam questions

Do not contribute exam questions, answer options, or anything reconstructed from an exam you sat. This includes "I remember a question about X, so here it is." That breaks the exam agreement you signed, and it gets this repository taken down.

### Why the Exam Traps tables are different

Every note ends with an **Exam Traps** table, so it is worth being explicit about why that is allowed.

| | Exam Traps table | A real exam question |
|---|---|---|
| **Source** | Derived from the concept and from public documentation | Recalled from a sat exam |
| **Level** | Concept-level: a distinction that is easy to get backwards | Item-level: a specific stem with specific options |
| **Shape** | "Here are two things people confuse, and how to tell them apart" | "Which of the following four options..." |
| **Test** | Would still be useful if the exam did not exist | Only exists because the exam exists |

An Exam Traps row says *this distinction is subtle, here is how to keep it straight*. It never says *this appeared on the exam*. If a row you are writing only makes sense as a memory of an exam item, cut it.

> **The test:** For every table, diagram, and exam-trap row, ask "can I point to where this claim comes from?" If you cannot, cut it, or mark it explicitly as current-practice context.

---

## Note Conventions

These are observed from the existing notes. Match them and your PR will merge quickly.

### Visual-first

Prefer a visual over a paragraph. If something can be a diagram, table, or ASCII box, make it one. Text explains what the visual cannot.

Brevity comes from **layering**, never from deleting. Every concept gets a scan layer (the heading, the table row, the diagram node) and a depth layer (the prose, blockquote, and code below it). When material will not fit a table cell in about ten words, it moves down a layer into prose. It does not get cut.

> **Earn every diagram.** Does this need arrows, flow, or spatial grouping? If not, it is a table. Every diagram needs at least one directional arrow: a set of boxes joined by `~~~` is a table wearing a costume.

### The seven-part shape

Every note follows the same skeleton. There is a copy-paste version at [.github/NOTE_TEMPLATE.md](.github/NOTE_TEMPLATE.md).

| # | Part | What it does |
|---|---|---|
| 1 | **H1 title** | `# Topic: The Angle`. One H1 per file. |
| 2 | **Orientation** | One or two sentences placing this note after the previous one, with a relative link. Often closes on a `> **The framing:**` or `> **The goal:**` callout. |
| 3 | **Body sections** | H2 per concept. Each runs: concept in 1-2 sentences, then a visual, then the detail the visual cannot carry, then a callout. One concept per section. |
| 4 | **Scenario** | A `> [!CAUTION]` block. Bold the opening setup sentence, tell the failure story, close on a bold `**The lesson:**` line. |
| 5 | **Cost · Complexity · Risk** | A lavender `flowchart LR` rubric. About twelve words per cell: it is a memory hook, not an essay. |
| 6 | **Quick Revision** | Always the last H2. A summary mermaid flowchart, then a concept-to-one-line table. |
| 7 | **Exam Traps** | An H3 inside Quick Revision. Three columns: `If you see...`, `The trap`, `The right call`. Three to six rows, one short sentence per cell. |

### Callout vocabulary

Blockquotes open with a bold label. Stay inside the established set rather than inventing a new one:

| Label | Use for |
|---|---|
| `> **The key:**` | The one thing to take from the section |
| `> **The trap:**` | A tempting wrong turn |
| `> **The lesson:**` | Closes a `[!CAUTION]` scenario |
| `> **Rule of thumb:**` | A heuristic that holds most of the time |
| `> **Tip:**` | Practical advice |
| `> **Exam trap:**` | A mistake the exam is likely to test |
| `> **Testable distinction:**` | Two things that look alike and are not |

### Mermaid colour palette

Three fills only, and **every node carries `color:#000`** so text stays legible when GitHub renders the diagram in dark mode. This is not optional: without it, dark-mode readers get black-on-dark or white-on-light nodes.

| Role | Style |
|---|---|
| Concepts, properties, terms to learn | `fill:#fff3cd,stroke:#ffc107,color:#000` |
| Actions, mitigations, answers, endpoints | `fill:#d4edda,stroke:#28a745,color:#000` |
| Cost · Complexity · Risk blocks only | `fill:#e8eaf6,stroke:#5c6bc0,color:#000` |

Node text budget is three short lines, about twelve words. Bold labels with `<b>`, break lines with `<br/>`. A diagram and a table must never carry the same content at full length: the diagram is the map, the table is the detail.

### Voice

- Direct, second person. Short sentences. Declarative, not hedging.
- No emojis, no em dashes, no filler openings ("Let's dive in").
- No "In this section we will learn about". Just start teaching.
- Bold key terms at first mention.

### File naming and links

- `NN-Title-Case.md` with a numeric prefix, major words capitalised. Folders use the same shape: `NN-Section-Name/`.
- Cross-references use **relative links**, never bare "see the previous section": `the [four properties](01-How-Claude-Behaves.md)`. Link across levels with `../../Foundations/...`.
- A term is defined once in the repo and linked thereafter. Extending a definition is fine. Contradicting one is not.

### Marking fast-moving facts

The platform changes faster than these notes do. When a claim is true now but likely to drift, mark it rather than stating it flatly:

```markdown
> **Current practice note:** `stop_details` is available from Claude Opus 4.7 onward.
> Re-check the category list in the stop-reasons documentation rather than hardcoding it.
```

Use `> **Current practice note:**` for API surface, model names, and feature availability, and `> **Currency note:**` for anything about the platform's shape that could be reorganised. Always say where to re-check.

**Never write an unverifiable exam fact.** Question counts, time limits, passing scores, fees, and domain weightings are set by Anthropic and change between exam versions. Do not put a number in these notes. Write "check the current exam guide" and link the [official program page](https://www.pearsonvue.com/us/en/anthropic.html).

---

## Pull Request Process

1. Fork, then branch from `main`. Name it for the work: `fix/guardrails-fail-closed`, `add/prompt-caching-note`.
2. Keep the PR to one topic. A typo fix and a new note are two PRs.
3. Fill in [the PR template](.github/PULL_REQUEST_TEMPLATE.md). The checklist is the review.
4. For a factual correction, link the documentation page that supports it. "The docs say otherwise" without a link is hard to action.
5. If you are adding a note, say in the PR description which module it belongs to and update that module's README table in the same PR.

Not sure whether something is worth a PR? [Open an issue](../../issues/new/choose) or start a [discussion](../../discussions) first.

### Review checklist

A maintainer will check:

- [ ] No verbatim course material, no recalled exam questions
- [ ] Every claim traces to public documentation or to a concept already established in the repo
- [ ] No invented mapping: nothing is paired, ranked, or categorised in a way the source material does not
- [ ] No unverifiable exam facts (counts, timings, scores, fees, weightings)
- [ ] Seven-part shape intact, Quick Revision and Exam Traps present
- [ ] Mermaid parses, every node carries `color:#000`, every diagram has a directional arrow
- [ ] Diagram and table are not duplicating each other at full length
- [ ] Relative links resolve, headings anchor correctly
- [ ] Terminology matches the rest of the repo, or the difference is deliberate and flagged
- [ ] File named `NN-Title-Case.md`, module README updated to match

---

## Four Quick Ways to Help

You do not need to write a whole note.

| | What | Effort |
|---|---|---|
| **Fix a wrong claim** | Something contradicts the docs. Open a [content correction](../../issues/new/choose) with the doc link. | Minutes |
| **Flag a stale fact** | A model name, API field, or feature description has aged out. Open a [currency update](../../issues/new/choose). | Minutes |
| **Fill a thin topic** | A section is a stub or a module is missing a note. Open a [missing or thin topic](../../issues/new/choose) issue, or write it. | An hour up |
| **Add an Exam Traps row** | You found a distinction that catches people out. One row, three cells. | Minutes |

---

## Licensing

By contributing, you agree that your contribution is licensed under [CC BY-SA 4.0](LICENSE), the same licence that covers the rest of this repository. Short illustrative code snippets are exempt from the attribution and ShareAlike requirement, as set out in [NOTICE.md](NOTICE.md).
