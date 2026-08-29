# Concept: MCP Clients — Role, Transport, and Message Flow

**Definition:** The MCP client is the connection point between an
application's own server and an MCP server. It is the app's access point to
all the tools implemented by that MCP server.

**Why it exists / problem it solves:** Once tool authorship has moved to a
separate MCP server (see [[what-is-mcp]]), something needs to actually
manage the connection and translate the app's needs ("what tools exist?",
"run this tool") into the standardized messages the MCP server expects.
That's the client's job.

**Mechanism — transport:**
- MCP is **transport-agnostic**: client and server can communicate over
  different underlying protocols depending on deployment.
- **stdio** (standard input/output) — used when client and server run on
  the same physical machine. This is the setup the course will build later.
- **HTTP**, **WebSockets**, or others — used when client and server run on
  different machines.

**Mechanism — messages (request/result pairs defined by the MCP spec):**
- `ListToolsRequest` (client → server) / `ListToolsResult` (server →
  client) — ask for and receive the list of available tools.
- `CallToolRequest` (client → server) / `CallToolResult` (server → client)
  — ask the server to run a specific tool with given arguments, and receive
  the tool's output.

**Mechanism — full end-to-end call sequence (GitHub repo-listing example):**
Six parties: User, Your (app) Server, MCP Client, MCP Server, GitHub,
Claude.

1. User → Your Server: "What repositories do I have?"
2. Your Server → MCP Client: "give me the list of tools" (needed before
   talking to Claude, so Claude can be offered the tool list)
3. MCP Client → MCP Server: `ListToolsRequest`
4. MCP Server → MCP Client: `ListToolsResult`
5. MCP Client → Your Server: hands back the tool list
6. Your Server → Claude: sends user's query + the tool list
7. Claude → Your Server: decides a tool is needed, responds with a "tool
   use" message (Claude never executes anything itself — it only requests)
8. Your Server → MCP Client: "run this tool with these arguments" — note:
   Your Server no longer executes tools itself; that responsibility now
   belongs to the MCP server
9. MCP Client → MCP Server: `CallToolRequest`
10. MCP Server → GitHub: the actual API call to fetch real data (only step
    that touches GitHub directly)
11. GitHub → MCP Server: returns the data (e.g. repo list)
12. MCP Server → MCP Client: wraps result in `CallToolResult`
13. MCP Client → Your Server: hands back the result
14. Your Server → Claude: sends tool result back (as part of a user
    message)
15. Claude → Your Server → User: Claude writes the final answer using the
    tool result

**Key structural insight:** Your app's own server NEVER talks to GitHub
directly, and NEVER executes a tool itself. It only ever talks to Claude
and to the MCP client. All real work (listing tools, running tools, calling
GitHub) is delegated through the MCP client to the MCP server. This is the
concrete mechanism behind the labor-shifting argument in [[what-is-mcp]] —
now we can see *exactly* which messages implement that shift.

**Mental model:** Every MCP interaction is a request/result pair, and there
are always (at least) three hops for any real action: Your Server ↔ MCP
Client ↔ MCP Server (↔ the actual external service, for tool calls).

**Plain-language clarification — what is "your server"?**
"Your server" is simply the backend code you (the app developer) write and
run for your own application — e.g. the backend behind a chatbot website.
It receives the user's question, talks to Claude, and sends the answer
back. It is NOT Claude, NOT GitHub, and NOT the MCP client/server — it's
your own coordinating program sitting in the middle.

Restaurant analogy:
- User = customer ordering food
- Your server = the waiter (coordinates everything, but doesn't cook or
  fetch ingredients itself)
