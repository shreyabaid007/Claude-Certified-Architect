# How Claude Behaves

Four properties of the model shape every design decision that follows. None are flaws to fix. Each is a force you design around, the way a structural engineer designs around the properties of building materials.

> **The goal:** Recognize the four properties by name and understand each one's design consequences. You are not making design decisions yet. You are building the vocabulary for them.

---

## The Four Properties at a Glance

```mermaid
flowchart TD
    center["<b>Claude's Four Properties</b><br/>Every capability has a matching limitation"]

    NTP["<b>Next-Token Prediction</b><br/>Excels at patterns.<br/>Fails at specifics."]
    K["<b>Knowledge</b><br/>Strong on common topics.<br/>Weak on rare or changing ones."]
    WM["<b>Working Memory</b><br/>Powerful inside the window.<br/>Nothing exists outside it."]
    S["<b>Steerability</b><br/>Follows concrete instructions.<br/>Drifts on abstract ones."]

    center --> NTP
    center --> K
    center --> WM
    center --> S

    style NTP fill:#fff3cd,stroke:#ffc107,color:#000
    style K fill:#fff3cd,stroke:#ffc107,color:#000
    style WM fill:#fff3cd,stroke:#ffc107,color:#000
    style S fill:#fff3cd,stroke:#ffc107,color:#000
```

The same characteristic that makes Claude capable in one situation is the same one that makes it fail in another. Read each property below as a capability paired with its limitation and the mitigation an architect reaches for.

---

## Property 1: Next-Token Prediction

```mermaid
flowchart LR
    classDef green fill:#d4edda,stroke:#28a745,color:#000
    classDef red fill:#f8d7da,stroke:#dc3545,color:#000
    classDef blue fill:#cce5ff,stroke:#007bff,color:#000

    C["<b>Capability</b><br/>Summarizing, reformatting,<br/>explaining well-established<br/>concepts and common patterns"]:::green --- L["<b>Limitation</b><br/>Precision on specifics.<br/>Names, dates, citations,<br/>statistics. Looks accurate,<br/>but isn't."]:::red --- M["<b>Mitigation</b><br/>Citations, uncertainty signaling,<br/>generator-verifier loops.<br/>Route factual lookups<br/>through tool calls."]:::blue
```

---

## Property 2: Knowledge

```mermaid
flowchart LR
    classDef green fill:#d4edda,stroke:#28a745,color:#000
    classDef red fill:#f8d7da,stroke:#dc3545,color:#000
    classDef blue fill:#cce5ff,stroke:#007bff,color:#000

    C["<b>Capability</b><br/>Topics that are common,<br/>recent, and consistently<br/>represented in training data"]:::green --- L["<b>Limitation</b><br/>Rare, niche, contested, or<br/>frequently changing topics.<br/>Stale info presented with<br/>the same confident tone."]:::red --- M["<b>Mitigation</b><br/>Web search, RAG, tool use,<br/>or MCP servers. Make an<br/>external system the source<br/>of truth."]:::blue
```

---

## Property 3: Working Memory

```mermaid
flowchart LR
    classDef green fill:#d4edda,stroke:#28a745,color:#000
    classDef red fill:#f8d7da,stroke:#dc3545,color:#000
    classDef blue fill:#cce5ff,stroke:#007bff,color:#000

    C["<b>Capability</b><br/>Anything that fits in<br/>the active context window"]:::green --- L["<b>Limitation</b><br/>Hard edge. Once content<br/>falls outside the window,<br/>the model has zero<br/>access to it."]:::red --- M["<b>Mitigation</b><br/>Progressive context loading,<br/>chunking, front-loading<br/>critical info. Summarize<br/>across turns."]:::blue
```

Two distinct errors happen at the context window edge:

| Error | When it happens | What you see |
|-------|-----------------|--------------|
| **Oversized request** | Prompt is too large to send | `400 invalid_request_error` (token limit) or `413 request_too_large` (byte limit). Rejected before generation. |
| **Truncated output** | Prompt fits, but generation hits the window ceiling | `model_context_window_exceeded` stop reason. Output cuts off mid-response. |

