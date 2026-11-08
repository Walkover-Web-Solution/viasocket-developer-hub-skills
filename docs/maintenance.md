# Documentation maintenance

State for the weekly documentation review: what was reviewed, where each topic lives, and what is still open. The
next run reviews changes since the revision below, then the open items.

## Last review

- Reviewed revision: `f34f805` (main, 2026-10-26). First run: full inventory.
- Checks run: `python3 code/build-kb-sections.py && git diff --exit-code -- knowledge-base/index.md knowledge-base/sections`
  (passed, 185 section files); `--check` (up to date); relative links in every `.md` outside `knowledge-base/sections/`
  (one broken, fixed: README pointed to `dh-review-chat.md`); every `<file> "<Heading>"` cited by `skills/*.md`,
  `dh-review-agent.md` and the two read-in-full KB files resolves to a heading.

## What this repo is

Prompts and knowledge, not an application: skills that agents follow through the viaSocket MCP to build Developer Hub
plugs (`skills/`), the knowledge base they cite (`knowledge-base/`), the publish policy, the review prompt, and the
prompts of viaSocket's in-product planner. The only code is `code/build-kb-sections.py` (generates the KB index and
sections) and `code/vectorless-search-rag.js` (KB retrieval snippet for the planner).

## Coverage map

| Topic | Authoritative location | Status |
| ----- | ---------------------- | ------ |
| Agent entry point, constraints | `AGENTS.md` (Claude Code reads it via `CLAUDE.md`) | verified |
| Skill selection | `skills/index.md` | verified |
| Skill runtime / prompt templates | `skills/skill-architecture.md` | partial: not re-verified against the live MCP |
| Publish rules, safety, rollback | `knowledge-base/publish-policy.md` | verified (wins over other files) |
| Plug/action/trigger knowledge | `knowledge-base/dh-knowledgebase.md` + cited files | partial: citations resolve; content not checked against the live Developer Hub API |
| Connections (auth) | `knowledge-base/dh-connection-kb.md` + cited files | partial: as above |
| Developer Hub data model | `knowledge-base/dh-database-schema.md` | partial: not checked against the live API |
| Review gate | `dh-review-agent.md`, `knowledge-base/plug-review.md` | verified exists and is cited |
| In-product planner architecture | `architecture-context/current_architecture.md`; plan in `target_architecture.md` | partial: not re-verified |
| Product overview for humans | `README.md` | partial: describes the in-product planner, not the skills |
| Generated KB index/sections | `code/build-kb-sections.py` → `knowledge-base/index.md`, `knowledge-base/sections/` | verified |
| CI | `.github/workflows/kb-sections.yml` (rebuild + commit), `docstar.yml` (publish changed `.md` to DocStar) | verified from config, not run |
| Public/private boundary | `AGENTS.md` "Changing this repo" | verified: repo is public; all `.md` publish to DocStar |
| Product vision, ICP, success measures | none (no `VISION.md`) | missing: needs an owner decision |
| UI/design, website/SEO, experiments, data workloads, CLI/SDK | — | not applicable: no UI, site, analytics or SDK in this repo |
| Backend, performance, caching | — | not applicable: behaviour lives in viaSocket's Developer Hub, documented via the KB |

## Open items

- `docstar.md` says synced docs live under `docs/` with YAML frontmatter, but `docstar.yml` sends every changed `.md`
  in the repo without frontmatter. Decide which is intended.
- No `VISION.md`: product purpose, audience and non-goals are only implied by `README.md` and `skills/index.md`.
- `README.md` describes the in-product planner only; it does not mention the MCP skills that `skills/index.md` serves.
- KB and skill content have not been checked against the live Developer Hub API in this review.