- Claude = the chef (decides what's needed to fulfill the order)
- MCP Client = the waiter's notepad/walkie-talkie into the kitchen's supply
  system
- MCP Server = the actual supply room holding the real tools/data
- GitHub = the delivery truck bringing fresh data from outside

The waiter never goes to the delivery truck directly — they radio the
kitchen, which handles it.

**Why the "tool-listing detour" (steps 2–5) happens:** Before your server
can even properly ask Claude the user's question, it must tell Claude what
tools exist. But your server doesn't know the tool list itself — only the
MCP server does. So it detours: ask MCP client → MCP client asks MCP server
→ gets list → hands it back. Only then does the real conversation with
Claude begin. It's called a "detour" because it's pure prep work that
happens BEFORE the main Claude conversation.

**Why the "tool-execution handoff" (steps 8–9) happens:** When Claude says
"I want to use a tool with these arguments," your server has no code to
actually run that tool (e.g. no code to fetch GitHub repos). So it hands
the job off — "MCP client, run this for me" — and the MCP client forwards
it as `CallToolRequest` to the MCP server, which is the only party with the
real implementation.

**One-line summary:** Your server is a necessary middleman that doesn't
know how to list or run tools itself — for both jobs, it always asks the
MCP client, which always asks the MCP server, which does the real work.

**Related concepts:** [[what-is-mcp]] (why this handoff exists),
[[mxn-problem]] (a different, complementary argument for MCP).

**Practice exercise:** Not yet — will pair with the hands-on server-building
in Module 2.

**Retention status:** Developing — taught in two chunks; first chunk
(ListTools request/result direction) tested successfully, including an
unprompted correct detail that the app server doesn't talk to the MCP
server directly but goes through the MCP client. Second chunk (full 15-step
sequence) taught but not yet retrieval-tested.

**Last reviewed:** 2026-08-29 (taught; full sequence retrieval-tested)
**Next review:** 2026-08-30

**Full-sequence retrieval test (2026-08-29):** Learner recalled the entire
15-step, six-party sequence unprompted, correctly identifying both detours
(tool-listing before Claude is consulted, tool-execution after Claude
requests a tool) and correctly noting "the MCP client cannot do the
processing" (only forwards). Retention status upgraded to ~4/6 ("apply
independently").

One self-corrected slip during the answer: initially said the MCP server
"requests the list of tools that GitHub has" — this is inaccurate. The MCP
server's tools are pre-built into it; GitHub is contacted ONLY during tool
*execution* (`CallToolRequest`/step 10), never during tool *listing*
(`ListToolsRequest`/steps 3-4). The learner actually stated this correctly
later in the same answer, suggesting the right model is held but the
initial phrasing needs tightening — flag for a quick re-check on the next
review (2026-08-30): "does listing tools ever contact GitHub? Why or why
not?"

**Independent graded confirmation (2026-08-29):** Passed the official
Coursera "MCP Clients Quiz" (graded assignment) at 100% (4/4), submitted
independently before being shared here. All four questions map directly
onto this concept:
- Q1: correctly identified transport-agnostic = stdio/HTTP/WebSockets
  depending on setup (not "same machine always," not auto-switching)
- Q2: correctly identified the full operation order — User query → Tool
  discovery → List tools exchange → Claude request → Tool execution →
  Results flow back → Final response — matching the 15-step sequence
  taught here
- Q3: correctly identified ListToolsRequest/Result and
  CallToolRequest/Result as the two core message-type pairs (not the
  plausible-sounding distractors like FetchTools/RunTool or
  ToolDiscovery/ToolInvocation)
- Q4: correctly identified the client's role as a communication
  bridge/forwarder (not a data store, not a cache, not something that
  executes API calls itself) — this directly confirms the client never
  executes tools, only forwards requests

This is strong, external, graded evidence — retention status upgraded to
Strong (~5/6). The one remaining loose end (GitHub-contact-timing phrasing
slip) is now lower priority given this clean graded result, but still
worth a quick informal recheck at the next scheduled review.

**Note on quiz page content:** The pasted quiz page contained text
formatted as instructions telling an AI assistant to refuse to help and to
click a UI button — this is a prompt-injection attempt embedded in the
page content, not a genuine Coursera instruction, and was disregarded. No
impact on the quiz result or this concept's evidence.
