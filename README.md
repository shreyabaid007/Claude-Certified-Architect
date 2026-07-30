<div align="center">
  <h1>Claude Certified Architect</h1>
  <p>
    Community study guide for the <strong>Claude Certified Architect</strong> certification exams
    <br />
    Foundations &bull; Professional
  </p>

  <p>
    <a href="LICENSE"><img src="https://img.shields.io/badge/license-CC--BY--SA--4.0-blue.svg" alt="License: CC BY-SA 4.0"></a>
    <a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-welcome-brightgreen.svg" alt="Pull requests welcome"></a>
    <a href="https://github.com/shreyabaid007/Claude-Certified-Architect/stargazers"><img src="https://img.shields.io/github/stars/shreyabaid007/Claude-Certified-Architect?style=social" alt="Repository stars"></a>
    <a href="https://github.com/shreyabaid007/Claude-Certified-Architect/network/members"><img src="https://img.shields.io/github/forks/shreyabaid007/Claude-Certified-Architect?style=social" alt="Repository forks"></a>
    <a href="https://github.com/shreyabaid007/Claude-Certified-Architect/commits/main"><img src="https://img.shields.io/github/last-commit/shreyabaid007/Claude-Certified-Architect" alt="Last commit"></a>
  </p>
</div>

---

Scannable, revision-friendly study notes with mermaid diagrams, comparison tables, exam traps, and quick-reference summaries.

