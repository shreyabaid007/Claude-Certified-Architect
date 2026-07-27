# Model Context Protocol

MCP is a communication layer that gives Claude access to external tools, data, and prompts without you writing all the integration code. It shifts the burden of tool definitions and execution from your application to specialized **MCP servers**.

```mermaid
flowchart LR
    A["<b>Your App</b><br/>(MCP Client)"] --> B["<b>MCP Server</b><br/>Tools, Resources, Prompts"]
    B --> C["<b>External Service</b><br/>GitHub, AWS, DB, etc."]
```

---

## Why MCP Exists

Without MCP, building a chatbot that accesses GitHub means writing every tool yourself: schemas, functions, error handling, and maintenance for every endpoint you need.

```mermaid
flowchart TD
    subgraph WITHOUT ["Without MCP"]
        A1["<b>Your Server</b>"] --> B1["list_repos()"]
        A1 --> B2["get_pull_requests()"]
        A1 --> B3["create_issue()"]
        A1 --> B4["get_commit_history()"]
        A1 --> B5["merge_pr()"]
        A1 --> B6["...dozens more"]
    end
```

GitHub has massive functionality: repositories, pull requests, issues, projects, branches, reviews. Each tool requires both a schema definition and a function implementation. That is a lot of code to write, test, and maintain.

![Without MCP: all tools authored by you](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748542646%2F09_-_001_-_Introducing_MCP_05.1748542646307.jpg)

MCP flips this. Someone else authors and hosts the tools. You just connect.

```mermaid
flowchart LR
    subgraph YOUR_APP ["Your App"]
        A["<b>MCP Client</b>"]
    end
    subgraph MCP ["MCP Server (GitHub)"]
        B1["list_repos()"]
        B2["get_pull_requests()"]
        B3["create_issue()"]
        B4["..."]
    end
    A --> B1
    A --> B2
    A --> B3
    A --> B4
```

![With MCP: tools live inside the MCP server](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748542646%2F09_-_001_-_Introducing_MCP_08.1748542646653.jpg)

> **The key:** MCP servers provide tool schemas and functions already defined for you. You consume them rather than build them.

---

## Common Misconceptions

| Question | Answer |
|---|---|
| **"Isn't MCP just tool use?"** | No. Tool use is the mechanism Claude uses to call functions. MCP is about who writes and hosts those functions. With MCP, someone else has done that work. |
| **"Who authors MCP servers?"** | Anyone. Service providers often release official implementations (e.g., AWS, GitHub, Stripe). |
| **"How is this different from calling APIs directly?"** | Direct API calls require you to author every schema and function. MCP gives you pre-built tools ready to use. |

---

## Architecture

Three components make up the MCP architecture:

```mermaid
flowchart LR
    subgraph CLIENT_SIDE ["Your Application"]
        A["<b>Your Server</b><br/>(application logic)"]
        B["<b>MCP Client</b><br/>(communication bridge)"]
    end
    subgraph SERVER_SIDE ["MCP Server"]
        C["<b>Tools</b>"]
        D["<b>Resources</b>"]
        E["<b>Prompts</b>"]
    end
    F["<b>External Service</b><br/>(GitHub, DB, etc.)"]

    A <--> B
    B <--> C
    B <--> D
    B <--> E
    C --> F
```

| Component | Role |
|---|---|
| **Your Server** | Application logic: receives user input, calls Claude, returns responses |
| **MCP Client** | Communication bridge between your server and MCP servers. Handles message passing and protocol details |
| **MCP Server** | Exposes tools, resources, and prompts. Wraps external service functionality |

> **Rule of thumb:** in real projects, you build either a client or a server, not both. You build a server to expose your service. You build a client to consume someone else's.

---

## Transport: How Client and Server Talk

MCP is **transport agnostic**. The client and server can communicate through different methods.

| Transport | When to use |
|---|---|
| **stdio** (standard I/O) | Client and server on the same machine. Most common for local development |
| **HTTP** | Client and server on different machines |
| **WebSockets** | Real-time, persistent connections |

![Transport options: stdio, HTTP, WebSockets](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748542645%2F09_-_002_-_MCP_Clients_03.1748542645442.jpg)

