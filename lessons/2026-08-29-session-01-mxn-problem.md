# Session Log — 2026-08-29 (Session 1)

## Context

First working session on this course. Repository structure initialized
(global + course-level folders per the learning-system spec). Coursera
course map captured from screenshots (Modules 1–4, see LEARNING_STATE.md).

## What happened

Started Module 1 ("Introduction") using retrieval-first teaching rather than
jumping straight to lecture content, since the learner already has general
API/function-calling background.

### Retrieval round 1

**Question asked:** Without looking anything up — what problem does a
typical API solve when connecting an application to external data/tools,
and what's limiting about that when an AI model needs to use *many* tools?

**Learner's answer (paraphrased):** APIs (1) fetch data given permission,
(2) connect different software/hardware. The limitation with many tools is
"the networking graph, connection hierarchy, and automation."

**Evaluation:** Correct high-level intuition on what APIs do. The stated
limitation was vague/jargon-heavy without a precise mechanism behind it —
not yet clearly wrong, but not yet a concrete claim either. Used as a
stepping stone rather than corrected outright.

### Retrieval round 2

**Question asked:** Concretely, with 5 tools (Gmail, GitHub, weather API, a
database, a calculator) each with its own auth/schema/docs — what would you
have to build for an AI model to use all 5? From the model's perspective,
how does it "know" what functions exist and how to call them?

**Learner's answer:** "I might have to build the middleman which can
connect different tools with the agent."

**Evaluation:** Correct instinct (some translation layer is needed) but
still abstract — "middleman" wasn't yet unpacked into what that middleman
actually has to do (auth handling, schema translation, result parsing).

### Concept introduced: The M×N problem

Explained precisely: M AI apps × N tools = M×N custom integrations without a
shared protocol. See [concepts/mxn-problem.md](../concepts/mxn-problem.md)
for the full concept record.

### Retrieval round 3 — IN PROGRESS (not yet answered by learner)

Asked the learner to self-assess: was their earlier phrase "connection
hierarchy and automation" pointing at the same M×N problem, or gesturing at
something different? This question was interrupted by a request to persist
progress to the repo — answer still pending as of this log entry.

## Concepts touched

- M×N integration problem (Developing — see concept record)

## Mistakes / misconceptions

None yet logged — no answer has been clearly wrong, just imprecise/abstract.
Watch for whether "connection hierarchy and automation" turns out to be a
genuine misconception (e.g. confusing MCP with a general orchestration/
workflow-automation tool) once the learner responds.

## Next step

1. Get the learner's answer to the pending retrieval-round-3 question.
2. Continue Module 1: introduce what MCP actually is (client-server
   protocol, servers expose tools/resources/prompts, clients discover and
   invoke them) — ideally still retrieval-first where prior API knowledge
   applies.
3. Eventually have the learner watch/summarize "Introducing MCP" and "MCP
   clients" videos and process them per the transcript-ingestion workflow.
