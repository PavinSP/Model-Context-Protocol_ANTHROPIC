# Session Log — 2026-08-29 (Session 3)

## Context

Learner completed the Coursera "Connecting Integration Challenges to MCP"
dialogue (Module 1, 15 min) independently, then pasted the full transcript
including their own answers and Coursera's built-in feedback. This is
independent, external evidence of retention — not scaffolded by this
session's own questions.

## What happened

Coursera's dialogue tested exactly the material taught in sessions 1-2
(M×N problem, MCP as labor-shifting middleman, client-server message
types) plus asked about MCP server components (tools/resources/prompts) —
which had only been *named in passing* so far, never actually taught.

### Strengths confirmed by Coursera's own feedback

- **M×N problem**: Learner reproduced the exact framing and numeric example
  (2 agents × 5→6 tools = 10→12 vs M+N = 7→8) completely unprompted, in an
  independent assessment context. This is strong external confirmation of
  [[mxn-problem]] retention — upgrading confidence further.
- **MCP as middleman / labor-shifting**: Correctly explained that the
  user's server only talks to the MCP client/server, and that adding a new
  tool costs one integration regardless of how many AI models use it.
  Confirms [[what-is-mcp]] retention, specifically the "adding a tool is
  cheap" consequence of M+N.
- **Message types**: Correctly identified ListToolsRequest and
  CallToolRequest as the client→server request types. Confirms
  [[mcp-clients]] retention on message types specifically (the fuller
  15-step sequence wasn't tested here, but the message vocabulary was).

### Gap exposed (real, not yet covered in our teaching)

When asked for the three components of an MCP server, learner answered
"tools, prompts, and requests" — conflating a **message type** (requests:
ListToolsRequest/CallToolRequest, which are exchanged BETWEEN client and
server) with an actual **server-side component** (which would be
resources). Needed a hint from Coursera's dialogue to arrive at
"resources" as the third component.

**This is not really a "mistake" in the misconception sense** — resources
and prompts have only ever been *mentioned by name* in our sessions
(originally spotted in the "Welcome to the course" roadmap and referenced
in [[what-is-mcp]]'s definition), never actually taught. So this gap is
expected and simply marks the next thing to teach, not a retention failure.

## Concepts touched

- [[mxn-problem]] — confirmed Strong via independent assessment
- [[what-is-mcp]] — confirmed via independent assessment (middleman +
  cheap-tool-addition framing)
- [[mcp-clients]] — confirmed on message-type vocabulary specifically
- **Resources** and **Prompts** (MCP server components) — identified as
  NOT YET TAUGHT. Need dedicated concept coverage before the "MCP Clients
  Quiz" (graded, due 2026-08-31).

## Mistakes / misconceptions logged

None new — the tools/prompts/requests mixup is a coverage gap, not a
misconception, since resources/prompts were never actually taught.

## Next step

1. Teach **resources** and **prompts** as MCP server components — this is
   the single highest-priority gap before the graded MCP Clients Quiz
   (due 2026-08-31, ~2 days out).
2. Check the course syllabus/module map — resources and prompts are
   explicitly covered in Module 3 ("Connecting with MCP clients": Defining
   Resources, Defining Prompts). Flag: the graded MCP Clients Quiz is in
   MODULE 1, but resources/prompts aren't formally taught until MODULE 3.
   Need to verify with the user whether the Module 1 quiz actually expects
   resources/prompts knowledge, or just tools + client/server basics — the
   Coursera dialogue asking about all three components suggests at least
   surface-level awareness is expected earlier than the deep-dive module.
3. Continue toward the MCP Clients Quiz (due 2026-08-31) and "Explaining
   Client–Server Communication" practice assignment, remaining Module 1
   items.