> **Tip:** Check the `usage` field on every response and use the token-counting API before you send to avoid hitting either limit.

---

## Property 4: Steerability

```mermaid
flowchart LR
    classDef green fill:#d4edda,stroke:#28a745,color:#000
    classDef red fill:#f8d7da,stroke:#dc3545,color:#000
    classDef blue fill:#cce5ff,stroke:#007bff,color:#000

    C["<b>Capability</b><br/>Short, concrete, verifiable<br/>instructions with defined<br/>formats, explicit length<br/>limits, and clear roles"]:::green --- L["<b>Limitation</b><br/>Abstract or ambiguous<br/>instructions, long reasoning<br/>chains, precise computation.<br/>Follows letter, drifts<br/>from intent."]:::red --- M["<b>Mitigation</b><br/>System prompts, structured<br/>outputs, code execution.<br/>Restate the goal alongside<br/>the instruction when they<br/>might diverge."]:::blue
```

---

## From Property to Design Consequence

Each property maps to a design consequence you will use later in the course.

```mermaid
flowchart LR
    classDef blue fill:#cce5ff,stroke:#007bff,color:#000
    classDef yellow fill:#fff3cd,stroke:#ffc107,color:#000
    classDef green fill:#d4edda,stroke:#28a745,color:#000

    P1["<b>Next-Token<br/>Prediction</b>"]:::blue
    P2["<b>Knowledge</b>"]:::blue
    P3["<b>Working<br/>Memory</b>"]:::blue
    P4["<b>Steerability</b>"]:::blue

    D1["<b>Non-determinism</b><br/>Same input, different outputs.<br/>You cannot certify behavior<br/>you only observed once."]:::yellow
    D2["<b>Knowledge &<br/>Capability Boundaries</b><br/>Reliable on common topics.<br/>Unreliable on rare or<br/>fast-changing ones."]:::yellow
    D3["<b>Context as a<br/>Finite Resource</b><br/>What you put in, the order,<br/>and what you leave out<br/>are design decisions."]:::yellow
    D4["<b>Confidence Is<br/>Not Validity</b><br/>Wrong answers arrive in<br/>the same fluent tone<br/>as right ones."]:::yellow

    P1 --> D1
    P2 --> D2
    P3 --> D3
    P4 --> D4

    D1 -. "Feeds" .-> E1["Evaluation frameworks<br/><i>Module 2</i>"]:::green
    D2 -. "Feeds" .-> E2["Reference architectures<br/>& RAG<br/><i>Later in Module 1</i>"]:::green
    D3 -. "Feeds" .-> E3["Model & context<br/>strategy<br/><i>Later in Module 1</i>"]:::green
    D4 -. "Feeds" .-> E4["Human-in-the-loop<br/>& verification<br/><i>Module 3</i>"]:::green
```

| Property | Design Consequence | Where it applies |
|----------|--------------------|------------------|
| **Next-Token Prediction** | **Non-determinism.** Same input can produce different outputs. Evaluation frameworks exist because you cannot certify behavior observed only once. | Evaluation work (Module 2) |
| **Knowledge** | **Knowledge and capability boundaries.** Reliable on common, recent, consistent topics. For everything else, use web search, RAG, tools, or MCP as the source of truth. | Reference architectures & RAG (Module 1) |
| **Working Memory** | **Context as a finite resource.** The context window has a fixed token budget. What goes in, in what order, and what stays out are design decisions affecting quality and cost. | Model & context strategy (Module 1) |
| **Steerability** | **Confidence is not validity.** Claude can be wrong in the same fluent, assured tone it uses when right. Human-in-the-loop and verification are architectural choices, not afterthoughts. | Responsible deployment (Module 3) |

---

## Scenario: A Failure That Began with a Misread Property

