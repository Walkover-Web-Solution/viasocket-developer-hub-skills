# Instructions for AI agents working in this repo

Cursor, Codex and other agents load this file automatically when they open the repo.

- Start at [skills/index.md](skills/index.md). It picks exactly one skill for the task; read that skill whole and follow it. Do not
  read the other skills.
- Read [knowledge-base/publish-policy.md](knowledge-base/publish-policy.md) before publishing anything; it wins over
  every other file.
- Never read all of `knowledge-base/`. Read the files the chosen skill says to read in full; for every other
  `<file> "<Heading>"` it cites, find the heading in [knowledge-base/index.md](knowledge-base/index.md) and read only
  that section's file.
- `knowledge-base/index.md` and `knowledge-base/sections/` are generated: to change knowledge, edit the source file in
  `knowledge-base/` and run `python3 code/build-kb-sections.py`.
- The root `dh-*-agent.md` files (except `dh-review-agent.md`, used for reviews), `dh-master-planner.md`,
  `system-instruction/` and `sub-agents/` are prompts for viaSocket's in-product planner, not for you.

## Changing this repo

- The repo is public, and on every push to `main` every changed `.md` file is published to DocStar
  (`.github/workflows/docstar.yml`). Never commit secrets, tokens or customer data.
- After editing `knowledge-base/*.md` or `code/build-kb-sections.py`, run `python3 code/build-kb-sections.py` and
  commit the result; `python3 code/build-kb-sections.py --check` exits 1 if it is out of date. CI
  (`.github/workflows/kb-sections.yml`) rebuilds and commits it on `main` too.
- To add or rename a skill, change the table in `skills/index.md` only.

| Task | Start at |
| ---- | -------- |
| Use a skill (build a plug, action, trigger or connection) | `skills/index.md` |
| Change knowledge (fields, perform code, connections, UX) | the source file in `knowledge-base/`, then rebuild |
| Change who may publish what | `knowledge-base/publish-policy.md` |
| Change the review a plug must pass | `dh-review-agent.md`, `knowledge-base/plug-review.md` |
| Understand the in-product planner pipeline | `architecture-context/current_architecture.md` (planned: `target_architecture.md`) |
| Documentation coverage, last reviewed revision, open gaps | `docs/maintenance.md` |
