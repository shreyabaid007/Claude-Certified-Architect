# Claude Certified Architect — Study Notes

Notes for the two Claude Certified Architect exams. Each note leads with a diagram or table, then explains, and ends with a quick-revision summary.

Official course: [Claude Certified Architect Professional](https://anthropic-partners.skilljar.com/path/claude-certified-architect-professional). Full A–Z terms are in the [Glossary](GLOSSARY.md).

## Foundations - CCAR-F

1. [AI Fluency: Framework & Foundations](Foundations/01-AI-Fluency-Framework-and-Foundations/)
2. [Building with the Claude API](Foundations/02-Building-with-the-Claude-API/)
3. [Claude on Google Cloud](Foundations/03-Claude-on-Google-Cloud/)
4. [Claude Code in Action](Foundations/04-Claude-Code-in-Action/)

## Professional - CCAR-P

1. [Claude Platform & Solution Design](Professional/01-Claude-Platform-and-Solution-Design/)
2. [Enterprise Integration & Production](Professional/02-Enterprise-Integration-and-Production/)
3. [Responsible AI, Safety & Risk](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/)
4. [Stakeholder Engagement & GTM](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/)
5. [Team Enablement & Ops](Professional/05-Team-Enablement-and-Operational-Productivity/)

### CCAR-P Exam Blueprint

| Domain | Weight | ~Questions | Objective | Covered in |
|---|---|---|---|---|
| **1. Solution Design & Architecture** — pattern selection, decomposition, business alignment | 17% | ~11 | Translate business problems into Claude-based AI solutions | [Where Claude Fits](Professional/01-Claude-Platform-and-Solution-Design/03-Where-Claude-Fits.md) |
| | | | Design end-to-end architectures (input → processing → output → feedback loops) | [Platform Map & Primitives](Professional/01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md), [Reference Architectures](Professional/01-Claude-Platform-and-Solution-Design/06-Reference-Architectures.md) |
| | | | Select appropriate architectural patterns (workflow, agentic, augmented LLM) | [Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md) |
| | | | Design multi-agent systems and orchestration strategies | [Multi-Agent Systems & Orchestration](Professional/01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md) |
| | | | Apply decomposition techniques for complex problem solving | [Where Claude Fits](Professional/01-Claude-Platform-and-Solution-Design/03-Where-Claude-Fits.md) |
| | | | Align solutions to business value pillars (efficiency, transformation, productivity, cost, SLAs) | [Sizing & Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md) (the Five Pillars), [Tradeoff Framing & GTM](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/02-Tradeoff-Framing-and-GTM.md) |
| **2. Models, Prompting & Context Engineering** — model tiers, prompt techniques, caching | 13% | ~8 | Design system prompts, templates, and guardrails | [Prompt Architecture & Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md), [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md) |
| | | | Apply prompt engineering techniques (zero-shot, few-shot, chain-of-thought, etc.) | [Prompt Engineering](Foundations/02-Building-with-the-Claude-API/03-Prompt-Engineering.md) (Foundations note — covers clarity, XML structure, and few-shot; zero-shot/CoT aren't named explicitly) |
| | | | Implement prompt reuse strategies (e.g., caching, modular prompts) | [Prompt Architecture & Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md) |
| | | | Evaluate accuracy-latency tradeoffs and justify configuration decisions | [Model, Context Window & Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md) |
| **3. Integration** — MCP, RAG, auth, tool scoping (the heaviest domain) | 19% | ~12 | Evaluate tool/agent configuration for capability bloat | [Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md) (least-privilege tools) |
| | | | Analyze authentication and authorization requirements to identify security gaps | [Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md), [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md) |
| | | | Evaluate connection protocols and select the appropriate integration mechanism | [Entry Points & Interfaces](Professional/01-Claude-Platform-and-Solution-Design/10-Entry-Points-and-Interfaces.md), [Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md) |
| **4. Evaluation, Testing & Optimization** — metrics, eval datasets, failure diagnosis | 16% | ~10 | Design evaluation datasets and test frameworks using a mix of testing methodologies | [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md) |
| | | | Diagnose system issues (prompt failure, hallucinations, model mismatch) | [A/B Testing & Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md) (the failure taxonomy), [Operational Support](Professional/05-Team-Enablement-and-Operational-Productivity/03-Operational-Support.md) |
| | | | Optimize token usage, latency, and cost-performance trade-offs | [Model, Context Window & Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md), [From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md) |
| | | | Monitor system performance using logging and observability tools | [A/B Testing & Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md) |
| | | | Identify risks, limitations, and failure modes of LLM systems | [From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md), [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md) |
| **5. Governance, Safety & Risk** — guardrail layers, HITL, compliance frameworks | 14% | ~9 | Apply human-in-the-loop validation strategies | [Multi-Agent Systems & Orchestration](Professional/01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md), [Review Routing](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/04-Review-Routing.md) |
| | | | Ensure compliance with regulations (e.g., GDPR, HIPAA, FedRAMP) | [Compliance](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/05-Compliance.md) |
| | | | Address ethical AI considerations (bias, fairness, transparency) | [Fairness](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/03-Fairness.md) |
| **6. Stakeholder Communication & Lifecycle** — discovery, SLAs, ADRs, lifecycle phases | 14% | ~9 | Conduct structured discovery and requirement gathering | [Discovery](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/01-Discovery.md) |
| | | | Communicate architectural decisions and trade-offs | [Tradeoff Framing & GTM](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/02-Tradeoff-Framing-and-GTM.md) |
| | | | Manage stakeholder feedback loops and expectation alignment (including SLAs) | [Feedback Loops](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/03-Feedback-Loops.md) |
| | | | Document architectures and provide implementation guidance | [Documentation](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/04-Documentation.md) |
| **7. Developer Productivity & Enablement** — Claude Code team configuration | 7% | ~4 | Configure Claude tools and environments for teams (e.g., Claude Code) | [Team Setup](Professional/05-Team-Enablement-and-Operational-Productivity/01-Team-Setup.md) |
| | | | Improve developer workflows using AI-assisted tooling | [Developer Workflows](Professional/05-Team-Enablement-and-Operational-Productivity/02-Developer-Workflows.md) |
| | | | Support debugging and operational issue resolution | [Operational Support](Professional/05-Team-Enablement-and-Operational-Productivity/03-Operational-Support.md) |

---

<a href="https://www.credly.com/badges/dccf39e5-7132-40cf-a4c3-d4bbf5258660/public_url"><img src="badge.png" alt="Claude Certified Architect – Professional" width="110" align="left"></a>

I put these notes together while preparing for the Claude Certified Architect — Professional (CCAR-P) exam, which I’m happy to share I’ve [successfully cleared](https://www.credly.com/badges/dccf39e5-7132-40cf-a4c3-d4bbf5258660/public_url). 🎉

Sharing them here in the hope that they can make the preparation journey a little easier for others. If they help, a ⭐ is appreciated — it helps others preparing for the same exam find this.

Licensed under [CC BY 4.0](LICENSE).
