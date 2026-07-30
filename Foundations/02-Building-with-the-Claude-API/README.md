# Building with the Claude API

The full spectrum of working with Anthropic models using the Claude API. Eight notes, running from a first authenticated request through to agents that decide their own next step.

**Status:** Complete

---

## Notes in This Module

| Notes | Covers |
|---|---|
| [01-Accessing-and-Making-Requests](01-Accessing-and-Making-Requests.md) | SDK setup and authentication, the message structure, model naming, and the request parameters that shape a response |
| [02-Prompt-Evaluation](02-Prompt-Evaluation.md) | Prompt engineering versus prompt evaluation, the three paths after writing a prompt, the five-step evaluation workflow, and a complete eval pipeline built end to end |
| [03-Prompt-Engineering](03-Prompt-Engineering.md) | The iterative improvement loop against an eval pipeline, the baseline prompt, and the four techniques: be clear and direct, be specific with guidelines, XML tags for structure, few-shot examples |
| [04-Tool-Use](04-Tool-Use.md) | The tool use loop, writing tool functions and schemas, handling multi-block responses, returning tool results, multi-turn tool conversations, fine-grained tool calling, and the built-in tools |
| [05-Retrieval-Augmented-Generation](05-Retrieval-Augmented-Generation.md) | Why not to include everything, the RAG pipeline stage by stage, chunking, text embeddings, vector databases, cosine similarity search, hybrid semantic and lexical search, and multi-index pipelines |
| [06-Claude-Features](06-Claude-Features.md) | Extended thinking, image support, PDF support, citations, prompt caching, and code execution with the Files API |
| [07-Model-Context-Protocol](07-Model-Context-Protocol.md) | What MCP actually is, the client-server architecture, the three primitives, message types, and building both a server and a client against a running example |
| [08-Agents-and-Workflows](08-Agents-and-Workflows.md) | The four workflow patterns (chaining, parallelization, routing, evaluator-optimizer), combining them, what makes something an agent, and environment inspection |

---

[Back to Foundations](../README.md) · [Back to the study guide](../../README.md)
