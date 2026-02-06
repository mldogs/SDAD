# Prompt: Bootstrap SDAD documentation pack

Paste this to a coding agent **inside the target project repo**.

---

You are a coding agent. Your task is to generate the **initial SDAD documentation pack** for this repository,
starting only from `PROJECT_BRIEF.md`.

## Preflight (avoid the common “template/ trap”)

All paths in this prompt are relative to the **repository root you are currently in**.

- You must create/update SDAD files at repo root (e.g. `.agent/AGENTS.md`, `docs/constitution/*`).
- **Do not** update files under `template/` (if it exists). If you accidentally wrote into `template/`, that’s a mistake.

If `PROJECT_BRIEF.md` is missing at repo root but you see `template/PROJECT_BRIEF.md` (and `template/docs/...` etc),
it means the SDAD template was copied *as a folder* instead of being copied *into the repo root*.

In that case, fix the structure first:

1) Copy the template contents into repo root (preserving dotfolders):

   - `rsync -a template/ ./`

2) Continue this task using repo‑root files (not `template/...`).

## Output requirements

- Do **not** implement product code yet. Focus only on documentation scaffolding and correctness.
- Treat `docs/constitution/*` as **immutable**: create/update them, but if you need to change their meaning,
  ask first and record the change in the future ExecPlan Decision Log.
- Keep docs concrete: no vague language; acceptance criteria must be verifiable by commands/tests.
- Keep open questions to **max 3**, with multiple choice options.

## What to do

1) Read `PROJECT_BRIEF.md` (repo root).

2) Create/update the SDAD files:
- `.agent/AGENTS.md` (Codex contract: Always/Ask/Never + commands)
- `.agent/PLANS.md` (already present; keep canonical)
- `CLAUDE.md` (mirror of agent contract)
- `docs/START_HERE.md` (entrypoint for a fresh agent)
- `docs/constitution/PURPOSE.md`
- `docs/constitution/CONSTRAINTS.md`
- `docs/constitution/ARCHITECTURE.md`
- `docs/constitution/QUALITY_GATES.md`
- `docs/constitution/SECURITY.md` (optional but recommended)

3) Create the first ExecPlan:
- Path: `docs/execplans/pilot_execplan.md`
- Use the structure from `.agent/PLANS.md`.
- Ensure the ExecPlan file is exactly **one single fenced code block** labeled `md` (no nested ```).
- Put concrete acceptance criteria and concrete commands into the plan (even if some are TODO placeholders).

4) If critical preferences are missing (stack, test runner, dependency policy, etc.), ask up to **3** questions.
Each question must include 2–4 mutually exclusive options and a recommended default.

5) If this is a git repo (there is a `.git/` directory), create **one local commit** with the generated/updated docs:
   - commit message: `docs: bootstrap SDAD doc pack`
   - do **not** push to any remote

## Definition of done (for this task)

- The repository has a coherent SDAD doc pack.
- A fresh agent with empty context can read `docs/START_HERE.md` and `docs/execplans/pilot_execplan.md`
  and start implementation with minimal/no follow‑ups.

At the end, reply with:
- a short checklist of files you created/updated
- the exact next instruction: “Start a fresh agent and paste `sdad_starter_pack/prompts/02_fresh_agent_run.md`”.
