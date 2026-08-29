# Concept: The M×N Integration Problem

**Definition:** Without a shared protocol, connecting M AI applications to N
tools/data sources requires building M×N custom integrations — one adapter
per (AI app, tool) pair.

**Why it exists / problem it solves:** Each tool (Gmail, GitHub, a database,
a weather API, etc.) has its own auth method, request/response schema, and
capabilities. For an AI model to use a tool, something has to translate that
tool's capabilities into a form the model can read (e.g. a function/tool
schema) and translate the model's calls back into real API requests. Without
a standard, every AI application that wants to support every tool must
hand-write this translation layer itself.

**Mechanism:**
- M = number of AI applications (ChatGPT, Claude Desktop, a custom agent, an
  IDE assistant, ...)
- N = number of tools/data sources (Gmail, GitHub, a weather API, a
  database, ...)
- Naively: M × N custom integrations, each needing to handle auth, schema
  translation, and result parsing.
- Adding one new tool means every AI app needs a new adapter for it. Adding
  one new AI app means it needs adapters for every tool it wants to support.
- This is the same shape as the classic pre-USB problem: every device
  needed its own cable/driver for every computer, until USB standardized the
  interface.

**Mental model:** MCP is being introduced (per the course) as a way to
collapse M×N integrations into M + N — each tool builds ONE MCP server, each
AI app builds ONE MCP client, and any client can talk to any server through
the same protocol. (This is the hypothesis to verify as the course
continues — not yet confirmed by course material beyond the intro framing.)

**Non-example:** A single hardcoded integration (e.g. one chatbot with one
custom Gmail plugin) is not the M×N problem — the problem only shows up at
scale, when you have multiple apps and/or multiple tools.

**Related concepts:** API function calling, tool/function schemas,
client-server architecture. [[api-function-calling]] (link to be created
once that concept is formally captured).

**Previously learned in:** Prior general knowledge of APIs, referenced
during retrieval practice on 2026-08-29 (not part of a Coursera course
inside this repo).

**Practice exercise:** None yet — to be added once MCP's actual client/server
mechanism is covered (Module 1 videos).

**Retention status:** Developing — introduced via retrieval practice, not
yet tested from memory in a later session.

**Last reviewed:** 2026-08-29 (initial introduction)
**Next review:** 2026-08-30 (next day, per spaced repetition schedule)
