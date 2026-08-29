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

**Related concepts:** [[what-is-mcp]] (why this handoff exists),
[[mxn-problem]] (a different, complementary argument for MCP).

**Practice exercise:** Not yet — will pair with the hands-on server-building
in Module 2.

**Retention status:** Developing — taught in two chunks; first chunk
(ListTools request/result direction) tested successfully, including an
unprompted correct detail that the app server doesn't talk to the MCP
server directly but goes through the MCP client. Second chunk (full 15-step
sequence) taught but not yet retrieval-tested.

**Last reviewed:** 2026-08-29 (taught; partial retrieval test on chunk 1)
**Next review:** 2026-08-30
