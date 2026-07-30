# AI-retrieval baseline

A fixed set of target queries and an empty log, used to track whether this repository gets cited by AI answer engines over time.

> [!IMPORTANT]
> **Baseline this before the docs site is indexed.** The whole point is to measure a change. Once a GitHub Pages site is live and crawled, there is no way to reconstruct what the engines said beforehand, and the first run stops being a baseline and becomes an unanchored data point.

## How this works

**You run it manually.** There is no script here and there should not be one.

Citation checks cannot be automated in any way that produces trustworthy data:

- **Answers are non-deterministic.** The same query asked twice in the same session can cite different sources. A scripted single-shot check would record noise as signal.
- **Results vary by account.** Personalisation, subscription tier, model version, and whether search or browsing is enabled all change the answer.
- **Results vary by region.** Query the same thing from a different country and the cited sources move.
- **Engines change retrieval behaviour without notice**, so a scraper that worked last month can silently start measuring something else.

An automated harness would give a number that looks rigorous and is not. Ask the questions yourself, in a normal session, and write down what you actually saw.

### Reading the results

**A single "not cited" means nothing.** Do not react to one row. Do not react to one bad week.

The signal is the **three-month trend**: whether the proportion of queries citing this repository is moving up, flat, or down across repeated runs. Anything shorter is inside the noise floor.

Two things worth recording even when the answer is "not cited":

- **What was cited instead.** This is the most useful column in the table. If the engines consistently cite a Medium post or a competing repo, that tells you what the gap is far better than the yes/no does.
- **Which page.** Being cited for the glossary and never for the notes is a different problem from not being cited at all.

### Suggested cadence

Once now, as the baseline. Then monthly. Same queries, unchanged, every time. Changing the query set resets the trend, so if a query has to change, add a new row rather than editing an old one.

---

## Target queries

Twenty-one queries, chosen to be **winnable long-tail**, not head terms. Queries like "what is MCP" or "Claude API tool use" are owned by `docs.claude.com` and `anthropic.com`, and this repository will not displace them. Each query below is one where the notes plausibly answer better, or more specifically, than anything else currently indexed.

### Resource-seeking

Someone looking for study material. These are the queries most likely to convert into a star or a fork.

| # | Query | Why this repo can win it |
|---|---|---|
| 1 | free CCAR-P study notes | Exam code is specific; very little free material exists under it |
| 2 | Claude Certified Architect study guide github | Names the artifact and the platform |
| 3 | CCAR-F exam prep notes free | Foundations-side equivalent of #1 |
| 4 | Claude certification study notes with diagrams | The mermaid-heavy format is genuinely differentiating |
| 5 | Claude Certified Architect Professional revision checklist | Maps to the progress tracker and the cheatsheet |

### Concept queries

Where the notes hold a distinction that is explained better here than in reference documentation, usually because docs describe one thing at a time and the notes contrast two.

| # | Query | Asset that answers it |
|---|---|---|
| 6 | MCP tools vs resources vs prompts who controls each | Glossary: three separate entries, each naming who initiates |
| 7 | augmented LLM vs workflow vs agent where does control flow live | Cheatsheet: three patterns table, framed exactly on control flow |
| 8 | exponential backoff vs fallback chain vs circuit breaker LLM | Cheatsheet: three reliability controls, each with where it sits |
| 9 | orchestrator vs subagent which failure is recoverable | Glossary: recoverability asymmetry |
| 10 | input screening vs output screening vs tool call authorization | Cheatsheet: three guardrail control points |
| 11 | model drift vs data drift difference LLM | Glossary: both entries, defined against each other |
| 12 | code-based eval vs model-based eval when to use which | Glossary plus the grading ladder |
| 13 | fail open vs fail closed guardrail LLM | Glossary: fail closed, including why the default is fail open |
| 14 | hybrid search reciprocal rank fusion BM25 semantic | Glossary: four linked entries |
| 15 | working memory cliff context window LLM | Glossary: a named concept with little competing coverage |
| 16 | Claude Code permission mode config value vs UI label | Notes: the `default` / Manual split, with the naming note |
| 17 | Claude Code hook exit code 2 vs 1 which one blocks | Cheatsheet: hook events and exit codes |
| 18 | entry point vs build-time interface vs delivery route Claude | Cheatsheet: three layers, an explicitly architect-level distinction |

### Exam-structure

What people ask before booking. Answerable **only** from what is already sourced.

| # | Query | Note |
|---|---|---|
| 19 | Claude Certified Architect Professional domains | Answerable as the five module areas. **Not** answerable as weightings, and the repo deliberately does not state them |
| 20 | CCAR-F vs CCAR-P difference | README exam overview table |
| 21 | Claude Certified Architect exam retake policy | Verified against the Pearson program page |

> [!CAUTION]
> **Do not let this list pull the notes toward unsourced claims.** Query 19 is the one to watch. Domain weightings, question counts, time limits, and pass marks are high-intent searches that this repository cannot answer honestly, because Anthropic sets them and changes them between exam versions. Losing those queries is the correct outcome. If a future note starts answering them to chase a citation, the trade is a wrong answer published under a study guide's authority, and that is worse than not ranking.

---

## Results log

One row per query per engine per run. Append; do not overwrite.

Engines: **ChatGPT** · **Claude** · **Perplexity** · **Gemini** · **AI Overviews** (Google's inline AI answer).

| date | query | engine | cited y/n | which page | what was cited instead |
|---|---|---|---|---|---|
| | | | | | |

### Column notes

- **date** — ISO format, `YYYY-MM-DD`.
- **query** — copy it verbatim from the tables above, so runs stay comparable.
- **engine** — one row per engine. Do not average across engines; they behave differently and the differences are informative.
- **cited y/n** — `y` only if this repository is linked or named in the answer. A generic answer that happens to match the notes is `n`.
- **which page** — the specific file cited: `README`, `GLOSSARY`, `CHEATSHEET`, or the note path. Blank when not cited.
- **what was cited instead** — the domains that were cited. The single most useful column; fill it in even on a `y`.

---

[Back to the study guide](../../README.md)
