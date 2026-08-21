# Cheatsheet

Every countable set in these notes, on one page. This is the last thing to read before an exam, and the fastest way to check whether a name has fallen out of your head.

Each set links to the note that teaches it. For definitions of individual terms, see the [glossary](GLOSSARY.md).

> [!IMPORTANT]
> **Verify as you read.** Check specific claims against [Anthropic's documentation](https://docs.claude.com); if a note contradicts the docs, the docs win.
> **No exam facts here.** Question counts, time limits, passing scores, and domain weightings are set by Anthropic and change between versions. Read them from the current official exam guide, never from a third-party summary.

---

## Foundations

### The 4 Ds

[AI Fluency](Foundations/01-AI-Fluency-Framework-and-Foundations/README.md)

| D | Ask yourself | Three parts | Stops you from |
|---|---|---|---|
| **Delegation** | Who should do this: me, AI, or both? | Problem · Platform · Task | Handing over work you should have kept |
| **Description** | How do I ask for what I need? | Product · Process · Performance | Getting a great answer to the wrong question |
| **Discernment** | Is the answer any good? | Product · Process · Performance | Using something that sounds right but is wrong |
| **Diligence** | Am I being responsible? | Creation · Transparency · Deployment | Being fast in a way you cannot defend |

Description and Discernment share the same three words: one is for asking, one for checking. That is why they loop.

### Three ways to work with AI

[AI Fluency](Foundations/01-AI-Fluency-Framework-and-Foundations/README.md)

| Mode | You give | AI gives |
|---|---|---|
| **Automation** | The task and the steps | The work |
| **Augmentation** | Your knowledge and judgment | Speed and new angles |
| **Agency** | The goal and the limits | Its own next steps |

Not levels to climb. You switch between all three, often in one chat. Moving right gives more power and less visibility, which is why Diligence matters most on the right.

### Five-step request flow

[Accessing and Making Requests](Foundations/02-Building-with-the-Claude-API/01-Accessing-and-Making-Requests.md)

Request to server → request to Anthropic API → model processing → response to server → response to client.

### Four required API fields

[Accessing and Making Requests](Foundations/02-Building-with-the-Claude-API/01-Accessing-and-Making-Requests.md)

`api_key` · `model` · `messages` · `max_tokens`

Four processing stages: Tokenize → Embed → Contextualize → Generate.

### Three paths after writing a prompt

[Prompt Evaluation](Foundations/02-Building-with-the-Claude-API/02-Prompt-Evaluation.md)

| Path | Risk |
|---|---|
| Test once, ship it | High. Breaks on unexpected inputs |
| Test a few times, tweak | Medium. Misses edge cases users find |
| Run an eval pipeline | Low. Objective scores drive iteration |

### Five-step eval workflow

[Prompt Evaluation](Foundations/02-Building-with-the-Claude-API/02-Prompt-Evaluation.md)

Draft → Dataset → Run → Grade → Iterate

Three grader types: **code** (syntax/format), **model** (quality/task-following), **human** (nuance/depth).

### Four prompt engineering techniques

[Prompt Engineering](Foundations/02-Building-with-the-Claude-API/03-Prompt-Engineering.md)

Be clear and direct · Be specific with guidelines · XML tags for structure · Few-shot examples

Use **descriptive** XML tag names: `<sales_records>`, not `<data>`.

### Four-step tool use loop

[Tool Use](Foundations/02-Building-with-the-Claude-API/04-Tool-Use.md)

| Step | Who acts |
|---|---|
| **1. Initial request** | Your app sends the question plus tool schemas |
| **2. Tool request** | Claude returns a `ToolUse` block naming the function and arguments |
| **3. Data retrieval** | Your app executes the function and collects the result |
| **4. Final response** | Claude receives the result and generates the answer |

**Claude never executes code itself.** Every `ToolUse` block needs a matching `tool_result` block, and the `tools` parameter must still be passed on the follow-up call.

### Built-in tools: who writes what

[Tool Use](Foundations/02-Building-with-the-Claude-API/04-Tool-Use.md)

| | Schema | Implementation | Execution |
|---|---|---|---|
| **Custom tool** | You | You | You |
| **Text editor tool** | Built in | You | You |
| **Web search tool** | Built in | Built in | API |

### Four chunking strategies

[Retrieval-Augmented Generation](Foundations/02-Building-with-the-Claude-API/05-Retrieval-Augmented-Generation.md)

| Strategy | Trade-off |
|---|---|
| **Size-based** | Works on anything; cuts mid-sentence. The common production choice, with overlap |
| **Structure-based** | Cleanest chunks; needs well-formatted docs |
| **Sentence-based** | Good middle ground; ignores section boundaries |
| **Semantic-based** | Most relevant chunks; computationally expensive |

### Retrieval vocabulary

[Retrieval-Augmented Generation](Foundations/02-Building-with-the-Claude-API/05-Retrieval-Augmented-Generation.md)

**Cosine similarity** 1.0 = identical; **cosine distance** is `1 - similarity`, and it is what most vector DBs return. **BM25** is lexical, strong on IDs and exact phrases. **Hybrid search** runs semantic and lexical in parallel. **Reciprocal Rank Fusion** merges ranked lists by rank position, not raw scores.

### Six Claude features

[Claude Features](Foundations/02-Building-with-the-Claude-API/06-Claude-Features.md)

| Feature | Key detail |
|---|---|
| **Extended thinking** | Budget minimum 1024 tokens. Incompatible with pre-filling and temperature |
| **Image support** | Max 100 images per request. Token cost ≈ (w × h) / 750 |
| **PDF support** | `type: "document"`, `media_type: "application/pdf"` |
| **Citations** | Enabled per document block. Returns `cited_text` plus page or character positions |
| **Prompt caching** | Max 4 breakpoints, min 1024 tokens, cache lives 1 hour |
| **Code execution + Files API** | Isolated container, no network. Files uploaded once and referenced by ID |

### Three MCP primitives

[Model Context Protocol](Foundations/02-Building-with-the-Claude-API/07-Model-Context-Protocol.md)

| Primitive | What it is |
|---|---|
| **Tools** | Functions Claude can invoke mid-conversation |
| **Resources** | Read-only data your app fetches by URI, skipping the tool-use loop |
| **Prompts** | Pre-built instruction templates |

**Transport:** stdio for local, HTTP or WebSockets for remote.

### Four workflow patterns and two agent habits

[Agents and Workflows](Foundations/02-Building-with-the-Claude-API/08-Agents-and-Workflows.md)

**Chaining** (sequential sub-tasks) · **Parallelization** (concurrent, then aggregate) · **Routing** (classify, then dispatch) · **Evaluator-optimizer** (produce, grade, iterate).

Agents need **abstract tools** (generic and combinable, not hyper-specialized) and **environment inspection** (observe the result of every action).

### Vertex AI setup: four steps

[Claude on Google Cloud](Foundations/03-Claude-on-Google-Cloud/README.md)

Enable Anthropic models in Vertex AI → enable the specific model in Model Garden → install the gcloud CLI → authenticate.

### Six permission modes

[Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md)

| Config value | UI label |
|---|---|
| `default` | Manual |
| `acceptEdits` | Accept Edits |
| `plan` | Plan |
| `auto` | Auto |
| `dontAsk` | Don't Ask |
| `bypassPermissions` | Bypass Permissions |

The config value is what you write in `settings.json`; the UI label is what the interface shows.

**Shift+Tab cycles `default` → `acceptEdits` → `plan`.** The other three are not in the base cycle: `auto` joins when your account qualifies, `bypassPermissions` joins only if you started with an enabling flag, and `dontAsk` never appears in the cycle at all. Cycle membership is version- and account-dependent, so [re-check the docs](https://code.claude.com/docs/en/permission-modes) for a specific setup.

### Hook events and exit codes

[Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md)

| Event | Can block? |
|---|---|
| **PreToolUse** | Yes. Can also rewrite the call with `updatedInput` |
| **PostToolUse** | Too late to stop. Auto-format, auto-lint |
| **Stop** | Yes. Gate on test pass |
| **SessionStart** | No. Prime environment, restore state |
| **PreCompact / PostCompact** | No |

**Exit 2 blocks** and feeds stderr back to Claude. **Exit 1 does not block.** Exit 0 is success.

**Four config locations, stacked:** enterprise → project → user → local.

---

## Professional

### The four properties

[How Claude Behaves](Professional/01-Claude-Platform-and-Solution-Design/01-How-Claude-Behaves.md)

| Property | Design consequence |
|---|---|
| **Next-token prediction** | Great at common patterns, unreliable on specifics. Citations, retrieval, verifier loops |
| **Knowledge** | Strong on common and recent, weak on rare or changing. RAG, tools, or MCP as source of truth |
| **Working memory** | The context window is a hard edge. What goes in, and in what order, is a design decision |
| **Steerability** | Follows concrete instructions, drifts on abstract ones. Restate the goal alongside the instruction |

### Three layers every deployment passes through

[Platform Map and Primitives](Professional/01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md)

| Layer | What it decides | Examples |
|---|---|---|
| **Entry point** | Who talks to Claude, and how | Claude.ai, Claude Code, a custom app on the API |
| **Build-time interface** | What the partner's code is written to | Direct API, SDKs, MCP, Agent SDK |
| **Delivery route** | Where traffic terminates, whose infrastructure | Anthropic direct, AWS Bedrock, GCP Vertex AI, Microsoft Foundry |

Collapsing these three is a common design error. They are chosen for different reasons: the user, the engineering team, and the compliance posture.

### Seven primitives

[Platform Map and Primitives](Professional/01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md)

| Primitive | Its one job |
|---|---|
| **Tools** | Act |
| **MCP** | Connect |
| **Subagents** | Isolate / parallelize |
| **Hooks** | Guarantee |
| **Skills** | Package a procedure |
| **Agent Teams** | Coordinate peers |
| **Dynamic Workflows** | Compose at runtime |

> **Exam trap:** There is no fixed "core vs optional" grid mapping the seven primitives onto the three patterns. A workflow *often* uses tools; no pattern is defined by a required primitive set.

> **Testable distinction:** A **multi-agent system** is an orchestrator delegating to subagents, which is hierarchical. **Agent Teams** is a separate primitive: agents as coordinated **peers**. Delegation down is not coordination across.

### Three owners

[Where Claude Fits](Professional/01-Claude-Platform-and-Solution-Design/03-Where-Claude-Fits.md)

**What Claude does** (language understanding, summarization, planning, drafting, tool-mediated action) · **what existing systems do** (anything already paid for and made reliable) · **what humans do** (judgment, exceptions, approvals).

The trap is collapsing all three into "what Claude does." Over-assigning to Claude makes the process more expensive, slower, and harder.

### Three patterns

[Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md)

| Pattern | Where control flow lives |
|---|---|
| **Augmented LLM** (also *augmented call*) | Never branches on what the model decides |
| **Workflow** | Named steps orchestrated in your code |
| **Agent** | Inside the model. Goal plus tools, model picks the sequence |

### Four workflow sub-patterns

[Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md)

| Sub-pattern | When it earns its place |
|---|---|
| **Chaining** | Stages with clear handoffs, each output feeding the next |
| **Routing** | Inputs vary in kind and need different handling |
| **Parallelization** | Sub-tasks are independent and can run at once |
| **Evaluator-optimizer** | Quality is verifiable but one attempt is not reliable enough |

### Choosing: five factors in sequence

[Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md)

Predictability → error cost → observability → latency budget → cost.

**The first factor that rules out a pattern is the deciding one.** Low/Medium/High describe what the factor *costs you* under that pattern, so low is favourable. Poorly bounded agents are often the most expensive pattern.

### Five reference architectures

[Reference Architectures](Professional/01-Claude-Platform-and-Solution-Design/06-Reference-Architectures.md)

| Architecture | One way it goes wrong |
|---|---|
| **Agent** | Unbounded autonomy |
| **RAG** | Applied to live state |
| **Document processing pipeline** | No exception path |
| **Customer service / ticket triage** | Retrieval used for live order status |
| **Coding agent** | Editing and committing with no human review gate |

### Multi-agent

[Multi-Agent Systems and Orchestration](Professional/01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md)

**Orchestrator** owns the goal and never does sub-task work. **Subagent** owns one scoped sub-task in its own context.

**Recoverability asymmetry:** subagent failures are usually recoverable, orchestrator failures usually are not. Make subagent work idempotent, protect orchestrator state, propagate one shared trace identifier.

### Four terms that are easy to conflate

[Model, Context Window, and Context Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md)

| Term | Who owns it |
|---|---|
| **Context window** | The model, per call |
| **Retrieval** | Your retrieval layer |
| **Persistent application state** | Your system |
| **Summaries and memory layers** | Your application |

> **Testable distinction:** The model has no native memory between calls. Anything that persists does so because your application stored it and passed it back in. Memory is an architectural choice, not a model capability.

### Four context strategies

[Model, Context Window, and Context Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md)

| Strategy | Reach for it when |
|---|---|
| **Monolithic** | Bounded tasks with predictable input size, and stable prefixes that cache well |
| **Progressive** | Most production workloads. The right default |
| **Retrieval (RAG)** | The corpus is too large to fit in context |
| **Compaction** | Long-running sessions that would hit the limit mid-task |

Monolithic and progressive are the two poles; retrieval and compaction sit between them. Monolithic breaks down as context accumulates turn over turn, and attention quality can degrade well before the hard limit.

### Four caching mechanics

[Prompt Architecture and Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md)

**Cache breakpoints** (mark the fixed/variable boundary) · **content ordering** (static before dynamic, always) · **TTL selection** (match cache life to how often the fixed content changes) · **knowing when the write is not worth it**.

Caching is a design decision, not a default to switch on everywhere.

### Four delivery routes

[Delivery Routes and Regulated Constraints](Professional/01-Claude-Platform-and-Solution-Design/11-Delivery-Routes-and-Regulated-Constraints.md)

| Route | Billed on | Authenticated by | Pick when |
|---|---|---|---|
| **Anthropic first-party** | Anthropic | Anthropic API key | No binding cloud commitment, or newest features matter most |
| **AWS Bedrock** | Partner's AWS account | IAM | A committed AWS enterprise agreement |
| **GCP Vertex AI** | Partner's GCP project | Google Cloud credentials | The ML stack already lives in Vertex |
| **Microsoft Foundry (Azure)** | Partner's Azure subscription | Entra ID | A Microsoft enterprise agreement |

Direct API by default. Bedrock or Vertex when procurement or residency requires it. Foundry requires per-route verification: it offers **two hosting forms** (in the partner's Azure environment, or on Anthropic infrastructure) with different compliance implications.

CSP-mediated routes tend to lag the first-party API on new features. Bedrock uses **inference profiles** for cross-region routing.

### Eval workflow: five stages

[Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md)

Define the task → golden dataset → automated checks → judge scoring → interpret and act.

### The grading ladder

[Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md)

Cheapest reliable method first: **code** → **calibrated judge** → **human**.

Grade with a different model than the one being evaluated (self-preference). Calibrate the judge against human labels before trusting it.

### Three reliability controls

[From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md)

| Control | Where it sits |
|---|---|
| **Exponential backoff** | Closest to the API call |
| **Fallback chain** | Orchestration. Needs its own evals |
| **Circuit breaker** | Service boundary |

### Three feasibility verdicts

[Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md)

| Verdict | What you state alongside it |
|---|---|
| **Feasible as scoped** | The assumptions |
| **Feasible with constraints** | Each constraint, plus its failure mode |
| **Not feasible** | The disqualifying constraint, and any scope reduction that would change the verdict |

### Five ROI pillars, four ROI steps

[Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md)

**Pillars:** efficiency · transformation · productivity · solution cost · performance SLAs.

**Steps:** name the baseline in a business unit → predict the post-deployment state in the same unit → subtract recurring run cost → state payback period and sensitivity.

**Three ways the map goes wrong:** the baseline is estimated rather than measured; the projection assumes full automation when the verdict requires human review; run cost comes from an average instead of the sizing distribution.

### Five integration layers

[Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md)

Compliance constraints → identity and SSO → authorization and policy → data handling and PII → observability and audit logging.

Compliance is a pre-filter: it eliminates routes and entry points before the rest of the design begins. A PII leak into request logs surfaces in the next audit, not the next deployment.

### Four A/B test components

[A/B Testing and Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md)

**Hypothesis** (falsifiable, names the expected direction) · **assignment** (random, consistent per user or session) · **primary metric** (fixed before the run) · **sample size** (from minimum detectable effect, baseline, and confidence).

Choosing the metric after seeing results is **outcome-shopping**. LLM output variance is higher than deterministic systems, so required samples are larger. Statistical significance is not the same question as whether the effect is large enough to matter.

### Failure taxonomy

[A/B Testing and Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md)

Prompt failure · Hallucination · Model mismatch · Orchestrator-workers failure. Each has its own fix, so classify before you fix.

**Drift:** *model drift* is behaviour changing on stable inputs; *data drift* is the input distribution changing.

### Two alignment layers

[Alignment](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/01-Alignment.md)

**Training-time alignment** is set before any deployment exists and knows only broad classes of harm. **Inference-time control** enforces your deployment's rules: system instructions, input and output checks, tool permissions, review gates.

**Claude cannot enforce a rule it was never given.** System instructions shape behaviour; they are not enforcement.

### Four-layer alignment stack

[Alignment](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/01-Alignment.md)

| Layer | Owner | Blind spot |
|---|---|---|
| **1. Trained behavior** | Anthropic | Your domain policy, data rules, authorization model |
| **2. System-prompt instruction** | Architect | Anything an adversarial input can talk Claude out of |
| **3. Runtime screening** | Architect | Actions with side effects; novel attacks a classifier misses |
| **4. Authorization** | Architect | Content quality and fairness |

**Constitution priority order:** broadly safe → ethical → comply with guidelines → genuinely helpful. Holistic, not a strict sequence.

### Five risk categories

[Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md)

| Category | What happens |
|---|---|
| **Direct prompt injection** | User input overrides system instructions |
| **Indirect prompt injection** | Malicious instructions arrive via retrieved content or tool outputs |
| **Token-budget exhaustion** | Oversized or padded inputs truncate work or inflate cost |
| **Tool and action abuse** | Model induced to call a side-effecting tool outside policy |
| **Data exposure** | Sensitive fields enter the context window or the logs |

**Risk assessment entry, six fields:** category · affected component · likelihood · impact · mitigation control · owner · evidence artifact.

### Three guardrail control points

[Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md)

**Input screening** before the model · **output screening** before the user · **authorization** before any side effect.

A control at one point does nothing for the others. Choose **fail closed** explicitly, or the code chooses fail open for you.

**Model-based checks** handle ambiguous intent and can be evaded. **Deterministic checks** handle defined rules and all authorization, and catch only what they anticipated.

### Four fairness injection points

[Fairness](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/03-Fairness.md)

Retrieval corpus · prompt framing · few-shot examples · downstream routing.

Three sit before the model call, one after it. Naming them is what makes fairness an architectural property you can inspect rather than a model attribute.

### Review routing

[Review Routing](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/04-Review-Routing.md)

Route by **reversibility**, **cost of a wrong answer**, and **confidence**, not by volume. Routing by volume floods the queue and reviews collapse into rubber-stamping.

Confidence does not change the stakes; it tells you how much volume to send to a person. **Reviewer view** needs all three: inputs, model output, flag reason. **Consent fatigue** is the failure; move to plan-level or exception review.

### Compliance: obligation to evidence

[Compliance](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/05-Compliance.md)

A framework states an **obligation**; you supply the **technical control**, the **owner**, and the **evidence artifact**.

The evidence artifact is the one most often missed and the one the reviewer checks.

### Discovery: the three-step filter

[Discovery](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/01-Discovery.md)

Listen (the business goal in plain language) → translate (into requirements, assumptions, unresolved constraints) → write down (before the conversation moves on).

### Four discovery categories

[Discovery](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/01-Discovery.md)

| Category | What it produces |
|---|---|
| **Must do** | The work Claude owns versus what stays with a system or a human |
| **Must not do** | Boundaries and forbidden actions. Stakeholders rarely volunteer these, so ask explicitly |
| **Must cost** | A latency target, a per-interaction ceiling, a volume forecast |
| **Must prove** | Proof obligations. Far cheaper to find here than in a legal review weeks later |

### SLAs name three things

[Feedback Loops](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/03-Feedback-Loops.md)

Metric (what are we measuring?) · threshold (what counts as a breach?) · consequence (what happens when one occurs?).

### Three readers, one document

[Documentation](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/04-Documentation.md)

| Reader | What they need |
|---|---|
| **Inheriting engineer** | Decisions, rejected alternatives, and why each was rejected |
| **Compliance reviewer** | Obligation, control, owner, evidence artifact |
| **Returning Architect** | Dated decisions, labelled assumptions, open items with owners |

A document built for one reader and not the others is incomplete even when it is detailed.

### Outcome document: six fields

[Entry Point and Outcome Document](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/05-Entry-Point-and-Outcome-Document.md)

Use case · metric before · metric after · control · measurement owner · reuse potential

### Verification checklist: four dimensions

[Developer Workflows](Professional/05-Team-Enablement-and-Operational-Productivity/02-Developer-Workflows.md)

Correctness · Security · Maintainability · **Human understanding**

The fourth is what catches judgment erosion, where engineers accept output they no longer fully understand.

### Two developer-workflow failure modes

[Developer Workflows](Professional/05-Team-Enablement-and-Operational-Productivity/02-Developer-Workflows.md)

**Lumpy adoption:** a few developers use the tooling heavily, the rest barely touch it, so practice never standardizes. **Stalling at basic chat:** the team treats Claude as a question-answering box and the higher-value workflows are never enabled.

Both look like adoption from a distance and produce little value up close.

---

## Exam logistics

Verified against the [official program page](https://www.pearsonvue.com/us/en/anthropic.html).

| | |
|---|---|
| **Exam codes** | CCAR-F (Foundations), CCAR-P (Professional) |
| **Eligibility** | Claude Partner Network |
| **Prep and registration** | [Anthropic Partner Academy](https://anthropic-partners.skilljar.com/page/partner-certifications) |
| **Scheduling** | Pearson VUE, test centre or OnVUE online proctoring |
| **Retakes** | 14 days after a first attempt, 30 after a second, 90 after a third |
| **Attempt cap** | 4 per exam per rolling 12 months |
| **Badges** | Credly |
| **Fees (as of July 2026)** | $125 Foundations, $175 Professional. Check the current course pages before booking |

**Format, domain weightings, and scoring are not listed here** because they are set by Anthropic and change between exam versions. Read them from the current official exam guide.

---

[Back to the study guide](README.md) · [Glossary](GLOSSARY.md)
