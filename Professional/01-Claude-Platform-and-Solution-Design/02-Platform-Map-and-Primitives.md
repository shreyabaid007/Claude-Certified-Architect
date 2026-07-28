# Platform Map & Primitives

You know the four properties from the previous section. Now name the two remaining pieces of vocabulary before any design decision: the three layers a deployment passes through, and the seven primitives you assemble solutions from.

---

## Three Layers, Three Distinct Decisions

These layers are not alternatives. Every deployment involves all three. Confusing them is the most common source of muddled architecture conversations.

```mermaid
flowchart TD
    classDef concept fill:#fff3cd,stroke:#ffc107,color:#000

    subgraph EP["<b>ENTRY POINTS</b> · Stakeholder: User"]
        direction LR
        E1["Claude.ai<br/>(web/mobile/desktop)"]:::concept
        E2["Claude Code"]:::concept
        E3["Custom App<br/>built on the API"]:::concept
    end

    subgraph BI["<b>BUILD-TIME INTERFACES</b> · Stakeholder: Engineer"]
        direction LR
        B1["Direct API"]:::concept
        B2["SDKs"]:::concept
        B3["MCP"]:::concept
        B4["Agent SDK"]:::concept
    end

    subgraph DR["<b>DELIVERY ROUTES</b> · Stakeholder: Infra"]
        direction LR
        D1["Anthropic<br/>directly"]:::concept
        D2["AWS<br/>Bedrock"]:::concept
        D3["GCP<br/>Vertex AI"]:::concept
        D4["Microsoft<br/>Foundry"]:::concept
    end

    EP ==> BI ==> DR
```

| Layer | Chosen for | Stakeholder |
|-------|-----------|-------------|
| **Entry Point** | The user and the work | End user, product owner |
| **Build-Time Interface** | The engineering team and the integration | Developer, tech lead |
| **Delivery Route** | Cloud commitments and compliance posture | Infrastructure, security, procurement |

> **The key:** A decision in one layer rarely dictates the others. These are three different conversations with three different stakeholders.

### Scenario: Collapsing the Layers

> **The trap:** A retail banking proposal put Claude Code (an engineering entry point) in front of non-engineering branch staff because "it's all Claude." The same model does sit underneath every entry point, but the entry point is the wrapper. Claude Code was built for developers in a terminal, not for bank staff following a workflow. Collapsing the three layers into one erased the distinction that should have ruled the choice out immediately.

### Cost, Complexity, Risk

```mermaid
flowchart LR
    classDef risk fill:#fce4ec,stroke:#e91e63,color:#000

    C["<b>Cost</b><br/>Picking the wrong layer because<br/>the vocabulary was unclear means<br/>paying for the wrong solution,<br/>then paying again to replace it."]:::risk
    X["<b>Complexity</b><br/>When the three layers are named<br/>precisely, a design review isolates<br/>which decision is contested.<br/>When blurred, it argues in circles."]:::risk
    R["<b>Risk</b><br/>An entry point chosen before the<br/>user is named is a common,<br/>avoidable architecture error<br/>traceable to collapsing the<br/>three layers into one."]:::risk

    C ~~~ X ~~~ R
```

---

## Seven Primitives, Seven Jobs

Every pattern in this course (augmented call, workflow, agent) is an assembly of these primitives. Name them once here so later lessons become combinations of parts you already recognize.

```mermaid
flowchart LR
    classDef concept fill:#fff3cd,stroke:#ffc107,color:#000

    T["<b>Tools</b><br/>Act"]:::concept
    M["<b>MCP</b><br/>Connect"]:::concept
    S["<b>Subagents</b><br/>Isolate /<br/>Parallelize"]:::concept
    H["<b>Hooks</b><br/>Guarantee"]:::concept
    SK["<b>Skills</b><br/>Package a<br/>Procedure"]:::concept
    AT["<b>Agent Teams</b><br/>Coordinate<br/>Peers"]:::concept
    DW["<b>Dynamic<br/>Workflows</b><br/>Compose at<br/>Runtime"]:::concept

    T ~~~ M ~~~ S ~~~ H
    SK ~~~ AT ~~~ DW
    T ~~~ SK
```

| Primitive | Job | What it is |
|-----------|-----|------------|
| **Tools** | Act | A function the model can call to take an action or fetch a result from your code |
| **MCP** | Connect | A protocol for exposing a set of tools so multiple Claude clients reach the same entry points |
| **Subagents** | Isolate / Parallelize | Hand a scoped sub-task to a separate context so work runs in isolation or in parallel |
| **Hooks** | Guarantee | Deterministic code that fires on defined events to enforce a rule the model cannot skip |
| **Skills** | Package a Procedure | A versioned, reusable unit (instructions plus optional scripts) that packages a repeatable procedure |
| **Agent Teams** | Coordinate Peers | Multiple agents working as coordinated peers, each owning part of a larger goal |
| **Dynamic Workflows** | Compose at Runtime | Assemble the steps of a workflow at runtime rather than fixing them in advance |

> **Tip:** Agent Teams and Dynamic Workflows extend older vocabulary of single agents and fixed workflows. You will see them named in current practitioner conversations even though many existing systems predate them.

### How Primitives Become Patterns