---

## Message Types

Once connected, the client and server exchange specific message types defined in the MCP specification.

```mermaid
sequenceDiagram
    participant C as MCP Client
    participant S as MCP Server

    Note over C,S: Discovery
    C->>S: ListToolsRequest
    S->>C: ListToolsResult (available tools)

    Note over C,S: Execution
    C->>S: CallToolRequest (tool name + args)
    S->>C: CallToolResult (tool output)
```

| Message | Direction | Purpose |
|---|---|---|
| **ListToolsRequest** | Client to Server | "What tools do you provide?" |
| **ListToolsResult** | Server to Client | List of available tool schemas |
| **CallToolRequest** | Client to Server | "Run this tool with these arguments" |
| **CallToolResult** | Server to Client | The tool's output |

![Message types between client and server](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748542645%2F09_-_002_-_MCP_Clients_04.1748542645814.jpg)

---

## Complete Flow: End to End

Here is the full communication flow when a user asks "What repositories do I have?"

```mermaid
sequenceDiagram
    participant U as User
    participant S as Your Server
    participant MC as MCP Client
    participant MS as MCP Server
    participant GH as GitHub API
    participant C as Claude API

    U->>S: "What repos do I have?"
    S->>MC: list_tools()
    MC->>MS: ListToolsRequest
    MS->>MC: ListToolsResult
    MC->>S: tool schemas

    S->>C: User message + tool schemas
    C->>S: ToolUse: list_repos()

    S->>MC: call_tool("list_repos", {})
    MC->>MS: CallToolRequest
    MS->>GH: GET /user/repos
    GH->>MS: repo data
    MS->>MC: CallToolResult
    MC->>S: tool result

    S->>C: Tool result
    C->>S: Final text response
    S->>U: "You have 5 repositories..."
```

> **Tip:** your server never talks to GitHub directly. The MCP server handles that. Your server only talks to the MCP client and Claude.

![Complete MCP flow with all participants](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748542651%2F09_-_002_-_MCP_Clients_18.1748542650970.jpg)

---

## Project: CLI Document Chatbot

The hands-on project builds a CLI chatbot with two components: an MCP client handling user interactions and a custom MCP server managing document operations.

```mermaid
flowchart LR
    A["<b>User</b><br/>CLI input"] --> B["<b>main.py</b><br/>Application logic"]
    B --> C["<b>MCP Client</b><br/>mcp_client.py"]
    C --> D["<b>MCP Server</b><br/>mcp_server.py"]
    D --> E["<b>In-Memory Docs</b><br/>dict of documents"]
    B --> F["<b>Claude API</b>"]
```

The server provides two tools (read and edit documents), two resources (list and fetch documents), and a formatting prompt. All documents are stored in a Python dictionary for simplicity.

```
┌──────────────────────────────────────────────────────┐
│  Project Structure                                   │
├──────────────────────────────────────────────────────┤
│  main.py          → entry point, wires everything    │
│  mcp_client.py    → MCPClient class                  │
│  mcp_server.py    → FastMCP server + tools           │
│  core/            → CLI app, Claude service, chat    │
│  .env             → API key + model config           │
└──────────────────────────────────────────────────────┘
```

---

## Defining Tools with the Python SDK

The MCP Python SDK turns tool creation from verbose JSON schemas into decorated Python functions.

```mermaid
flowchart LR
    A["<b>@mcp.tool</b><br/>decorator"] --> B["<b>Python function</b><br/>with type hints"]
    B --> C["<b>Auto-generated</b><br/>JSON schema"]
```

### Read Tool

```python
from mcp.server.fastmcp import FastMCP
from pydantic import Field

mcp = FastMCP("DocumentMCP", log_level="ERROR")

docs = {
    "deposition.md": "This deposition covers the testimony of Angela Smith, P.E.",
    "report.pdf": "The report details the state of a 20m condenser tower.",
    "financials.docx": "These financials outline the project's budget and expenditures.",
}

@mcp.tool(
    name="read_doc_contents",
    description="Read the contents of a document and return it as a string.",
)
def read_document(
    doc_id: str = Field(description="Id of the document to read"),
):
    if doc_id not in docs:
        raise ValueError(f"Doc with id {doc_id} not found")
    return docs[doc_id]
```

