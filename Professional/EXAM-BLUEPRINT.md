# CCAR-P Exam Blueprint

Every CCAR-P objective, grouped by exam domain, mapped to the note that covers it. Domain weights are from the official exam guide; the objective-to-note mapping is our own, not an official crosswalk.

| Domain | Weight | ~Questions | Objective | Covered in |
|---|---|---|---|---|
| **1. Solution Design & Architecture** — pattern selection, decomposition, business alignment | 17% | ~11 | Translate business problems into Claude-based AI solutions | [Where Claude Fits](01-Claude-Platform-and-Solution-Design/03-Where-Claude-Fits.md) |
| | | | Design end-to-end architectures (input → processing → output → feedback loops) | [Platform Map & Primitives](01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md), [Reference Architectures](01-Claude-Platform-and-Solution-Design/06-Reference-Architectures.md) |
| | | | Select appropriate architectural patterns (workflow, agentic, augmented LLM) | [Choosing a Pattern](01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md) |
| | | | Design multi-agent systems and orchestration strategies | [Multi-Agent Systems & Orchestration](01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md) |
| | | | Apply decomposition techniques for complex problem solving | [Where Claude Fits](01-Claude-Platform-and-Solution-Design/03-Where-Claude-Fits.md) |
| | | | Align solutions to business value pillars (efficiency, transformation, productivity, cost, SLAs) | [Sizing & Feasibility](02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md) (the Five Pillars), [Tradeoff Framing & GTM](04-Stakeholder-Engagement-Lifecycle-and-GTM/02-Tradeoff-Framing-and-GTM.md) |
| **2. Models, Prompting & Context Engineering** — model tiers, prompt techniques, caching | 13% | ~8 | Design system prompts, templates, and guardrails | [Prompt Architecture & Reuse](01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md), [Guardrails](03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md) |
| | | | Apply prompt engineering techniques (zero-shot, few-shot, chain-of-thought, etc.) | [Prompt Engineering](../Foundations/02-Building-with-the-Claude-API/03-Prompt-Engineering.md) (Foundations note — covers clarity, XML structure, and few-shot; zero-shot/CoT aren't named explicitly) |
| | | | Implement prompt reuse strategies (e.g., caching, modular prompts) | [Prompt Architecture & Reuse](01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md) |
| | | | Evaluate accuracy-latency tradeoffs and justify configuration decisions | [Model, Context Window & Strategy](01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md) |
| **3. Integration** — MCP, RAG, auth, tool scoping (the heaviest domain) | 19% | ~12 | Evaluate tool/agent configuration for capability bloat | [Enterprise Integration Patterns](02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md) (least-privilege tools) |
| | | | Analyze authentication and authorization requirements to identify security gaps | [Enterprise Integration Patterns](02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md), [Guardrails](03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md) |
| | | | Evaluate connection protocols and select the appropriate integration mechanism | [Entry Points & Interfaces](01-Claude-Platform-and-Solution-Design/10-Entry-Points-and-Interfaces.md), [Enterprise Integration Patterns](02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md) |
| **4. Evaluation, Testing & Optimization** — metrics, eval datasets, failure diagnosis | 16% | ~10 | Design evaluation datasets and test frameworks using a mix of testing methodologies | [Evals as Acceptance Criteria](02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md) |
| | | | Diagnose system issues (prompt failure, hallucinations, model mismatch) | [A/B Testing & Observability](02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md) (the failure taxonomy), [Operational Support](05-Team-Enablement-and-Operational-Productivity/03-Operational-Support.md) |
| | | | Optimize token usage, latency, and cost-performance trade-offs | [Model, Context Window & Strategy](01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md), [From POC to Production](02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md) |
| | | | Monitor system performance using logging and observability tools | [A/B Testing & Observability](02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md) |
| | | | Identify risks, limitations, and failure modes of LLM systems | [From POC to Production](02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md), [Guardrails](03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md) |
| **5. Governance, Safety & Risk** — guardrail layers, HITL, compliance frameworks | 14% | ~9 | Apply human-in-the-loop validation strategies | [Multi-Agent Systems & Orchestration](01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md), [Review Routing](03-Responsible-AI-Safety-and-Risk-for-Architects/04-Review-Routing.md) |
| | | | Ensure compliance with regulations (e.g., GDPR, HIPAA, FedRAMP) | [Compliance](03-Responsible-AI-Safety-and-Risk-for-Architects/05-Compliance.md) |
| | | | Address ethical AI considerations (bias, fairness, transparency) | [Fairness](03-Responsible-AI-Safety-and-Risk-for-Architects/03-Fairness.md) |
| **6. Stakeholder Communication & Lifecycle** — discovery, SLAs, ADRs, lifecycle phases | 14% | ~9 | Conduct structured discovery and requirement gathering | [Discovery](04-Stakeholder-Engagement-Lifecycle-and-GTM/01-Discovery.md) |
| | | | Communicate architectural decisions and trade-offs | [Tradeoff Framing & GTM](04-Stakeholder-Engagement-Lifecycle-and-GTM/02-Tradeoff-Framing-and-GTM.md) |
| | | | Manage stakeholder feedback loops and expectation alignment (including SLAs) | [Feedback Loops](04-Stakeholder-Engagement-Lifecycle-and-GTM/03-Feedback-Loops.md) |
| | | | Document architectures and provide implementation guidance | [Documentation](04-Stakeholder-Engagement-Lifecycle-and-GTM/04-Documentation.md) |
| **7. Developer Productivity & Enablement** — Claude Code team configuration | 7% | ~4 | Configure Claude tools and environments for teams (e.g., Claude Code) | [Team Setup](05-Team-Enablement-and-Operational-Productivity/01-Team-Setup.md) |
| | | | Improve developer workflows using AI-assisted tooling | [Developer Workflows](05-Team-Enablement-and-Operational-Productivity/02-Developer-Workflows.md) |
| | | | Support debugging and operational issue resolution | [Operational Support](05-Team-Enablement-and-Operational-Productivity/03-Operational-Support.md) |

---

[Back to the study guide](../README.md)
