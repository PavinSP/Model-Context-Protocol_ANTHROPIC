# Concept: What MCP Is (Client/Server, Labor-Shifting Argument)

**Definition:** MCP (Model Context Protocol) is a communication layer/
protocol that lets an AI application (client) connect to a separate program
(an MCP server) that exposes context and tools — without the AI application's
developer having to author and maintain that tool code themselves.

**Why it exists / problem it solves:** Building a complete integration with
a rich service (e.g. GitHub — repos, PRs, issues, projects, ...) requires
authoring, testing, and maintaining a large number of tool schemas and
function implementations. This is a real, ongoing engineering burden on the
developer of the AI application.

**How it works (mechanism):**
- Two major elements: **client** and **server**.
- The server exposes three kinds of internal components: **tools**
  (functions the model can call), **resources** (data the server shares
  with clients), and **prompts** (tuned instructions for the model) — tools
  covered first, resources/prompts covered in later lessons.
- Without MCP: the AI app's own developer authors the tool schema +
  function implementation, inside their own server/app.
- With MCP: a separate program (the **MCP server**) authors and runs that
  tool schema + function implementation. The AI app becomes an **MCP
  client** that connects to it. Authorship/execution has moved — the
  schema and function still exist, just not in your codebase.
- An MCP server can be authored by anyone (open spec), but official/
  canonical servers are often released by the service provider itself
  (e.g. an official GitHub MCP server, an official AWS MCP server).

**Mental model:** MCP is a **labor-shifting** argument, distinct from (but
complementary to) the **M×N counting** argument covered earlier
([[mxn-problem]]). M×N is about how many integrations must exist as you add
apps/tools. This concept is about **who has to write and maintain** each
integration's schema/function — MCP moves that authorship off your team and
onto whoever built/maintains the MCP server, often the service provider.

**Example:** A chat app letting users ask Claude "what open PRs do I have
across all my repos?" — without MCP, the app's developer writes a GitHub-PR
tool schema + function (and would need many more to cover all of GitHub's
surface area). With MCP, an existing GitHub MCP server already exposes this
as a tool; the app just connects as a client.

**Non-example / misconception to avoid:** "MCP and tool use are the same
thing." They are NOT identical — tool use (a model calling a function via a
schema) is a general capability that exists independent of MCP. MCP is a
protocol about *who authors and executes* those tools (a separate reusable
MCP server, vs. the app developer writing it inline). MCP is built on top of
tool use, not a replacement for it. This is called out in the video as a
common criticism that stems from not understanding MCP's actual scope.

**Common questions (from video):**
1. Who authors MCP servers? → Anyone; often the service provider makes an
   official one.
2. How is this different from calling the API directly? → You still need a
   schema + function either way; MCP just means someone else wrote it.
3. Is MCP the same as tool use? → No, complementary — MCP is about
   authorship/execution location, not a new kind of model capability.

**Related concepts:** [[mxn-problem]] (integration count vs. integration
labor — two distinct but complementary arguments for MCP), tool/function
schemas, client-server architecture, MCP resources, MCP prompts (upcoming).

**Previously learned in:** Builds directly on the M×N retrieval exercise
from this same session (2026-08-29).

**Practice exercise:** Not yet — will follow once resources/prompts and
actual client-server mechanics (discovery, invocation) are covered.

**Retention status:** Developing (~2-3/6). Retrieval test on 2026-08-29:
Q1 (GitHub example, what stays/changes) — correct and precise. Q2 (tool use
vs MCP distinction) — right direction but initially conflated "tool use"
(a model behavior) with "authorship location" (MCP's actual contribution);
clarified with a concrete non-MCP-vs-MCP example (see below). Q3 (relation
to M×N) — correctly identified the two arguments as related-but-distinct,
but mislabeled M×N as being about "labor" — M×N is about integration
*count* (architecture/scaling), not about who performs the labor. Corrected.

**Clarifying example added during teaching (tool use vs. MCP):**
- Tool use alone (no MCP): you write `get_weather(city)` + its JSON schema
  yourself, hand it to Claude via the Anthropic API's tool-use feature,
  Claude calls it, your code runs it.
- With MCP: a weather MCP server already implements `get_weather(city)`
  (schema + function) as its own separate process. Your app is now an MCP
  client that discovers and forwards the call to that server instead of
  running the function itself.
- Takeaway: tool use (model decides to call a function) happens identically
  in both cases from the model's point of view. MCP didn't add a new model
  capability — it added a standard way to discover/invoke tools that live
  in someone else's server. Analogy: MCP is to tool use what HTTP is to
  "making a request" — a protocol underneath a general capability, not the
  capability itself.

**Last reviewed:** 2026-08-29 (taught + first retrieval test)
**Next review:** 2026-08-30