### Edit Tool

```python
@mcp.tool(
    name="edit_document",
    description="Edit a document by replacing a string in the documents content with a new string",
)
def edit_document(
    doc_id: str = Field(description="Id of the document that will be edited"),
    old_str: str = Field(description="The text to replace. Must match exactly, including whitespace"),
    new_str: str = Field(description="The new text to insert in place of the old text"),
):
    if doc_id not in docs:
        raise ValueError(f"Doc with id {doc_id} not found")
    docs[doc_id] = docs[doc_id].replace(old_str, new_str)
```

| SDK Feature | Benefit |
|---|---|
| **`@mcp.tool` decorator** | Registers the function as a tool and auto-generates the JSON schema |
| **`Field()` from Pydantic** | Adds parameter descriptions that help Claude understand what each argument expects |
| **Type hints** | Drive automatic schema generation and validation |
| **Error handling** | `ValueError` messages are returned to Claude, which can self-correct |

> **The key:** you write a normal Python function. The SDK handles the protocol. Compare this to the manual `ToolParam` approach from the tool use module.

---

## The Server Inspector

The MCP SDK includes a browser-based inspector for testing your server without connecting to a full application.

```bash
mcp dev mcp_server.py
```

This starts a dev server on port 6277. Open the URL in your browser.

![MCP Inspector dashboard](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748542727%2F09_-_005_-_The_Server_Inspector_05.1748542726831.jpg)

### Testing Workflow

```mermaid
flowchart LR
    A["<b>Connect</b><br/>to server"] --> B["<b>List Tools</b><br/>see available tools"]
    B --> C["<b>Select a Tool</b><br/>fill parameters"]
    C --> D["<b>Run Tool</b><br/>see results"]
    D --> E["<b>Verify</b><br/>chain operations"]
```

| Step | What you do |
|---|---|
| **Connect** | Click Connect to start the MCP server |
| **List Tools** | See all tools, resources, and prompts |
| **Test** | Fill in parameters and run individual tools |
| **Verify** | Chain operations (edit then read) to confirm behavior |

![Inspector showing tool test results](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748542728%2F09_-_005_-_The_Server_Inspector_17.1748542728249.jpg)

> **Tip:** the inspector is actively developed, so the UI may look different from these screenshots. The core testing functionality stays the same.

---

## Implementing the Client

The MCP client consists of two layers: a `ClientSession` (from the SDK) that manages the connection, and your `MCPClient` wrapper that provides a clean interface.

```mermaid
flowchart TD
    A["<b>Your Application</b><br/>main.py"] --> B["<b>MCPClient</b><br/>your wrapper class"]
    B --> C["<b>ClientSession</b><br/>SDK connection"]
    C --> D["<b>MCP Server</b><br/>via stdio transport"]
```

### Core Methods

Your client needs two methods to power the tool-use loop:

```python
from mcp import ClientSession, StdioServerParameters, types
from mcp.client.stdio import stdio_client

class MCPClient:
    async def list_tools(self) -> list[types.Tool]:
        result = await self.session().list_tools()
        return result.tools

    async def call_tool(
        self, tool_name: str, tool_input: dict
    ) -> types.CallToolResult | None:
        return await self.session().call_tool(tool_name, tool_input)
```

The `MCPClient` class uses `AsyncExitStack` for resource cleanup. When used as an async context manager, it connects on entry and cleans up on exit:

```python
async with MCPClient(command="uv", args=["run", "mcp_server.py"]) as client:
    tools = await client.list_tools()
    print(tools)  # [Tool(name="read_doc_contents", ...), Tool(name="edit_document", ...)]
```

```
┌──────────────────────────────────────────────────────┐
│  MCPClient Interface                                 │
├──────────────────────────────────────────────────────┤
│  list_tools()      → returns all tool schemas        │
│  call_tool()       → executes a tool by name         │
│  list_prompts()    → returns all prompt definitions   │
│  get_prompt()      → returns messages for a prompt   │
│  read_resource()   → fetches resource data by URI    │
│  cleanup()         → closes session and transport    │
└──────────────────────────────────────────────────────┘
```

