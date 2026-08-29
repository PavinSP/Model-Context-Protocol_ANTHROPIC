# Mistake Log: "Server" vs "MCP Server" Naming Ambiguity

**Concept:** MCP clients / full call sequence ([[mcp-clients]])

**My mistake:** In the "Explaining Client–Server Communication" practice
assignment (graded by AI, 80%/4/5), used the bare word "server" to refer to
both the app's own backend AND the MCP server interchangeably, without
distinguishing them — e.g. "the request goes to the server which then goes
to the MCP client and then to the server which goes back to the client."
Also used a generic example ("what does this repository have?") instead of
a concrete GitHub-specific one.

**What I believed:** That having previously understood the distinction
verbally (via the restaurant analogy in session 2) meant it would
automatically carry over into written explanation without extra
discipline.

**Correct understanding:** In writing, ALWAYS say "your app's server" (or
"my server") and "the MCP server" explicitly and consistently — never bare
"the server" — because the word is structurally ambiguous the moment both
parties exist in the same explanation. This must be an active writing
habit, not just a concept understood in conversation.

**Why the mistake was made:** Verbal Q&A in this session's earlier
practice used analogies (waiter/chef/kitchen) that made the distinction
easy to track without needing careful naming. Writing a standalone
explanation removed that scaffolding, and the underlying ambiguity of
reusing the word "server" resurfaced.

**Correction exercise done:** Guided step-by-step rewrite in the live
session, sentence by sentence, explicitly requiring "my server" / "the MCP
server" naming and a concrete tool name (`list_repo()`). Also re-surfaced
and resolved the related GitHub-contact-timing slip (see
[[mcp-clients]] "Recheck resolved" note) — this time with lighter
scaffolding than before, suggesting real (if incomplete) improvement.

**Related concepts:** [[mcp-clients]], [[what-is-mcp]]

**Date:** 2026-08-29
**Next review:** 2026-08-30 — cold, unprompted retest of the full sequence
in writing (not verbally), explicitly checking whether "server" ambiguity
and the GitHub-timing point both hold up without any scaffolding at all.
