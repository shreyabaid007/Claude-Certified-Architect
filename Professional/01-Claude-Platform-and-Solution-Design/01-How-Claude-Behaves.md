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

```
┌────────────────────────────────────────────────────────────┐
│  NEXT-TOKEN PREDICTION                                     │
├──────────────┬─────────────────────────────────────────────┤
│  Capability  │  Summarizing, reformatting, explaining      │
│              │  well-established concepts. Tasks built     │
│              │  on common patterns.                        │
├──────────────┼─────────────────────────────────────────────┤
│  Limitation  │  Anything requiring precision on specifics. │
│              │  Can produce text that appears accurate     │
│              │  but isn't. Risk concentrates around        │
│              │  names, dates, citations, and statistics.   │
├──────────────┼─────────────────────────────────────────────┤
│  Mitigation  │  Citations, uncertainty signaling, and      │
│              │  generator-verifier loops. Route factual    │
│              │  lookups through tool calls or              │
│              │  authoritative sources.                     │
└──────────────┴─────────────────────────────────────────────┘
```

---

## Property 2: Knowledge

```
┌────────────────────────────────────────────────────────────┐
│  KNOWLEDGE                                                 │
├──────────────┬─────────────────────────────────────────────┤
│  Capability  │  Topics that are common, recent, and        │
│              │  consistently represented in training data. │
├──────────────┼─────────────────────────────────────────────┤
│  Limitation  │  Topics that are rare, niche, contested,    │
│              │  or frequently changing. Stale or           │
│              │  incomplete information presented with      │
│              │  the same confident tone.                   │
├──────────────┼─────────────────────────────────────────────┤
│  Mitigation  │  Web search, RAG, tool use, or MCP servers  │
│              │  to make an external system the source of   │
│              │  truth. Re-introduce the data yourself      │
│              │  rather than relying on training data.      │
└──────────────┴─────────────────────────────────────────────┘
```

---

## Property 3: Working Memory

```
┌────────────────────────────────────────────────────────────┐
│  WORKING MEMORY                                            │
├──────────────┬─────────────────────────────────────────────┤
│  Capability  │  Anything that fits in the active context   │
│              │  window.                                    │
├──────────────┼─────────────────────────────────────────────┤
│  Limitation  │  The context window is a hard edge. Once    │
│              │  content falls outside, the model has no    │
│              │  access to it at all.                       │
├──────────────┼─────────────────────────────────────────────┤
│  Mitigation  │  Progressive context loading, chunking,     │
│              │  front-loading critical information.        │
│              │  Summarize across turns when context        │
│              │  is getting long.                           │
└──────────────┴─────────────────────────────────────────────┘
```

Two distinct errors happen at the context window edge:

| Error | When it happens | What you see |
|-------|-----------------|--------------|
| **Oversized request** | Prompt is too large to send | `400 invalid_request_error` (token limit) or `413 request_too_large` (byte limit). Rejected before generation. |
| **Truncated output** | Prompt fits, but generation hits the window ceiling | `model_context_window_exceeded` stop reason. Output cuts off mid-response. |

> **Tip:** Check the `usage` field on every response and use the token-counting API before you send to avoid hitting either limit.

---

## Property 4: Steerability

```
┌────────────────────────────────────────────────────────────┐
│  STEERABILITY                                              │
├──────────────┬─────────────────────────────────────────────┤
│  Capability  │  Short, concrete, verifiable instructions   │
│              │  with defined formats, explicit length      │
│              │  limits, and clear roles.                   │
├──────────────┼─────────────────────────────────────────────┤
│  Limitation  │  Abstract or ambiguous instructions, long   │
│              │  reasoning chains, tasks requiring precise  │
│              │  numerical or logical computation. May      │
│              │  follow the letter while drifting from      │
│              │  intent.                                    │
├──────────────┼─────────────────────────────────────────────┤
│  Mitigation  │  System prompts, structured outputs, code   │
│              │  execution for logical precision. Restate   │
│              │  the goal alongside the instruction when    │
│              │  intent and literal instruction might       │
│              │  diverge.                                   │
└──────────────┴─────────────────────────────────────────────┘
```

---

## From Property to Design Consequence

Each property maps to a design consequence you will use later in the course.

```mermaid
flowchart LR
    P1["<b>Next-Token<br/>Prediction</b>"]
    P2["<b>Knowledge</b>"]
    P3["<b>Working<br/>Memory</b>"]
    P4["<b>Steerability</b>"]

    D1["<b>Non-determinism</b><br/>Same input, different outputs.<br/>You cannot certify behavior<br/>you only observed once."]
    D2["<b>Knowledge &<br/>Capability Boundaries</b><br/>Reliable on common topics.<br/>Unreliable on rare or<br/>fast-changing ones."]
    D3["<b>Context as a<br/>Finite Resource</b><br/>What you put in, the order,<br/>and what you leave out<br/>are design decisions."]
    D4["<b>Confidence Is<br/>Not Validity</b><br/>Wrong answers arrive in<br/>the same fluent tone<br/>as right ones."]

    P1 --> D1
    P2 --> D2
    P3 --> D3
    P4 --> D4

    D1 -. "Feeds" .-> E1["Evaluation frameworks<br/><i>Module 2</i>"]
    D2 -. "Feeds" .-> E2["Reference architectures<br/>& RAG<br/><i>Later in Module 1</i>"]
    D3 -. "Feeds" .-> E3["Model & context<br/>strategy<br/><i>Later in Module 1</i>"]
    D4 -. "Feeds" .-> E4["Human-in-the-loop<br/>& verification<br/><i>Module 3</i>"]

    style D1 fill:#fff3cd,stroke:#ffc107,color:#000
    style D2 fill:#fff3cd,stroke:#ffc107,color:#000
    style D3 fill:#fff3cd,stroke:#ffc107,color:#000
    style D4 fill:#fff3cd,stroke:#ffc107,color:#000
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
