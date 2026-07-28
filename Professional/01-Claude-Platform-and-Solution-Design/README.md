# Claude Platform & Solution Design

Master the design decisions that translate an ambiguous business problem into a defensible Claude solution architecture.

**Status:** In progress

---

## Notes in This Module

| Notes | Covers |
|---|---|
| [01-How-Claude-Behaves](01-How-Claude-Behaves.md) | The four properties, their design consequences, and the context-window error codes |
| [02-Platform-Map-and-Primitives](02-Platform-Map-and-Primitives.md) | Entry points, build-time interfaces, delivery routes, and the seven primitives |
| [03-Where-Claude-Fits](03-Where-Claude-Fits.md) | The three owners, the delegation map, and the deterministic-rule failure mode |
| [04-Choosing-a-Pattern](04-Choosing-a-Pattern.md) | Augmented LLM, workflow, agent; the four workflow sub-patterns; the five-factor choice framework |
| [05-Multi-Agent-Systems-and-Orchestration](05-Multi-Agent-Systems-and-Orchestration.md) | Orchestrator and subagents, fan-out, the recoverability asymmetry, human-in-the-loop checkpoints |

Not yet written: reference architectures and RAG, and model and context strategy.

---

## Four Key Decisions

Before you build anything, you make four decisions:

| # | Decision | What you're answering | Notes |
|---|----------|-----------------------|-------|
| 01 | What part of the work should Claude own? | What goes to Claude, what stays with existing systems, what stays with a human | [Covered](03-Where-Claude-Fits.md) |
| 02 | What shape is the work? | Augmented call, automated workflow, or autonomous agent | [Covered](04-Choosing-a-Pattern.md), plus [multi-agent](05-Multi-Agent-Systems-and-Orchestration.md) |
| 03 | Can you name the reference architecture? | Pick a known blueprint upfront or risk expensive pivots later | Not yet written |
| 04 | Where does your work interact with Claude? | Entry point, model, and context strategy that keep it working and cost-conscious | [Entry points covered](02-Platform-Map-and-Primitives.md), model and context strategy not yet |

---

## Learning Objectives

```mermaid
flowchart LR
    subgraph A["<b>Decompose</b>"]
        A1["Break a request into<br/>Claude vs System vs Human<br/>using 4 AI properties"]
    end

    subgraph B["<b>Select Pattern</b>"]
        B1["Augmented call vs<br/>Workflow vs Agent:<br/>name what each costs"]
    end

    subgraph C["<b>Pick Architecture</b>"]
        C1["Match a reference architecture<br/>to the problem shape.<br/>Spot when RAG masks<br/>a live-state job"]
    end

    subgraph D["<b>Choose Model & Context</b>"]
        D1["Model tier, context window,<br/>context strategy.<br/>Evals gate every swap"]
    end

    subgraph E["<b>Map Entry Points</b>"]
        E1["Claude.ai / API / SDK /<br/>Claude Code / MCP:<br/>right tool, right layer"]
    end

    subgraph F["<b>Apply Governance</b>"]
        F1["User entry points vs<br/>build-time interfaces vs<br/>delivery routes.<br/>Regulatory constraints first"]
    end

    A --> B --> C --> D --> E --> F
```

| Objective | One-liner |
|-----------|-----------|
| **Decompose** | Split work across Claude, existing systems, and humans using the four AI properties |
| **Select Pattern** | Pick augmented call, workflow, or agent and name the cost of each |
| **Pick Architecture** | Match a reference architecture to the problem. Catch retrieval doing a live-state job |
| **Choose Model & Context** | Defend your model tier, context window, and context strategy. Evals gate every swap |
| **Map Entry Points** | Know which entry point fits (Claude.ai, API, SDK, Claude Code, MCP) and what belongs at each layer |
| **Apply Governance** | Separate user-facing entry points, build-time interfaces, and delivery routes. Regulatory constraints rule first |