---

## Defining Resources

Resources expose data from your MCP server, similar to GET endpoints in an HTTP API. Use them when you need to fetch information rather than perform actions.

```mermaid
flowchart LR
    A["<b>MCP Client</b>"] -->|ReadResourceRequest| B["<b>MCP Server</b>"]
    B -->|Resource Data| A
    B --> C["<b>Direct Resource</b><br/>docs://documents"]
    B --> D["<b>Templated Resource</b><br/>docs://documents/{doc_id}"]
```

### Two Types of Resources

| Type | URI Pattern | Use case |
|---|---|---|
| **Direct** | `docs://documents` | Static endpoints: list all items, get config |
| **Templated** | `docs://documents/{doc_id}` | Parameterized queries: fetch a specific item |

### Implementation

```python
@mcp.resource("docs://documents", mime_type="application/json")
def list_docs() -> list[str]:
    return list(docs.keys())

@mcp.resource("docs://documents/{doc_id}", mime_type="text/plain")
def fetch_doc(doc_id: str) -> str:
    if doc_id not in docs:
        raise ValueError(f"Doc with id {doc_id} not found")
    return docs[doc_id]
```

The SDK automatically parses `{doc_id}` from the URI and passes it as a keyword argument. The `mime_type` hints to clients how to parse the response.

![Resources vs Resource Templates in the inspector](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748542784%2F09_-_007_-_Defining_Resources_17.1748542783889.jpg)

### Accessing Resources from the Client

```python
import json
from pydantic import AnyUrl

async def read_resource(self, uri: str) -> Any:
    result = await self.session().read_resource(AnyUrl(uri))
    resource = result.contents[0]

    if isinstance(resource, types.TextResourceContents):
        if resource.mimeType == "application/json":
            return json.loads(resource.text)
        return resource.text
```

The response `contents` list contains the resource data plus metadata. Check the MIME type to determine how to parse it.

> **The key:** resources are fetched directly and injected into prompts. No tool call needed. This makes interactions faster when you know exactly what data you want.

### Tools vs Resources

| | Tools | Resources |
|---|---|---|
| **Purpose** | Perform actions, side effects | Fetch data, read-only |
| **Who decides to use them** | Claude (via tool use loop) | Your application code |
| **Analogy** | POST/PUT/DELETE endpoints | GET endpoints |
| **Example** | `edit_document()` | `docs://documents/{id}` |

---

## Defining Prompts

Prompts are pre-built, high-quality instruction templates defined on the MCP server. They give better results than ad-hoc user input because they are carefully crafted and tested.

```mermaid
flowchart LR
    A["<b>User triggers</b><br/>a prompt command"] --> B["<b>MCP Server</b><br/>returns messages"]
    B --> C["<b>Claude</b><br/>follows the prompt"]
    C --> D["<b>Tools</b><br/>executes actions"]
```

### Implementation

```python
from mcp.server.fastmcp.prompts import base

@mcp.prompt(
    name="format",
    description="Rewrites the contents of the document in Markdown format.",
)
def format_document(
    doc_id: str = Field(description="Id of the document to format"),
) -> list[base.Message]:
    prompt = f"""
    Your goal is to reformat a document to be written with markdown syntax.

    The id of the document you need to reformat is:
    <document_id>
    {doc_id}
    </document_id>

    Add in headers, bullet points, tables, etc as necessary.
    Use the 'edit_document' tool to edit the document.
    After the document has been edited, respond with the final version.
    """
    return [base.UserMessage(prompt)]
```

The `@mcp.prompt` decorator registers the function. Arguments are passed as keyword arguments when the client requests the prompt.

### Accessing Prompts from the Client

```python
async def list_prompts(self) -> list[types.Prompt]:
    result = await self.session().list_prompts()
    return result.prompts

async def get_prompt(self, prompt_name, args: dict[str, str]):
    result = await self.session().get_prompt(prompt_name, args)
    return result.messages
```

