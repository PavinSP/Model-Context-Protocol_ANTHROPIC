# Concept: The Three MCP Server Components — Tools, Resources, Prompts

**Definition:** Every MCP server exposes its functionality through three
kinds of components: tools, resources, and prompts. Each has a distinct
job.

**Why this matters:** This gap was surfaced by an independent Coursera
dialogue (see lessons/2026-08-29-session-03-dialogue-integration-challenges.md)
— resources and prompts had only been named in passing before this, never
actually taught, even though the Module 1 dialogue/quiz already probes for
them (full deep-dive is officially in Module 3).

**The three components:**

- **Tools** — functions the model can CALL to take an action or compute/
  fetch something based on input arguments (e.g. `search_repos(query="mcp")`,
  `list_repos()`). The model decides when to invoke these. Key trait: the
  server runs code/logic in response to arguments you supply.
- **Resources** — data the server makes AVAILABLE to the client, addressed
  more like a file/URI than a function call. You don't "call" a resource,
  you access/read it. Key trait: it's a piece of data that already exists;
  no computation or arguments needed to produce it.
- **Prompts** — pre-written, reusable instruction templates the server
  offers to help the model do something well (e.g. a "summarize this PR"
  template). These are tuned directions for the model, not raw data or an
  action.

**Distinguishing test:** For any given piece of server functionality, ask:
"Is this a THING I DO (tool — runs code/logic based on input), a THING I
READ (resource — just exposes existing data), or a THING THAT SHAPES HOW
THE MODEL IS INSTRUCTED (prompt — a template, not data or action)?"

**Mistake logged (2026-08-29):** When asked whether "the contents of
README.md from a repo" would be a tool, resource, or prompt, learner
initially answered "tool." Correct answer is **resource** — the README's
content is static/existing data being exposed, not a computation being
performed. Learner self-corrected after a second, sharper framing of the
distinguishing question ("server runs code based on input" vs. "server
just hands me existing data") and answered correctly and clearly on retry.

**Related concepts:** [[what-is-mcp]] (introduced "tools" first, before
resources/prompts existed as taught concepts), [[mcp-clients]]
(ListToolsRequest/CallToolRequest apply specifically to tools — resources
and prompts will have their own request/result message types, covered in
Module 3).

**Practice exercise:** None yet — full mechanics (how a client
lists/accesses resources, how prompts are selected/used) are covered in
Module 3 ("Defining Resources," "Defining Prompts").

**Retention status:** Developing (~3/6). Two distinguishing examples
tested: (1) README.md contents — initial answer wrong (called it a tool),
corrected successfully on retry. (2) A "generate a commit message for this
diff" instruction template — correctly identified as a prompt, though
initial phrasing said it instructs "the server" rather than "the model";
corrected — the server just stores/hands out the template, the instructions
inside are aimed at whatever model ends up using it. All three components
(tools, resources, prompts) have now been correctly distinguished at least
once. Needs an un-hinted, mixed-up review (not in teaching order) to
confirm before calling this Strong.

**Last reviewed:** 2026-08-29 (taught + two retrieval tests, both with one
correction each)
**Next review:** 2026-08-30