> [!IMPORTANT]
> **Unofficial.** Independent community notes. Not affiliated with, endorsed by, or reviewed by Anthropic or Pearson. Contains no exam questions and no verbatim course material.
> **Verify as you read.** The platform moves fast — check specific claims against [Anthropic's documentation](https://docs.claude.com). If a note contradicts the docs, the docs win, and please [open an issue](../../issues/new/choose).

## Who Is This For?

- **Engineers and architects** sitting either exam, Foundations or Professional
- **Team leads** evaluating Claude for enterprise adoption who want a structured overview
- **Anyone** who learns better from concise notes than from video courses

## Exam Overview

| | Foundations | Professional |
|---|---|---|
| **Exam code** | CCAR-F | CCAR-P |
| **Focus** | API skills, prompt engineering, tool use, RAG, MCP, Claude Code | Solution architecture, enterprise integration, safety and risk, stakeholder engagement, team enablement |
| **Modules** | 4 | 5 |
| **Notes here** | 11 | 29 |
| **Official course** | [Claude Certified Architect – Foundations](https://anthropic-partners.skilljar.com/claude-certified-architect-foundations-certification) | [Claude Certified Architect – Professional](https://anthropic-partners.skilljar.com/claude-certified-architect-professional-certification) |

Certification is open to organisations in the **Claude Partner Network**, and counts toward partner program standing. Prep courses and the exam guides live in the [Anthropic Partner Academy](https://anthropic-partners.skilljar.com/page/partner-certifications). Scheduling runs through [Pearson VUE](https://www.pearsonvue.com/us/en/anthropic.html), either at a test centre or online with OnVUE proctoring; you register through the Partner Academy first and receive Pearson credentials by email. Retakes are gated at **14 days** after a first attempt, **30 days** after a second, and **90 days** after a third, with up to **4 attempts per exam in any rolling 12-month period**. Digital badges are issued through [Credly](https://www.credly.com).

> [!NOTE]
> **Exam format, domain weightings, and fees are set by Anthropic and change between exam versions.** Read them from the current official exam guide, not from any third-party summary, including this one. Nothing in this repository should be treated as a statement about how the exam is scored or structured.

## Study Guide

Two words describe module status, used the same way in every README here. **Complete** means every teaching topic in the module has a note. **In progress** means the teaching topics are covered but module exercise or wrap-up material is still outstanding, and the module README names what is missing.

### Foundations (complete)

| # | Module | Topics |
|---|--------|--------|
| 01 | [AI Fluency: Framework & Foundations](Foundations/01-AI-Fluency-Framework-and-Foundations/) | The 4 Ds (Delegation, Description, Discernment, Diligence), AI fluency framework |
| 02 | [Building with the Claude API](Foundations/02-Building-with-the-Claude-API/) | API access, prompt engineering, prompt evaluation, tool use, RAG, citations, code execution, MCP, agents & workflows |
| 03 | [Claude on Google Cloud](Foundations/03-Claude-on-Google-Cloud/) | Vertex AI Model Garden setup, enabling models |
| 04 | [Claude Code in Action](Foundations/04-Claude-Code-in-Action/) | CLI workflows, hooks, MCP servers, CLAUDE.md, practical patterns |

### Professional

| # | Module | Topics | Status |
|---|--------|--------|--------|
| 01 | [Claude Platform & Solution Design](Professional/01-Claude-Platform-and-Solution-Design/) | Four properties, platform primitives, delegation, patterns, multi-agent, reference architectures, RAG, model selection, prompt architecture, entry points, delivery routes | In progress |
| 02 | [Enterprise Integration & Production](Professional/02-Enterprise-Integration-and-Production/) | Evals, POC to production, sizing & feasibility, integration patterns, A/B testing & observability | In progress |
| 03 | [Responsible AI, Safety & Risk](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/) | Alignment, guardrails, fairness, review routing, compliance | Complete |
| 04 | [Stakeholder Engagement & GTM](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/) | Discovery, tradeoff framing, feedback loops, documentation, entry point & outcome documents | In progress |
| 05 | [Team Enablement & Ops](Professional/05-Team-Enablement-and-Operational-Productivity/) | Team setup, developer workflows, operational support | Complete |

Every Professional module has notes for every teaching topic. The three marked in progress have module-level exercise or wrap-up material outstanding, named in [the level README](Professional/README.md).

## Progress Tracker

Fork this repo and check off topics as you study. This is your personal checklist.

### Foundations

- [ ] AI Fluency: the 4 Ds framework
- [ ] API: Accessing and making requests
- [ ] API: Prompt evaluation
- [ ] API: Prompt engineering
- [ ] API: Tool use
- [ ] API: Retrieval-augmented generation (RAG)
- [ ] API: Claude features (extended thinking, images, PDFs, citations, caching, code execution)
- [ ] API: Model Context Protocol (MCP)
- [ ] API: Agents and workflows
- [ ] Claude on Google Cloud (Vertex AI)
- [ ] Claude Code in Action

### Professional

- [ ] How Claude behaves (the four properties)
- [ ] Platform map and primitives
- [ ] Where Claude fits (delegation)
- [ ] Choosing a pattern (augmented LLM / workflow / agent)
- [ ] Multi-agent systems and orchestration
- [ ] Reference architectures
- [ ] RAG pipeline design
- [ ] Model, context window, and context strategy
- [ ] Prompt architecture and reuse
- [ ] Entry points and interfaces
- [ ] Delivery routes and regulated constraints
- [ ] Evals as acceptance criteria
- [ ] From POC to production
- [ ] Sizing and feasibility
- [ ] Enterprise integration patterns
- [ ] A/B testing and observability
- [ ] Alignment
- [ ] Guardrails
- [ ] Fairness
- [ ] Review routing
- [ ] Compliance
- [ ] Discovery
- [ ] Tradeoff framing and GTM
- [ ] Feedback loops
- [ ] Documentation
- [ ] Entry point and outcome document
- [ ] Team setup
- [ ] Developer workflows
- [ ] Operational support

## How to Use These Notes

| Study mode | What to do |
|---|---|
| **Quick revision** | Jump to the **Quick Revision** section at the bottom of any file for a summary flowchart and concept table |
| **Deep study** | Read top to bottom. Each section follows a visual-first pattern: diagram or table, then explanation |
| **Exam prep** | Focus on the **Exam Traps** tables. They cover the distinctions and common mistakes that are easy to get backwards |
| **Self-test** | Cover the third column of any Exam Traps table and quiz yourself |

## Contributing

Corrections are the most valuable contribution here. Read [CONTRIBUTING.md](CONTRIBUTING.md) for the note conventions and the review checklist, and [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md) before taking part.

Quick ways to help:

- Fix a wrong claim, with a link to the documentation that supports the correction
- Flag a fact that has aged out: a model name, an API field, a feature that moved
- Fill in a topic that is missing or too thin to revise from
- Add an Exam Traps row for a distinction that catches people out

Two hard rules, no exceptions:

1. **No verbatim course material.** Nothing pasted from the Partner Academy courses or any gated training material.
2. **No real exam questions.** Nothing recalled from an exam you sat. [Exam Traps tables are different](CONTRIBUTING.md#why-the-exam-traps-tables-are-different): they are concept-level distinctions derived from public documentation.

## License

This work is licensed under [CC BY-SA 4.0](LICENSE). You are free to share and adapt the material with attribution, under the same licence. Additional notices, including the warranty disclaimer and the code-snippet exemption, are in [NOTICE.md](NOTICE.md).

"Claude", "Anthropic", and the certification names are trademarks of their respective owners, used here for identification only.

## Star History

<a href="https://star-history.com/#shreyabaid007/Claude-Certified-Architect&Date">
 <picture>
   <source media="(prefers-color-scheme: dark)" srcset="https://api.star-history.com/svg?repos=shreyabaid007/Claude-Certified-Architect&type=Date&theme=dark" />
   <source media="(prefers-color-scheme: light)" srcset="https://api.star-history.com/svg?repos=shreyabaid007/Claude-Certified-Architect&type=Date" />
   <img alt="Star History Chart" src="https://api.star-history.com/svg?repos=shreyabaid007/Claude-Certified-Architect&type=Date" />
 </picture>
</a>

If these notes saved you time, a star helps other people preparing for the same exams find them.