> **The trap:** An architect saw a demo run cleanly five times in a row and concluded the behavior was deterministic. The team shipped a financial reconciliation pipeline that treated each model output as a fixed, repeatable result with no checks.
>
> In the second week of production the outputs drifted: the same statement, re-processed, produced a different categorization. The discrepancy was discovered by chance when an analyst happened to re-run a batch.
>
> Nothing changed in the input. Different outputs were produced because the model is non-deterministic and the architecture was built as though it was not.

The lesson: a demo is not evidence of determinism. The four properties are present whether your architecture acknowledges them or not.

---

## Cost, Complexity, Risk

```
┌──────────────────────────────────────────────────────────────┐
│  Cost        → Designing without these properties is the     │
│                most expensive mistake. The cost lands after   │
│                launch, when rework is most expensive and      │
│                rebuilding trust is hardest.                   │
├──────────────────────────────────────────────────────────────┤
│  Complexity  → Naming the properties up front keeps later    │
│                conversations precise. "This is a knowledge-  │
│                boundary problem" beats debating if the model  │
│                is "good enough."                              │
├──────────────────────────────────────────────────────────────┤
│  Risk        → The properties do not announce themselves.    │
│                A system that ignores them won't produce an    │
│                error. It drifts quietly. Found in an audit    │
│                or by an angry user, not by the system itself. │
└──────────────────────────────────────────────────────────────┘
```

---

## Quick Revision

```mermaid
flowchart LR
    A["<b>Four Properties</b><br/>Next-Token Prediction<br/>Knowledge<br/>Working Memory<br/>Steerability"] --> B["<b>Each Has</b><br/>A capability<br/>A matching limitation<br/>An architect's mitigation"]
    B --> C["<b>Design Consequences</b><br/>Non-determinism<br/>Knowledge boundaries<br/>Finite context<br/>Confidence ≠ validity"]
    C --> D["<b>Architect's Job</b><br/>Design around them.<br/>Never assume they<br/>are absent."]

    style A fill:#fff3cd,stroke:#ffc107,color:#000
    style D fill:#d4edda,stroke:#28a745,color:#000
```

| Concept | One-liner |
|---------|-----------|
| **Next-Token Prediction** | Great at patterns, unreliable on specifics. Mitigate with citations and verifier loops. |
| **Knowledge** | Strong on common topics, weak on rare or changing ones. Use RAG, tools, or MCP as the source of truth. |
| **Working Memory** | The context window is a hard edge. What goes in, and in what order, is a design decision. |
| **Steerability** | Follows concrete instructions well. Drifts on abstract ones. Restate the goal alongside the instruction. |
| **Non-determinism** | Same input, different outputs. You cannot certify behavior observed only once. |
| **Confidence is not validity** | Wrong answers sound just as fluent as right ones. Verification is architectural, not optional. |
| **A demo is not evidence** | Five clean runs do not prove determinism. The properties are always present. |

### Exam Traps

Cover the third column and quiz yourself.

| If you see... | The trap | The right call |
|---------------|----------|----------------|
| "The model hallucinated, so it's unreliable" | Blaming the model | The architect failed to design around next-token prediction. The missing mitigation is the bug, not the property. |
| `400 invalid_request_error` vs `model_context_window_exceeded` | Treating them as the same failure | `400` rejects before generation (prompt too large). `context_window_exceeded` truncates mid-response (output hit the ceiling). |
| "Same input gave different output, the model is random" | Confusing non-determinism with randomness | Non-determinism means variable outputs across runs. The response is evaluation frameworks, not retrying for the "right" answer. |
| A system fails. Which property was ignored? | Picking the wrong property | Know the pairings: Next-Token Prediction = Non-determinism, Knowledge = Knowledge Boundaries, Working Memory = Finite Context, Steerability = Confidence is Not Validity. |
| "The output was confident but wrong. Add more RAG." | Treating it as a Knowledge problem | Confidence is not validity is a Steerability consequence. The answer is human-in-the-loop and verification, not more retrieval. |