You are not choosing among primitives yet. Here is the preview of how they compose:

```mermaid
flowchart LR
    classDef concept fill:#fff3cd,stroke:#ffc107,color:#000

    W["<b>Workflow</b><br/>Steps wired in YOUR code<br/>You control the sequence<br/><br/>Core: Tools<br/>Opt: Hooks"]:::concept
    A["<b>Agent</b><br/>Model chooses ITS OWN<br/>sequence of Tool calls<br/><br/>Core: Tools<br/>Opt: Skills, Hooks"]:::concept
    MA["<b>Multi-Agent System</b><br/>Orchestrator delegates<br/>to Subagents<br/><br/>Core: Tools, Subagents,<br/>Agent Teams<br/>Opt: Dynamic Workflows"]:::concept

    W --- A --- MA
```

| Pattern | Core Primitives | Optional Primitives |
|---------|----------------|---------------------|
| **Workflow** | Tools | Hooks |
| **Agent** | Tools | Skills, Hooks |
| **Multi-Agent System** | Tools, Subagents, Agent Teams | Dynamic Workflows, Hooks |

> **The key:** A Workflow is you telling the model what to do step by step. An Agent is the model deciding its own steps. A Multi-Agent System is agents coordinating as a team. The control shifts from you to the model as you move right.

### Scenario: Missing Shared Vocabulary

> **The trap:** In an architecture review, someone said "we'll use an agent." Five people heard five different things: a single tool-using model, a multi-step workflow, a team of subagents, Claude Code, and a chatbot. The design conversation stalled for twenty minutes before anyone realized they were describing different architectures with the same word.

Shared vocabulary eliminates this. The primitives table above is the starting point.

### Cost, Complexity, Risk

```mermaid
flowchart LR
    classDef risk fill:#fce4ec,stroke:#e91e63,color:#000

    C["<b>Cost</b><br/>Reaching for a heavier primitive<br/>than the job requires is paid in<br/>latency, tokens, and operational<br/>surface area on every request."]:::risk
    X["<b>Complexity</b><br/>Each primitive added is a part to<br/>build, observe, and govern. Use<br/>the fewest primitives necessary<br/>to meet the requirement."]:::risk
    R["<b>Risk</b><br/>Without shared vocabulary, teams<br/>cannot communicate effectively<br/>because they do not agree on<br/>what the parts are."]:::risk

    C ~~~ X ~~~ R
```

---

## Quick Revision

```mermaid
flowchart LR
    classDef concept fill:#fff3cd,stroke:#ffc107,color:#000
    classDef action fill:#d4edda,stroke:#28a745,color:#000

    A["<b>Three Layers</b><br/>Entry Point<br/>Build-Time Interface<br/>Delivery Route"]:::concept --> B["<b>Different stakeholders</b><br/>User / Engineer / Infra<br/>Don't collapse them"]:::concept
    B --> C["<b>Seven Primitives</b><br/>Tools, MCP, Subagents,<br/>Hooks, Skills,<br/>Agent Teams,<br/>Dynamic Workflows"]:::concept
    C --> D["<b>Compose into Patterns</b><br/>Workflow / Agent /<br/>Multi-Agent System"]:::action
```

| Concept | One-liner |
|---------|-----------|
| **Entry Point** | What the user interacts with (Claude.ai, Claude Code, custom app) |
| **Build-Time Interface** | What the engineer codes against (API, SDK, MCP, Agent SDK) |
| **Delivery Route** | Where traffic terminates (Anthropic, Bedrock, Vertex, Foundry) |
| **Tools** | Let the model act: call a function, fetch a result |
| **MCP** | Expose tools so multiple clients share the same entry points |
| **Subagents** | Scoped sub-tasks in separate contexts for isolation or parallelism |
| **Hooks** | Deterministic enforcement the model cannot skip |
| **Skills** | Versioned, reusable procedures packaged for repeat use |
| **Agent Teams** | Coordinated peer agents, each owning part of a goal |
| **Dynamic Workflows** | Steps assembled at runtime, not hardcoded in advance |
| **Don't collapse layers** | Entry point, interface, and route are three conversations with three stakeholders |
| **Fewest primitives** | Each one added is a part to build, observe, and govern |

### Exam Traps

Cover the third column and quiz yourself.

| If you see... | The trap | The right call |
|---------------|----------|----------------|
| "Should we use an entry point or a delivery route?" | Picking one over the other | They are not alternatives. Every deployment involves all three layers. |
| Claude Code proposed for bank branch staff | "It's all Claude, same model underneath" | Wrong entry point for the user. Entry point is chosen for the user, not the model. |
| "We'll use an agent" in an architecture review | Treating it as a complete architecture statement | Name which primitives: "a tool-calling agent" or "subagents with an orchestrator." |
| "Enforce a rule the model must never violate" | System prompt with strong wording | Hooks. Only primitive that fires deterministically. The model cannot skip a hook. |
| Fixed predictable steps vs dynamic sequence | Calling both "an agent" | Fixed steps = Workflow (you control). Dynamic = Agent (model controls). |
| "We need Agent Teams for this two-step task" | Reaching for the heaviest primitive | Use the fewest primitives. A single tool call may be all you need. |
