# Glossary

Every term in these notes, defined once, in one place. Each entry stands on its own: you should be able to land here from a search, read one definition, and leave without needing the surrounding page.

Where a term is introduced in Foundations and extended in Professional, both senses are given. A term is defined once in this repo and linked thereafter, so if you find a definition here that contradicts a note, [open an issue](../../issues/new/choose).

> [!IMPORTANT]
> **Unofficial.** Independent community notes, not affiliated with or reviewed by Anthropic or Pearson. Check specific claims against [Anthropic's documentation](https://docs.claude.com); if a note contradicts the docs, the docs win.

[A](#a) · [B](#b) · [C](#c) · [D](#d) · [E](#e) · [F](#f) · [G](#g) · [H](#h) · [I](#i) · [J](#j) · [K](#k) · [L](#l) · [M](#m) · [N](#n) · [O](#o) · [P](#p) · [R](#r) · [S](#s) · [T](#t) · [U](#u) · [V](#v) · [W](#w)

---



## A



### Agent

A pattern where Claude receives a goal and a set of tools, then decides its own sequence of steps to reach completion. Control flow lives inside the model rather than in your code, which is what separates an agent from a [workflow](#workflow). Reach for one when you cannot enumerate the steps in advance, or when the same tool set has to serve wildly different goals.

Taught in [Agents and Workflows](Foundations/02-Building-with-the-Claude-API/08-Agents-and-Workflows.md) and [Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md).

### Agent SDK

The library that runs the Claude Code loop from inside your own application code, in TypeScript or Python. It gives you a managed multi-turn loop covering iteration, tool execution, and termination, so you get agentic behaviour without hand-rolling the orchestration. Use it when the work belongs inside your product rather than in a developer's terminal.

Taught in [Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md) and [Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md).

### Augmented LLM

One bounded model call, optionally with tools or retrieval attached. The defining property is that control flow never branches on what the model decides. Also called an **augmented call**; expect either name in a question stem. It is the simplest of the three patterns, and the right default when you know the task and know what good looks like.

Taught in [Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md).

## B



### Batch API

An asynchronous processing path offering a 50% cost reduction and up to 100,000 requests per batch. Available where the SLA tolerates async turnaround. Check BAA coverage before routing regulated data through it.

Taught in [Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md).

### BM25

A lexical (keyword) search algorithm that weights terms by rarity. Strong on identifiers, error codes, and exact phrases, which is precisely where semantic embedding search is weakest. Pairing the two is [hybrid search](#hybrid-search).

Taught in [Retrieval Augmented Generation](Foundations/02-Building-with-the-Claude-API/05-Retrieval-Augmented-Generation.md).

### Boundary condition

A written statement of where an architecture works and where it stops working. Producing these is the step between choosing an architecture and writing a statement of work: without them, the scope has no edge and the SOW cannot describe one.

Taught in [Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md).

### Build-time interface

The layer a partner's engineering team writes code against, such as the API, an SDK, or MCP. Distinct from an [entry point](#entry-point), which is about who talks to Claude, and from a [delivery route](#delivery-route), which is about whose infrastructure the traffic runs on. Chosen for the engineering team and the integration.

Taught in [Platform Map and Primitives](Professional/01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md).

## C



### Cache breakpoint

The boundary between the fixed, cacheable prefix of a prompt and the variable remainder. Everything before the breakpoint can be reused across requests; everything after is reprocessed each time. Placing it well is what makes [prompt caching](#prompt-caching) pay.

Taught in [Prompt Architecture and Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md).

### Chaining

A workflow sub-pattern that breaks a large task into sequential stages with clean handoffs, each stage consuming the previous stage's output. Use it when the task decomposes into stages with defined intermediate outputs, such as extract, then classify, then summarise.

Taught in [Agents and Workflows](Foundations/02-Building-with-the-Claude-API/08-Agents-and-Workflows.md) and [Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md).

### Champion rollout

A team-enablement pattern where one champion per department proves the workflow and seeds the first batch of users before broad rollout follows. It is the standard mitigation for [lumpy adoption](#lumpy-adoption).

Taught in [Team Setup](Professional/05-Team-Enablement-and-Operational-Productivity/01-Team-Setup.md).

### Chunk

The unit of text that gets retrieved in a RAG pipeline. Chunk size and boundary strategy are chosen by the shape of the corpus, not by preference. See also [semantic chunking](#semantic-chunking).

Taught in [RAG Pipeline Design](Professional/01-Claude-Platform-and-Solution-Design/07-RAG-Pipeline-Design.md).

### Circuit breaker

A reliability control that trips on an error-rate threshold so that calls fail fast instead of queueing against a failing dependency. Sits at the service boundary, which distinguishes it from [exponential backoff](#exponential-backoff) (close to the API call) and a [fallback chain](#fallback-chain) (in orchestration).

Taught in [From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md).

### Citations

A Claude API feature that links each claim in a response to the exact source text it came from. Returns `cited_text` plus page numbers for PDFs or character positions for plain text. A direct mitigation for the unreliability of [next-token prediction](#next-token-prediction) on specifics.

Taught in [Claude Features](Foundations/02-Building-with-the-Claude-API/06-Claude-Features.md).

### CLAUDE.md

A guidance file Claude Code loads at launch. It is guidance, not enforced configuration: every line competes with every other line for attention, so the leaner the file, the more reliably any single rule is followed. A rule that must not be skipped belongs in a [hook](#hooks) instead.

Taught in [Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md).

### Claude Code

Anthropic's agentic coding tool, available across terminal, IDE, desktop, and web. The same agent wherever you work. For architects, the constraint that matters is scope: it is a developer workflow tool, not a backend for multi-tenant or customer-facing products.

Taught in [Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md), [Entry Points and Interfaces](Professional/01-Claude-Platform-and-Solution-Design/10-Entry-Points-and-Interfaces.md), and [Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md).

### Code-based eval

A deterministic check that runs in milliseconds: schema validation, regex, parse success, length, or an authoritative lookup. Cheap and perfectly repeatable, but it cannot judge interpretation or quality. First rung of the [grading ladder](#grading-ladder).

Taught in [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md).

### Compaction

Summarising accumulated context so a long session fits back inside the [context window](#context-window). It is one-way and its fidelity is hard to measure, so treat what it discards as genuinely gone.

Taught in [Model, Context Window, and Context Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md).

### Completeness checklist

The test applied to handoff documentation: decision, rejected alternatives, the tradeoff each resolved, owner, evidence artifact, and audit-ready status. It exists so a successor who was never in the room can make a safe change.

Taught in [Documentation](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/04-Documentation.md).

### Confidence

A score estimating how likely a given output is to be wrong. Used to tune how much volume gets routed to human review. Useful only if calibrated: an uncalibrated confidence score is worse than none, because it invites trust it has not earned.

Taught in [Review Routing](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/04-Review-Routing.md).

### Consent fatigue

The failure mode where dozens of approvals in a row turn human review into clicking through. The fix is structural, not motivational: move to plan-level or exception-based review so each approval carries real weight.

Taught in [Review Routing](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/04-Review-Routing.md).

### Constitution

Anthropic's written document of values and behaviour, used during training to generate examples and rank responses. It shapes what the model does by default; it does not know your organisation's policies. See [training-time alignment](#training-time-alignment).

Taught in [Alignment](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/01-Alignment.md).

### Context engineering

Deciding which mechanism is responsible for getting each kind of data in front of the model: retrieval, a tool call, the system prompt, or the conversation itself. The discipline that sits above any individual retrieval choice.

Taught in [Reference Architectures](Professional/01-Claude-Platform-and-Solution-Design/06-Reference-Architectures.md).

### Context window

The model's active attention space. Anything outside it does not exist for that call, and it resets between calls. Its size is a hard edge, not a soft limit: see [working-memory cliff](#working-memory-cliff).

Taught in [Model, Context Window, and Context Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md).

### Cosine similarity

A measure of the angle between two vectors, used to rank embedding search results. 1.0 means identical direction, 0 means unrelated. High similarity means "close in meaning space", which is not the same as "true".

Taught in [Retrieval Augmented Generation](Foundations/02-Building-with-the-Claude-API/05-Retrieval-Augmented-Generation.md).

### Cost projection

Input tokens charged at the input rate plus output tokens charged at the output rate, compared against the budget ceiling. Built before any code is written, as part of [sizing](#sizing).

Taught in [Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md).

## D



### Data drift

The input distribution has changed while the model has not. Distinguished from [model drift](#model-drift), where behaviour on stable inputs changes. Diagnosing which one you have determines whether you fix the pipeline or the prompt.

Taught in [A/B Testing and Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md).

### Decision log

A record of inputs, retrieved context, model output, and routing: enough to replay one decision after the fact. Distinct from observability, which asks whether the system is healthy rather than why one decision happened. In regulated settings the log is itself regulated data.

Taught in [Fairness](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/03-Fairness.md).

### Decision matrix

The rule for choosing a [delivery route](#delivery-route): direct API by default, Bedrock or Vertex when procurement or residency requires it, and Foundry only with per-route verification.

Taught in [Entry Point and Outcome Document](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/05-Entry-Point-and-Outcome-Document.md).

### Delegation

The first of the [4 Ds](#the-4-ds). Deciding what you do, what AI does, and what you do together. Its three parts are problem awareness, platform awareness, and task delegation. The failure it prevents is handing over work you should have kept.

Taught in [AI Fluency](Foundations/01-AI-Fluency-Framework-and-Foundations/README.md).

### Delegation map

The output of decomposing a request: an owner and a justification for every step, split across Claude, existing systems, and humans. The justification matters as much as the owner, because "where can Claude help?" is the wrong question.

Taught in [Where Claude Fits](Professional/01-Claude-Platform-and-Solution-Design/03-Where-Claude-Fits.md).

### Delivery route

Where API traffic terminates and whose infrastructure it runs on: whose cloud account, identity system, region, and contract. Chosen for cloud commitments and compliance posture, not for developer convenience. Distinct from an [entry point](#entry-point) and a [build-time interface](#build-time-interface).

Taught in [Platform Map and Primitives](Professional/01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md) and [Delivery Routes and Regulated Constraints](Professional/01-Claude-Platform-and-Solution-Design/11-Delivery-Routes-and-Regulated-Constraints.md).

### Description

The second of the [4 Ds](#the-4-ds). Asking clearly enough that the model can help properly. Its three parts are product (what you want), process (how to do it), and performance (how to behave). Applied to architecture, it means scope, format, and constraints: what separates a demo prompt from a production one. The failure it prevents is getting a great answer to the wrong question.

Taught in [AI Fluency](Foundations/01-AI-Fluency-Framework-and-Foundations/README.md) and [Prompt Architecture and Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md).

### Deterministic check

A guardrail implemented as a fixed rule rather than a model judgment. Correct for defined rules and for all authorization decisions. Brittle by nature: it catches only what it anticipated. Contrast [model-based check](#model-based-check).

Taught in [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md).

### Diligence

The fourth of the [4 Ds](#the-4-ds). Taking responsibility for what you do with AI and how you do it. Its three parts are creation, transparency, and deployment. Deployment diligence specifically means verifying and vouching for the outputs you use or share; its concrete deliverable is a [verification checklist](#verification-checklist). The failure it prevents is being fast in a way you cannot defend.

Taught in [AI Fluency](Foundations/01-AI-Fluency-Framework-and-Foundations/README.md), [Review Routing](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/04-Review-Routing.md), and [Developer Workflows](Professional/05-Team-Enablement-and-Operational-Productivity/02-Developer-Workflows.md).

### Discernment

The third of the [4 Ds](#the-4-ds). Judging whether what came back is actually good, rather than accepting it because it reads well. Uses the same three parts as [Description](#description): product, process, performance. In production it means classifying each output as acceptable, needs revision, or needs override, and feeding that judgment back into evals. The failure it prevents is using something that sounds right but is wrong.

Taught in [AI Fluency](Foundations/01-AI-Fluency-Framework-and-Foundations/README.md), [Fairness](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/03-Fairness.md), and [A/B Testing and Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md).

### Document processing pipeline

A reference architecture for structured extraction from semi-structured documents such as claims, invoices, and contracts. Handles OCR, extracts fields against a schema, validates, and routes exceptions. Commonly pairs with an [evaluator-optimizer](#evaluator-optimizer), because first-pass extraction on edge cases is not reliable enough to trust unchecked.

Taught in [Reference Architectures](Professional/01-Claude-Platform-and-Solution-Design/06-Reference-Architectures.md).

## E



### Entry point

The wrapper that decides who talks to Claude, what Claude can touch, and how much engineering it takes to get there. Chosen for the user and the work. Distinct from a [build-time interface](#build-time-interface) and a [delivery route](#delivery-route); collapsing these three is a common design error.

Taught in [Platform Map and Primitives](Professional/01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md) and [Entry Points and Interfaces](Professional/01-Claude-Platform-and-Solution-Design/10-Entry-Points-and-Interfaces.md).

### Environment inspection

The principle that an agent must observe the results of its own actions to know whether they succeeded. Without it, an agent proceeds on the assumption that each step worked, which is how silent failures compound.

Taught in [Agents and Workflows](Foundations/02-Building-with-the-Claude-API/08-Agents-and-Workflows.md).

### Escalation path

The documented route for an operational issue that leaves the team: who handles what, when it escalates, and the next-level contact. Pairs with a [runbook](#runbook) to keep the Architect out of every ticket.

Taught in [Operational Support](Professional/05-Team-Enablement-and-Operational-Productivity/03-Operational-Support.md).

### Eval

A structured test checking whether the system returns the expected and accurate output. Evals are the acceptance criteria for an LLM system: they are written before production code and they gate every subsequent change. See also [eval gate](#eval-gate), [code-based eval](#code-based-eval), and [model-based eval](#model-based-eval).

Taught in [Prompt Evaluation](Foundations/02-Building-with-the-Claude-API/02-Prompt-Evaluation.md) and [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md).

### Eval gate

The three things that make a model or prompt swap safe: a test set, a grading function, and a delta threshold. Treat a model swap as a code deployment, not a configuration tweak.

Taught in [Model, Context Window, and Context Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md).

### Evaluator-optimizer

A workflow sub-pattern where a generator produces output, a grader evaluates it against a rubric, and the loop repeats until a criterion passes or a retry limit is hit. Use it when quality is verifiable but a single attempt is not reliable enough.

Taught in [Agents and Workflows](Foundations/02-Building-with-the-Claude-API/08-Agents-and-Workflows.md) and [Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md).

### Exponential backoff

Progressively longer retry delays on `429`, timeout, or `5xx` responses. Sits closest to the API call of the three reliability controls; compare [fallback chain](#fallback-chain) and [circuit breaker](#circuit-breaker).

Taught in [From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md).

### Extended thinking

A billed, per-request reasoning pass before the model answers. Enable it for a measured accuracy gap, not by default: it costs tokens and latency on every request it touches.

Taught in [Claude Features](Foundations/02-Building-with-the-Claude-API/06-Claude-Features.md) and [Model, Context Window, and Context Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md).

## F



### Fail closed

Designing a control so that when it errors or is unavailable, traffic is blocked rather than passed. The alternative, fail open, looks like protection while providing none. Choose the direction explicitly, or the code chooses fail open for you.

Taught in [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md).

### Failure taxonomy

The categories a production LLM failure falls into: prompt failure, hallucination, model mismatch, and orchestrator-workers failure. Each has a different fix, which is why classifying the failure comes before fixing it.

Taught in [A/B Testing and Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md).

### Fallback chain

Serving an alternative model tier or a cached response instead of an error. Sits in the orchestration layer. Because the fallback path produces different output, it needs its own evals.

Taught in [From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md).

### Fan-out

The most common multi-agent shape: split a work item into independent units, dispatch one [subagent](#subagent) per unit, then synthesise the returned results. The win is that each subagent gets a clean context sized to its unit, and independent units run concurrently.

Taught in [Multi-Agent Systems and Orchestration](Professional/01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md).

### Feasibility

A verdict plus the constraints that make the verdict true. A feasibility assessment that only asks "can Claude do this" is a capability check; a real one names the compensating controls each of the four properties demands.

Taught in [Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md).

### FedRAMP control

An Anthropic-documented authorized route at the required impact level, used exclusively. Partial routing defeats the control.

Taught in [Compliance](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/05-Compliance.md).

### Feedback loop

A decision layer sitting above the observability stack, mapping signals to triage, decision, action, and review. Observability tells you a number moved; the feedback loop is what makes something happen as a result.

Taught in [Feedback Loops](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/03-Feedback-Loops.md).

### Few-shot examples

Input/output pairs included in a prompt to show the model what an ideal response looks like. More effective when you also explain why the example is good, rather than leaving the model to infer the pattern.

Taught in [Prompt Engineering](Foundations/02-Building-with-the-Claude-API/03-Prompt-Engineering.md).

### Fine-grained mode

A tool-use setting that disables API-side JSON validation for faster streaming, in exchange for you handling malformed tool input yourself.

Taught in [Tool Use](Foundations/02-Building-with-the-Claude-API/04-Tool-Use.md).

## G



### Golden dataset

Representative inputs paired with expected outputs, including edge cases and counterexamples. The word doing the work is *representative*: a dataset that does not reflect production traffic produces evals that do not mean anything.

Taught in [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md).

### Governance table

A table mapping each production signal to a trigger, an owner, and an action. It exists before launch, and it covers slow drifts as well as hard failures, because a slow drift has no obvious moment that prompts someone to look.

Taught in [Feedback Loops](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/03-Feedback-Loops.md).

### Governing layers

The Claude Code layers controlling what the agent is *allowed to touch*: hooks, permissions, and sandboxing. Contrast [shaping layers](#shaping-layers), which control what it knows and does.

Taught in [Entry Points and Interfaces](Professional/01-Claude-Platform-and-Solution-Design/10-Entry-Points-and-Interfaces.md).

### Grading ladder

The rule for choosing an eval grader: cheapest reliable method first. Code where a deterministic check works, then a calibrated judge model, then a human. Climbing a rung costs money and time, so only climb when the rung below genuinely cannot judge the thing.

Taught in [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md).

## H



### HIPAA control

A HIPAA-ready plan or first-party API under a signed BAA, with compliance mode enabled and only eligible features in use. Using an ineligible feature under a signed BAA is still a gap.

Taught in [Compliance](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/05-Compliance.md).

### Hooks

Deterministic code that runs at fixed points in the agentic loop, enforcing a rule the model cannot skip. `PreToolUse` can block or rewrite a call, `Stop` can refuse to end a turn, and exit code 2 is the blocking code (exit 1 does not block). The difference between a hook and [CLAUDE.md](#claudemd) is the difference between enforcement and guidance.

Taught in [Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md) and [Platform Map and Primitives](Professional/01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md).

### Human-in-the-loop checkpoint

A gate that pauses execution for human review, positioned by the risk and reversibility of the action about to be taken. Gate the irreversible, sample the rest: gating everything produces [consent fatigue](#consent-fatigue).

Taught in [Multi-Agent Systems and Orchestration](Professional/01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md).

### Hybrid search

Running semantic (embedding) and lexical ([BM25](#bm25)) search in parallel and merging the ranked lists, usually with [reciprocal rank fusion](#reciprocal-rank-fusion). Covers conceptual queries and exact-match queries, which no single index does well.

Taught in [Retrieval Augmented Generation](Foundations/02-Building-with-the-Claude-API/05-Retrieval-Augmented-Generation.md) and [RAG Pipeline Design](Professional/01-Claude-Platform-and-Solution-Design/07-RAG-Pipeline-Design.md).

## I



### Indirect injection

Malicious instructions arriving through retrieved content or tool outputs, which the model may treat as trusted. Input screening does not catch it, because the content enters after the input check has already passed. Retrieved content and tool outputs need their own classifier.

Taught in [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md).

### Inference-time control

Everything your application layer enforces at request time: system instructions, input and output checks, tool permissions, and review gates. This is where your organisation's rules live, because [training-time alignment](#training-time-alignment) never saw them.

Taught in [Alignment](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/01-Alignment.md).

## J



### Judge calibration

Confirming that a judge model agrees with human-labeled outputs before you trust its scores. An uncalibrated judge running at scale is worse than no judge, because it produces confident numbers nobody checks.

Taught in [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md).

### Judgment erosion

The failure where engineers accept output they no longer fully understand, because it looks right and passes shallow checks. Human understanding is the fourth dimension of the [verification checklist](#verification-checklist) precisely to catch this.

Taught in [Developer Workflows](Professional/05-Team-Enablement-and-Operational-Productivity/02-Developer-Workflows.md).

## K



### Knowledge

One of the [four properties](#the-four-properties). Claude is strong on common, recent, consistent topics and weak on rare or changing ones. The design consequence is that anything authoritative should come from RAG, a tool, or MCP rather than from the model's [parametric knowledge](#parametric-knowledge).

Taught in [How Claude Behaves](Professional/01-Claude-Platform-and-Solution-Design/01-How-Claude-Behaves.md).

## L



### Latency drivers

What actually determines response time: task complexity, model size, and output length. Notably *not* request volume, which is the intuition most people bring and the one that produces wrong capacity plans.

Taught in [Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md).

### Least privilege on tools

Scoping each agent's tool access to exactly its task. Every tool is both attack surface and token cost, so a subagent should not inherit the orchestrator's full tool set.

Taught in [Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md).

### Lumpy adoption

A rollout where a few heavy users and many non-users means practice never standardises. The team gets an average that describes nobody. [Champion rollout](#champion-rollout) is the counter.

Taught in [Developer Workflows](Professional/05-Team-Enablement-and-Operational-Productivity/02-Developer-Workflows.md).

## M



### MCP

**Model Context Protocol.** An open standard that shifts tool definitions and execution out of your application and into specialised servers. Architecturally it is a sharing convention across products, not a calling convention within one: build a server once and multiple Claude clients reach the same tools. The tradeoff is harder tool-call debugging, since the tool no longer lives in your codebase.

Taught in [Model Context Protocol](Foundations/02-Building-with-the-Claude-API/07-Model-Context-Protocol.md), [Platform Map and Primitives](Professional/01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md), and [Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md).

### MCP Client

The communication bridge between your application and one or more MCP servers. Handles the connection and relays tool calls; it does not implement the tools.

Taught in [Model Context Protocol](Foundations/02-Building-with-the-Claude-API/07-Model-Context-Protocol.md).

### MCP Server

A process wrapping an external service and exposing [tools](#tools), [resources](#resources), and [prompts](#prompts) for clients to consume.

Taught in [Model Context Protocol](Foundations/02-Building-with-the-Claude-API/07-Model-Context-Protocol.md).

### Model drift

Behaviour on stable inputs changing gradually over time. Detecting it needs periodic distribution comparison, not threshold alerts, because the change is slow enough that no single request crosses a threshold. Distinguish from [data drift](#data-drift).

Taught in [A/B Testing and Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md).

### Model version pinning

Pinning to a specific model version, monitoring deprecation notices, and keeping a migration runbook. Operational discipline required by every architecture, not just agentic ones.

Taught in [From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md).

### Model-based check

A guardrail that uses a model to judge ambiguous intent or language quality. Handles what a rule cannot express, and can be evaded by a determined input. Contrast [deterministic check](#deterministic-check).

Taught in [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md).

### Model-based eval

A judge model scoring output against a rubric, with its reasoning captured alongside the score. Handles quality judgments code cannot make; inconsistent on borderline cases unless reasoning is forced. Requires [judge calibration](#judge-calibration).

Taught in [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md).

### Multi-turn evals

A separate eval category that scores whole conversations rather than single responses, with its own golden dataset of transcripts. A system that scores well per-response can still fail across a conversation.

Taught in [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md).

## N



### Necessity filter

The data-handling rule: if a field is not required for the language task, it does not belong in the context window. Applied before encryption or access control, because the cheapest data to protect is data you never sent.

Taught in [Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md).

### Next-token prediction

One of the [four properties](#the-four-properties). The model is excellent at common patterns and unreliable on specifics. Mitigate with [citations](#citations), authoritative retrieval, and verifier loops rather than by asking it to try harder.

Taught in [How Claude Behaves](Professional/01-Claude-Platform-and-Solution-Design/01-How-Claude-Behaves.md).

### Non-determinism

The same input producing different outputs across runs. The design consequence is that you cannot certify behaviour you observed only once, which is why a demo is not evidence.

Taught in [How Claude Behaves](Professional/01-Claude-Platform-and-Solution-Design/01-How-Claude-Behaves.md).

## O



### Observability vs decision logging

The same instrumentation serving two questions. Observability asks whether the system is healthy. Decision logging asks why one specific decision happened. A system can be fully observable and still unable to explain a single outcome to a regulator.

Taught in [Fairness](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/03-Fairness.md).

### Orchestrator

In a multi-agent system, the agent that owns the goal: it decomposes the work, delegates to [subagents](#subagent), and synthesises the results. It never does the sub-task work itself. Protect its state, because of the [recoverability asymmetry](#recoverability-asymmetry).

Taught in [Multi-Agent Systems and Orchestration](Professional/01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md).

### Outcome document

The artifact that makes value legible to a non-technical sponsor. Six fields: use case, metric before, metric after, control, measurement owner, and reuse potential. Volume and error rate tell a sponsor the system runs, not what it is worth expanding.

Taught in [Entry Point and Outcome Document](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/05-Entry-Point-and-Outcome-Document.md).

## P



### p95

The value below which 95% of requests complete. A better design target than the median, because the median hides the tail that users actually complain about.

Taught in [From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md).

### Parallelization

A workflow sub-pattern that splits a task into independent sub-tasks, runs them concurrently, and aggregates the results. Requires that no sub-task depends on another's output.

Taught in [Agents and Workflows](Foundations/02-Building-with-the-Claude-API/08-Agents-and-Workflows.md) and [Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md).

### Parametric knowledge

What the model learned during training, as opposed to what it was given at request time. The architectural alternative is an authoritative answer from a retrieved source.

Taught in [How Claude Behaves](Professional/01-Claude-Platform-and-Solution-Design/01-How-Claude-Behaves.md).

### Payback period

The time for accumulated gain to cover build plus run cost. Never quote one without a [sensitivity analysis](#sensitivity-analysis), because the number moves sharply with small assumption changes.

Taught in [Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md).

### Permission modes

The six modes controlling what Claude Code can do without prompting. Config values are `default`, `acceptEdits`, `plan`, `auto`, `dontAsk`, and `bypassPermissions`; `default` is labelled **Manual** in the interface. Shift+Tab cycles `default` → `acceptEdits` → `plan` only: `auto` joins when the account qualifies, `bypassPermissions` when started with an enabling flag, and `dontAsk` never.

Taught in [Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md) and [Entry Points and Interfaces](Professional/01-Claude-Platform-and-Solution-Design/10-Entry-Points-and-Interfaces.md).

### Plugins

One installable unit bundling skills, hooks, subagents, and MCP configs. A plugin runs code on your machine with your privileges, and its hooks fire on every matching tool call, so read what it contains before enabling it. Reviewed is not the same as trusted.

Taught in [Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md).

### Priority order

The ordering in Anthropic's [constitution](#constitution): broadly safe, ethical, compliant with guidelines, genuinely helpful. Holistic rather than a strict sequence.

Taught in [Alignment](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/01-Alignment.md).

### Prompt caching

Preserving the processed prefix of a prompt so it is not reprocessed on every request. Savings scale with prefix length and reuse rate, which is why the [cache breakpoint](#cache-breakpoint) placement matters more than enabling the feature.

Taught in [Claude Features](Foundations/02-Building-with-the-Claude-API/06-Claude-Features.md) and [From POC to Production](Professional/02-Enterprise-Integration-and-Production/02-From-POC-to-Production.md).

### Prompt drift

An ungoverned prompt copied across teams becoming many quietly different versions, with no way to tell which one produced a given output. The reason a [prompt library](#prompt-library) or a [Skill](#skill) is a governance decision, not a tidiness one.

Taught in [Prompt Architecture and Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md).

### Prompt library

Shared prompt fragments that engineers assemble in their own code. Lightweight governance: enough to stop [prompt drift](#prompt-drift), less ceremony than a versioned [Skill](#skill).

Taught in [Prompt Architecture and Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md).

### Prompts

As an MCP primitive: pre-built instruction templates exposed by a server, which produce better results than ad-hoc user input.

Taught in [Model Context Protocol](Foundations/02-Building-with-the-Claude-API/07-Model-Context-Protocol.md).

## R



### RAG

**Retrieval Augmented Generation.** Break documents into [chunks](#chunk), search for the relevant ones, and include only those in the prompt. The alternative, including everything, fails on cost, latency, and the [context window](#context-window) at once. Watch for retrieval being used where a live-state tool call is actually needed.

Taught in [Retrieval Augmented Generation](Foundations/02-Building-with-the-Claude-API/05-Retrieval-Augmented-Generation.md) and [RAG Pipeline Design](Professional/01-Claude-Platform-and-Solution-Design/07-RAG-Pipeline-Design.md).

### Reciprocal rank fusion

The standard, low-tuning method for merging two ranked result lists. Favours items that rank well in both, which is what makes it a sensible default for [hybrid search](#hybrid-search).

Taught in [RAG Pipeline Design](Professional/01-Claude-Platform-and-Solution-Design/07-RAG-Pipeline-Design.md).

### Recoverability asymmetry

In multi-agent systems, [subagent](#subagent) failures are usually recoverable (retry, re-route, or flag the gap) while [orchestrator](#orchestrator) failures usually are not. Design for it: make subagent work idempotent and retryable, and protect orchestrator state.

Taught in [Multi-Agent Systems and Orchestration](Professional/01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md).

### Refusal handling

Detecting `stop_reason: "refusal"` plus `stop_details`, routing by category, and then resetting the context. A refused turn left in context tends to produce further refusals.

Taught in [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md).

### Rejected alternatives

The options not chosen and the tradeoff that ruled each one out. Without these, a successor cannot tell which choices are load-bearing, and will silently reverse one.

Taught in [Documentation](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/04-Documentation.md).

### Residency control

Regional processing and storage, plus validation that logs, caches, monitoring, and retention all stay inside the boundary. The failure is usually not the inference call; it is a log shipped somewhere else.

Taught in [Compliance](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/05-Compliance.md).

### Resources

As an MCP primitive: read-only data your application fetches by URI, skipping the tool-use loop entirely. Use when the app knows what it needs, rather than letting the model decide.

Taught in [Model Context Protocol](Foundations/02-Building-with-the-Claude-API/07-Model-Context-Protocol.md).

### Reversal cost

What it costs to undo an architectural decision later. The third question most tradeoff presentations skip, and the one that most often changes the outcome of a meeting.

Taught in [Tradeoff Framing and GTM](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/02-Tradeoff-Framing-and-GTM.md).

### Reviewer view

What a human reviewer needs to actually do the job: the inputs, the model output, and the reason it was flagged. Missing any one of the three degrades the review into a rubber stamp.

Taught in [Review Routing](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/04-Review-Routing.md).

### Risk assessment artifact

The written deliverable a security reviewer signs: category, component, likelihood and impact, mitigation, owner, and evidence. A risk assessment that lives only in someone's head is not a control.

Taught in [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md).

### Rollback criterion

The threshold at which you revert, set before the data comes in, so you never negotiate with yourself afterwards.

Taught in [Model, Context Window, and Context Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md).

### Routines

A saved prompt plus repo plus trigger, running on Anthropic's infrastructure with no server to build. Triggers can be a cron schedule, an HTTP POST, or a GitHub event. Recurring schedules run at most hourly, and each run starts from a fresh clone.

Taught in [Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md).

### Routing

A workflow sub-pattern where a classifier reads the input first and dispatches it to a specialised downstream path. Use it when inputs vary in kind and different kinds need different handling.

Taught in [Agents and Workflows](Foundations/02-Building-with-the-Claude-API/08-Agents-and-Workflows.md) and [Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md).

### Runbook

Known symptom-to-cause-to-action paths the team can follow without the Architect. The artifact that turns operational support from escalation into self-service.

Taught in [Operational Support](Professional/05-Team-Enablement-and-Operational-Productivity/03-Operational-Support.md).

## S



### Sample size

Derived from the minimum detectable effect, the baseline rate, and the confidence level. Larger for LLM experiments than for conventional A/B tests, because output variance is higher.

Taught in [A/B Testing and Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md).

### Scoping sequence

Requirement to capabilities, capabilities to architecture, architecture to [boundary conditions](#boundary-condition), conditions to SOW. Skipping a link produces a statement of work with no defensible edge.

Taught in [Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md).

### Self-preference

The bias where a model rates its own output more favourably. The mitigation is to grade with a different model than the one being evaluated.

Taught in [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md).

### Semantic chunking

Splitting a document on meaning boundaries so each [chunk](#chunk) is self-contained, reducing mid-idea cuts. One of several chunking strategies; the corpus decides which fits.

Taught in [RAG Pipeline Design](Professional/01-Claude-Platform-and-Solution-Design/07-RAG-Pipeline-Design.md).

### Sensitivity analysis

Testing how fragile a cost or ROI model is if volume doubles or the distribution shifts toward the tail. The difference between a projection and a guess.

Taught in [Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md).

### Server-side identity

Injecting the user's role into the system prompt from your server, rather than trusting a claim made in a user message. User-message claims are unverifiable by construction, so authorization built on them is not authorization.

Taught in [Enterprise Integration Patterns](Professional/02-Enterprise-Integration-and-Production/04-Enterprise-Integration-Patterns.md).

### Shadow testing

Sending copied production traffic to a new version while users always receive the current response, then scoring the shadow outputs offline. Gets you production-distribution evidence with zero user risk.

Taught in [A/B Testing and Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md).

### Shaping layers

The Claude Code layers controlling what the agent *knows and does*: CLAUDE.md, Skills, subagents, and MCP servers. Contrast [governing layers](#governing-layers).

Taught in [Entry Points and Interfaces](Professional/01-Claude-Platform-and-Solution-Design/10-Entry-Points-and-Interfaces.md).

### Shared configuration

A project-level baseline (CLAUDE.md, tools, permissions) that every developer on the team starts from. The point is that it is shared and checked in, not assembled personally by each engineer.

Taught in [Team Setup](Professional/05-Team-Enablement-and-Operational-Productivity/01-Team-Setup.md).

### Shared trace identifier

One identifier propagated across orchestrator and subagents so a single multi-agent run can be reconstructed end to end. Without it, traces fragment and a dropped unit is invisible.

Taught in [Multi-Agent Systems and Orchestration](Professional/01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md).

### Silent degradation

A RAG pipeline that was correct at launch decaying as documents are added, with no error and no alert. The reason retrieval quality needs periodic re-measurement rather than one-time validation.

Taught in [RAG Pipeline Design](Professional/01-Claude-Platform-and-Solution-Design/07-RAG-Pipeline-Design.md).

### Sizing

A cost model built before any code, accurate enough to validate the architecture against the budget. Covers call volume, token consumption, and cost. See [cost projection](#cost-projection) and [sensitivity analysis](#sensitivity-analysis).

Taught in [Sizing and Feasibility](Professional/02-Enterprise-Integration-and-Production/03-Sizing-and-Feasibility.md).

### Skill

A versioned, self-contained `SKILL.md` unit packaging a procedure, optionally with reference docs and scripts alongside it. Only skill descriptions load at launch, so there is little cost to packaging every procedure you repeat. The heavier-governance alternative to a [prompt library](#prompt-library).

Taught in [Claude Code in Action](Foundations/04-Claude-Code-in-Action/README.md) and [Prompt Architecture and Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md).

### Skill supply chain

Treating third-party skills as dependencies: trusted source, audit for anomalous and out-of-scope calls, a recorded verdict, and a sandboxed runtime. A skill is executable content, so it carries the risks of a dependency.

Taught in [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md).

### SLA structure

Metric, threshold, consequence. The threshold has to trace back to a discovery constraint or an eval baseline; a threshold with no provenance cannot be defended when it is missed.

Taught in [Feedback Loops](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/03-Feedback-Loops.md).

### Spend posture

Model defaults, allowlists, effort guidance, and per-user caps, set before the team starts using the system rather than after the first surprising invoice.

Taught in [Team Setup](Professional/05-Team-Enablement-and-Operational-Productivity/01-Team-Setup.md).

### Statistical significance

A result unlikely to be chance at the given sample size. It says nothing about whether the effect is large enough to be worth shipping, which is a separate judgment.

Taught in [A/B Testing and Observability](Professional/02-Enterprise-Integration-and-Production/05-AB-Testing-and-Observability.md).

### Steerability

One of the [four properties](#the-four-properties). Claude follows concrete instructions well and drifts on abstract ones. The mitigation is to restate the goal alongside the instruction, which reappears later as a prompt-design technique.

Taught in [How Claude Behaves](Professional/01-Claude-Platform-and-Solution-Design/01-How-Claude-Behaves.md).

### Streaming

Receiving the response incrementally rather than waiting for completion, via `stream=True` or `client.messages.stream()`. Changes perceived latency without changing total latency.

Taught in [Accessing and Making Requests](Foundations/02-Building-with-the-Claude-API/01-Accessing-and-Making-Requests.md).

### Structured output

Getting clean, parseable data instead of prose commentary, by prefilling the assistant message and using a stop sequence.

Taught in [Accessing and Making Requests](Foundations/02-Building-with-the-Claude-API/01-Accessing-and-Making-Requests.md).

### Subagent

In a multi-agent system, an agent owning one scoped sub-task in its own context, returning a result to the [orchestrator](#orchestrator). Make its work idempotent and retryable: see [recoverability asymmetry](#recoverability-asymmetry).

Taught in [Multi-Agent Systems and Orchestration](Professional/01-Claude-Platform-and-Solution-Design/05-Multi-Agent-Systems-and-Orchestration.md).

### Success criteria

What an eval suite has to specify: the specific behaviour, a threshold derived from the business requirement, failure-mode categories, and adversarial inputs. A threshold with no business provenance is a number someone made up.

Taught in [Evals as Acceptance Criteria](Professional/02-Enterprise-Integration-and-Production/01-Evals-as-Acceptance-Criteria.md).

### System prompts

Role and rules set via the `system` parameter, separate from the conversation messages. Behavioural instructions given here persist for the whole conversation.

Taught in [Accessing and Making Requests](Foundations/02-Building-with-the-Claude-API/01-Accessing-and-Making-Requests.md).

## T



### Template

A prompt with parameterized slots inside fixed scaffolding. The scaffolding is where guarantees live; the slots are where variation is allowed.

Taught in [Prompt Architecture and Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md).

### Temperature

A request parameter controlling output randomness: 0 is deterministic, 1 is creative. Pick the range by task type rather than leaving the default.

Taught in [Accessing and Making Requests](Foundations/02-Building-with-the-Claude-API/01-Accessing-and-Making-Requests.md).

### Text embedding

A numerical representation of meaning, where similar text produces similar numbers. The basis of semantic search; compared with [cosine similarity](#cosine-similarity).

Taught in [Retrieval Augmented Generation](Foundations/02-Building-with-the-Claude-API/05-Retrieval-Augmented-Generation.md).

### The 4 Ds

The four AI Fluency competencies: **[Delegation](#delegation), [Description](#description), [Discernment](#discernment), [Diligence**](#diligence). Description and Discernment share the same three parts (product, process, performance) because one is for asking and the other for checking, which is why they loop together.

Taught in [AI Fluency](Foundations/01-AI-Fluency-Framework-and-Foundations/README.md).

### The four properties

The four behavioural properties an architect reasons from: **[next-token prediction](#next-token-prediction), [knowledge](#knowledge), [working memory](#working-memory), [steerability**](#steerability). They are the lens applied to every step of a [delegation map](#delegation-map), and they are present whether or not your architecture acknowledges them.

Taught in [How Claude Behaves](Professional/01-Claude-Platform-and-Solution-Design/01-How-Claude-Behaves.md).

### Token counting

Measuring actual token usage with the `usage` field rather than estimating from character counts, because characters-per-token varies by content.

Taught in [Model, Context Window, and Context Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md).

### Tool schema

The JSON object with `name`, `description`, and `input_schema` that tells Claude how to call a function. The description is doing more work than the name: it is what the model reasons about when deciding whether the tool applies.

Taught in [Tool Use](Foundations/02-Building-with-the-Claude-API/04-Tool-Use.md).

### Tool use

The structured mechanism by which Claude requests external data or actions and receives results back. The loop is: model requests a tool, your code executes it, you return the result, the model continues.

Taught in [Tool Use](Foundations/02-Building-with-the-Claude-API/04-Tool-Use.md).

### Tools

As a platform primitive: a function the model can call to take an action or fetch a result. This is what lets the model *act* rather than only produce text.

As an MCP primitive: functions Claude can invoke mid-conversation, defined on a server with `@mcp.tool` and type hints.

Taught in [Platform Map and Primitives](Professional/01-Claude-Platform-and-Solution-Design/02-Platform-Map-and-Primitives.md) and [Model Context Protocol](Foundations/02-Building-with-the-Claude-API/07-Model-Context-Protocol.md).

### Tradeoff translation map

The shift from architecture framing to stakeholder decision language, done per choice. The same decision has to be sayable in both vocabularies or the review stalls.

Taught in [Tradeoff Framing and GTM](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/02-Tradeoff-Framing-and-GTM.md).

### Training-time alignment

Safety behaviour set before your deployment exists, and therefore general by design. It lowers baseline risk; it does not know your data-handling rules, authorization model, or domain policy. Assuming it covers a rule it was never given is the most common way a safety design fails. See [inference-time control](#inference-time-control).

Taught in [Alignment](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/01-Alignment.md).

### Translation table

The discovery artifact with one row per item: stakeholder statement, implied constraint, required architectural decision, and the assumption to document. It is what turns a preference into a testable constraint.

Taught in [Discovery](Professional/04-Stakeholder-Engagement-Lifecycle-and-GTM/01-Discovery.md).

### Transport

How an MCP client and server connect: stdio for local processes, HTTP or WebSockets for remote.

Taught in [Model Context Protocol](Foundations/02-Building-with-the-Claude-API/07-Model-Context-Protocol.md).

## U



### Underspecification

A gap in a prompt that the model fills with its own assumption, differently each time. The root cause of output variance that looks like [non-determinism](#non-determinism) but is actually a prompt defect.

Taught in [Prompt Architecture and Reuse](Professional/01-Claude-Platform-and-Solution-Design/09-Prompt-Architecture-and-Reuse.md).

## V



### Vector database

A store specialised for embedding search. Always keep the original text alongside the vector: you retrieve by vector but you send text to the model.

Taught in [Retrieval Augmented Generation](Foundations/02-Building-with-the-Claude-API/05-Retrieval-Augmented-Generation.md).

### Verification checklist

The explicit gate AI-generated output passes before production, across four dimensions: correctness, security, maintainability, and human understanding. It is the concrete deliverable that [Diligence](#diligence) produces, and a team writes its own.

Taught in [Developer Workflows](Professional/05-Team-Enablement-and-Operational-Productivity/02-Developer-Workflows.md).

### Vulnerability assessment

Walking the request and data paths to find where risk enters: user input, retrieved content, tool outputs, model output, and logs. Produces the [risk assessment artifact](#risk-assessment-artifact).

Taught in [Guardrails](Professional/03-Responsible-AI-Safety-and-Risk-for-Architects/02-Guardrails.md).

## W



### Working memory

One of the [four properties](#the-four-properties). The [context window](#context-window) is a hard edge, so what goes into it, and in what order, is a design decision rather than an implementation detail.

Taught in [How Claude Behaves](Professional/01-Claude-Platform-and-Solution-Design/01-How-Claude-Behaves.md).

### Working-memory cliff

The hardest edge of the four properties: a system works until it does not, then fails abruptly rather than degrading. It rarely appears during development on small, clean inputs, which is why it surfaces in production.

Taught in [Model, Context Window, and Context Strategy](Professional/01-Claude-Platform-and-Solution-Design/08-Model-Context-Window-and-Context-Strategy.md).

### Workflow

Named steps orchestrated in your code, with the model called at defined points. Because the control flow is yours, it is loggable, testable, and reasoned about like any other software. Contrast [agent](#agent), where control flow lives inside the model.

Taught in [Agents and Workflows](Foundations/02-Building-with-the-Claude-API/08-Agents-and-Workflows.md) and [Choosing a Pattern](Professional/01-Claude-Platform-and-Solution-Design/04-Choosing-a-Pattern.md).

---

[Back to the study guide](README.md) · [Cheatsheet](CHEATSHEET.md) · [Contributing](CONTRIBUTING.md)