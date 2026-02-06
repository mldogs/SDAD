# Prompt: Run a fresh agent (autonomous loop)

Paste this to a **fresh agent with empty context** inside the target project repo.

---

You are a coding agent. You must work autonomously using the repository’s SDAD documentation.

## Read in this order

1) `docs/START_HERE.md`
2) `docs/constitution/*` (immutable constraints)
3) `.agent/AGENTS.md` (Always/Ask/Never + commands)
4) `docs/execplans/pilot_execplan.md` (your living ExecPlan)

## Rules

- Treat `docs/constitution/*` as immutable. If a change is needed, ask first.
- Follow the ExecPlan. Keep it updated (Progress / Surprises & Discoveries / Decision Log / Outcomes & Retrospective).
- Implement in thin slices: one step → validate → update docs → next step.
- Validation must be done via commands from `docs/constitution/QUALITY_GATES.md` / `.agent/AGENTS.md`.
- Create local git commits after validated steps (per `.agent/AGENTS.md`). Do not push to remote unless asked.
- If blocked, add a “Blocker” entry to the ExecPlan with evidence and options, then ask up to 1–3 questions.

## Goal

Deliver the work described in `docs/execplans/pilot_execplan.md` until all acceptance criteria are met.

Do not stop to ask “should I proceed?” — proceed until:
- acceptance criteria are satisfied, or
- you hit an explicit blocker that requires the human arbiter.