When a user selects a prompt (e.g., `/format`), the system:

```mermaid
flowchart LR
    A["<b>User selects</b><br/>/format"] --> B["<b>Pick document</b><br/>doc_id argument"]
    B --> C["<b>get_prompt()</b><br/>interpolated messages"]
    C --> D["<b>Send to Claude</b><br/>with available tools"]
    D --> E["<b>Claude formats</b><br/>using edit_document"]
```

![Prompt workflow in the CLI](https://everpath-course-content.s3-accelerate.amazonaws.com/instructor%2Fa46l9irobhg0f5webscixp0bs%2Fpublic%2F1748542820%2F09_-_010_-_Prompts_in_the_Client_15.1748542820224.jpg)

> **Rule of thumb:** prompts should represent your domain expertise. They are pre-tested, carefully worded instructions that produce better results than what users would write on their own.

---

## The Three Primitives

MCP servers expose three types of capabilities. Each serves a different purpose in the communication flow.

```mermaid
flowchart TD
    A["<b>MCP Server</b>"] --> B["<b>Tools</b><br/>Actions Claude can invoke"]
    A --> C["<b>Resources</b><br/>Data your app can fetch"]
    A --> D["<b>Prompts</b><br/>Pre-built instructions"]

    style B fill:#d4edda,stroke:#28a745,color:#000
    style C fill:#fff3cd,stroke:#ffc107,color:#000
    style D fill:#d6eaf8,stroke:#2e86c1,color:#000
```

| Primitive | Who uses it | How it is accessed | Example |
|---|---|---|---|
| **Tools** | Claude decides to call them | Via the tool-use loop | `read_doc_contents`, `edit_document` |
| **Resources** | Your app fetches them directly | `read_resource(uri)` | `docs://documents`, `docs://documents/{id}` |
| **Prompts** | User selects them as commands | `get_prompt(name, args)` | `/format` with `doc_id` argument |

---

## Running the Server

Add this at the bottom of your `mcp_server.py` to make it runnable:

```python
if __name__ == "__main__":
    mcp.run(transport="stdio")
```

The `transport="stdio"` tells the server to communicate over standard input/output, which is how the client connects when both run on the same machine.

---

## Quick Revision

```mermaid
flowchart TD
    A["<b>MCP</b>"] --> B["<b>Server</b><br/>Hosts tools, resources, prompts"]
    A --> C["<b>Client</b><br/>Bridge to servers"]
    A --> D["<b>Transport</b><br/>stdio, HTTP, WebSockets"]
    B --> E["<b>Tools</b><br/>@mcp.tool decorator"]
    B --> F["<b>Resources</b><br/>@mcp.resource decorator"]
    B --> G["<b>Prompts</b><br/>@mcp.prompt decorator"]
    C --> H["<b>list_tools / call_tool</b>"]
    C --> I["<b>read_resource</b>"]
    C --> J["<b>get_prompt</b>"]
    E --> K["<b>Inspector</b><br/>mcp dev server.py"]
```

| Concept | One-line summary |
|---|---|
| **MCP** | Communication layer that shifts tool definitions and execution to specialized servers |
| **MCP Server** | Hosts tools, resources, and prompts that wrap external service functionality |
| **MCP Client** | Communication bridge between your application and MCP servers |
| **Transport** | How client and server talk: stdio (local), HTTP, or WebSockets |
| **Tools** | Decorated Python functions that Claude can invoke via the tool-use loop |
| **Resources** | Data endpoints (direct or templated) your app fetches directly into prompts |
| **Prompts** | Pre-built instruction templates that produce better results than ad-hoc input |
| **FastMCP** | Python SDK class that auto-generates JSON schemas from type hints and decorators |
| **Field()** | Pydantic helper that adds parameter descriptions for Claude |
| **Inspector** | Browser-based tool (`mcp dev`) for testing your server without a full application |
| **ListToolsRequest** | Client asks server what tools are available |
| **CallToolRequest** | Client asks server to execute a specific tool with arguments |
| **MCPClient wrapper** | Your class around `ClientSession` that handles connection lifecycle and cleanup |
