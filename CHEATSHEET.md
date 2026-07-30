# Cheatsheet

Every countable set in these notes, on one page. This is the last thing to read before an exam, and the fastest way to check whether a name has fallen out of your head.

Each set links to the note that teaches it. For definitions of individual terms, see the [glossary](GLOSSARY.md).

> [!IMPORTANT]
> **Unofficial.** Independent community notes, not affiliated with or reviewed by Anthropic or Pearson.
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

**Automation** (AI does the task you describe) → **Augmentation** (you and AI think together) → **Agency** (AI works alone inside your rules).

Not levels to climb. You switch between all three, often in one chat. Moving right gives more power and less visibility, which is why Diligence matters most on the right.

### Four required API fields

`api_key` · `model` · `messages` · `max_tokens`

Four processing stages: Tokenize → Embed → Contextualize → Generate.

### Five-step eval workflow

Draft → Dataset → Run → Grade → Iterate

Three grader types: **code** (syntax/format), **model** (quality/task-following), **human** (nuance/depth).

### Four prompt engineering techniques

Be clear and direct · Be specific with guidelines · XML tags for structure · Few-shot examples

### Three MCP primitives

| Primitive | What it is |
|---|---|
| **Tools** | Functions Claude can invoke mid-conversation |
| **Resources** | Read-only data your app fetches by URI, skipping the tool-use loop |
| **Prompts** | Pre-built instruction templates |

**Transport:** stdio for local, HTTP or WebSockets for remote.

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

Shift+Tab cycles the everyday ones. The config value is what you write in `settings.json`; the UI label is what the interface shows.

### Hook events and exit codes

| Event | Can block? |
|---|---|
| **PreToolUse** | Yes. Can also rewrite the call with `updatedInput` |
| **PostToolUse** | Too late to stop. Auto-format, auto-lint |
| **Stop** | Yes. Gate on test pass |
| **SessionStart** | No. Prime environment, restore state |
| **PreCompact / PostCompact** | No |

**Exit 2 blocks** and feeds stderr back to Claude. **Exit 1 does not block.** Exit 0 is success.

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

### Three patterns

[Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md)

| Pattern | Where control flow lives |
|---|---|
| **Augmented LLM** (also *augmented call*) | Never branches on what the model decides |
| **Workflow** | Named steps orchestrated in your code |
| **Agent** | Inside the model. Goal plus tools, model picks the sequence |

### Four workflow sub-patterns

| Sub-pattern | When it earns its place |
|---|---|
| **Chaining** | Stages with clear handoffs, each output feeding the next |
| **Routing** | Inputs vary in kind and need different handling |
| **Parallelization** | Sub-tasks are independent and can run at once |
| **Evaluator-optimizer** | Quality is verifiable but one attempt is not reliable enough |

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

**Orchestrator** owns the goal and never does sub-task work. **Subagent** owns one scoped sub-task in its own context.

**Recoverability asymmetry:** subagent failures are usually recoverable, orchestrator failures usually are not. Make subagent work idempotent, protect orchestrator state, propagate one shared trace identifier.

### Three reliability controls

[From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md)

| Control | Where it sits |
|---|---|
| **Exponential backoff** | Closest to the API call |
| **Fallback chain** | Orchestration. Needs its own evals |
| **Circuit breaker** | Service boundary |

### The grading ladder

Cheapest reliable method first: **code** → **calibrated judge** → **human**.

Grade with a different model than the one being evaluated (self-preference). Calibrate the judge against human labels before trusting it.

### Three feasibility verdicts

| Verdict | What you state alongside it |
|---|---|
| **Feasible as scoped** | The assumptions |
| **Feasible with constraints** | Each constraint, plus its failure mode |
| **Not feasible** | The disqualifying constraint, and any scope reduction that would change the verdict |

### Failure taxonomy

Prompt failure · Hallucination · Model mismatch · Orchestrator-workers failure. Each has its own fix, so classify before you fix.

**Drift:** *model drift* is behaviour changing on stable inputs; *data drift* is the input distribution changing.

### Five risk categories

[Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md)

| Category | What happens |
|---|---|
| **Direct prompt injection** | User input overrides system instructions |
| **Indirect prompt injection** | Malicious instructions arrive via retrieved content or tool outputs |
| **Token-budget exhaustion** | Oversized or padded inputs truncate work or inflate cost |
| **Tool and action abuse** | Model induced to call a side-effecting tool outside policy |
| **Data exposure** | Sensitive fields enter the context window or the logs |

### Three guardrail control points

**Input screening** before the model · **Output screening** before the user · **Authorization** before any side effect.

A control at one point does nothing for the others. Choose **fail closed** explicitly, or the code chooses fail open for you.

**Model-based checks** handle ambiguous intent and can be evaded. **Deterministic checks** handle defined rules and all authorization, and catch only what they anticipated.

### Four-layer alignment stack

[Alignment](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/01-Alignment.md)

| Layer | Owner | Blind spot |
|---|---|---|
| **1. Trained behavior** | Anthropic | Your domain policy, data rules, authorization model |
| **2. System-prompt instruction** | Architect | Anything an adversarial input can talk Claude out of |
| **3. Runtime screening** | Architect | Actions with side effects; novel attacks a classifier misses |
| **4. Authorization** | Architect | Content quality and fairness |

**Constitution priority order:** broadly safe → ethical → comply with guidelines → genuinely helpful. Holistic, not a strict sequence.

### Review routing

Route by **reversibility**, **cost of a wrong answer**, and **confidence**, not by volume. Routing by volume floods the queue and reviews collapse into rubber-stamping.

**Reviewer view** needs all three: inputs, model output, flag reason. **Consent fatigue** is the failure; move to plan-level or exception review.

### Outcome document: six fields

Use case · metric before · metric after · control · measurement owner · reuse potential

### Verification checklist: four dimensions

Correctness · Security · Maintainability · **Human understanding**

The fourth is what catches judgment erosion, where engineers accept output they no longer fully understand.

### Delivery route decision matrix

Direct API by default. Bedrock or Vertex when procurement or residency requires it. Foundry requires per-route verification.

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

[Back to the study guide](README.md) · [Glossary](GLOSSARY.md) · [Contributing](CONTRIBUTING.md)
