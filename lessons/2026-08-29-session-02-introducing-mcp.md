# Session Log — 2026-08-29 (Session 2)

## Context

Continuation of session 1. Learner processed "Welcome to the course"
(logistics only) then "Introducing MCP" (Module 1, 4 min) — the first
real conceptual video.

## Workflow correction from learner

User corrected the approach mid-session: teach the concept in FULL detail
first, write it to notes immediately, THEN test — not test before/instead
of teaching. This session followed that corrected order. Saved as a
standing preference (see memory: feedback-video-lesson-workflow covers the
video-first part; this reinforces teach-before-test as well).

## What happened

### Teaching: "Introducing MCP"

Taught the full content of the video: GitHub chatbot example, the
labor-shifting argument (MCP moves tool schema/function authorship from
the app developer to a separate MCP server), the three FAQs (who authors
MCP servers / how is this different from calling the API directly / is MCP
the same as tool use), and explicitly distinguished this "labor" argument
from the earlier M×N "count" argument. Written to
[concepts/what-is-mcp.md](../concepts/what-is-mcp.md).

### Retrieval test (after teaching)

**Q1 — GitHub example, what stays/changes without vs. with MCP:**
Learner's answer was correct and precise — correctly identified that the
tool/schema work still has to happen somewhere, but with MCP, GitHub does
it and the chatbot just connects as a client.

**Q2 — Distinction between "tool use" and "MCP":**
Learner's initial answer was directionally right but conflated "the model
using a function" with "who authored the function" — asked for an example
to sharpen this. Provided a concrete non-MCP-vs-MCP `get_weather` example
and the HTTP analogy (MCP is to tool use what HTTP is to "making a
request"). Learner should re-explain this back in a future review to
confirm it landed.

**Q3 — Relation between this video's argument and M×N:**
Learner correctly identified the two as related-but-distinct, but
mislabeled M×N as being "about labor" — corrected: M×N is about
integration *count*/scaling, this video's argument is about integration
*labor/authorship* for any single integration. This is now explicitly
cross-referenced in both concept files to prevent future conflation.

## Concepts touched

- What MCP is / labor-shifting argument (New → Developing, ~2-3/6) — see
  concepts/what-is-mcp.md
- M×N problem (Strong, refined) — cross-reference added to prevent
  conflating "count" and "labor" arguments

## Mistakes / misconceptions logged

1. **Misconception (corrected):** Conflating "tool use" (a model behavior)
   with "who authored the tool" (MCP's actual contribution). Corrected via
   the `get_weather` example and HTTP analogy. Should be re-tested in a
   future session without re-explaining first, to check if it stuck.
2. **Misconception (corrected):** Labeling M×N as being fundamentally about
   "labor" rather than "integration count." Corrected — cross-referenced in
   both concept notes.

## Next step

1. Re-test Q2 and Q3 in a future review session (2026-08-30 or later)
   WITHOUT re-explaining first, to check if the corrections actually stuck.
2. Watch and process "MCP clients" (`03_MCP_clients.txt` — already pasted
   by user but explicitly held back per user's request until this lesson's
   testing was complete). This is the next lesson to teach.
