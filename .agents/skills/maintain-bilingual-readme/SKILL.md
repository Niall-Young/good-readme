---
name: maintain-bilingual-readme
description: Maintain README.md as part of every implementation turn in Codex's currently opened project. Use after any code, configuration, asset, workflow, dependency, API, or behavior change to decide whether documentation is affected; create README.md when absent; keep it bilingual with a visible Chinese/English language switch; and verify README claims against repository evidence. Trigger for project-building, feature, fix, refactor, setup, migration, or documentation work even when the user does not explicitly mention README.
---

# Maintain Bilingual README

Treat README accuracy as part of the definition of done for project changes. Make a deliberate evidence-based decision after each implementation turn; do not rewrite documentation mechanically.

## Protect Project Scope

1. Treat the Codex workspace/current working directory or the user's explicit project path as the project root.
2. Resolve it to an absolute path before reading or writing.
3. Do not substitute an ancestor Git root for the opened project. This matters when the project sits inside a home-directory Git repository or monorepo.
4. Keep all README writes inside that project root unless the user explicitly identifies another target.
5. Honor repository instructions such as `AGENTS.md` before editing.

## Run the End-of-Turn Gate

Run this gate after completing and verifying the requested project change, before the final response.

### 1. Gather evidence

Run `scripts/inspect_readme_context.py <absolute-project-path>` for a compact JSON inventory. Also inspect:

- the final files changed in this turn, including staged, unstaged, and newly created files;
- existing README variants and their current claims;
- relevant manifests, example environment files, commands, entry points, configuration, and public interfaces;
- repository evidence required to describe the change accurately.

Use the script as evidence collection only. Make the documentation-impact decision yourself.

### 2. Decide whether README is affected

Update or create `README.md` when any condition is true:

- no project-root `README.md` exists;
- the project's purpose, audience, capabilities, or visible behavior changed;
- installation, prerequisites, startup, build, test, lint, deployment, or troubleshooting steps changed;
- dependencies, required services, environment variables, configuration, permissions, or security expectations changed;
- a public API, CLI command, route, data format, integration, or compatibility promise changed;
- the meaningful project structure or extension path changed enough to affect navigation;
- an existing README statement became incomplete, misleading, or false.

Normally leave README unchanged when the turn only contains:

- an internal refactor with identical public behavior and workflows;
- tests for already documented behavior;
- formatting, comments, or generated artifacts with no user-facing consequence;
- a tiny fix that does not change usage, guarantees, limitations, or troubleshooting guidance.

When evidence is borderline, prefer a small precise update over a broad rewrite. When README is unchanged, include a one-sentence reason in the final response.

### 3. Create or edit proportionally

If `README.md` is missing, read `references/readme-contract.md` completely and create it from repository evidence. If it exists, preserve its voice and useful organization while enforcing the bilingual contract. Read the reference when restructuring or repairing bilingual navigation; a small factual patch does not require reloading the whole template.

Keep the diff proportional:

- change only affected passages and their counterpart translation;
- preserve user-authored material unless it is wrong, duplicated, or superseded;
- avoid speculative roadmap items, unsupported badges, invented commands, or generic marketing copy;
- use `TODO` only when the repository already treats it as an explicit public commitment; otherwise omit unknown sections;
- never claim a command or workflow was verified unless it was actually run.

### 4. Enforce the bilingual contract

Require one project-root `README.md` with:

- a visible language switch near the top using stable anchors: `[中文](#中文) | [English](#english)`;
- a complete Chinese section headed `<a id="中文"></a>` and `## 中文`;
- a complete English section headed `<a id="english"></a>` and `## English`;
- the same section order, commands, facts, links, warnings, version constraints, and status in both languages;
- natural writing in each language rather than awkward literal translation;
- local language-return links for long documents when they materially improve navigation.

Treat the two languages as one semantic document. A factual change is incomplete until both sides agree.

### 5. Verify before handoff

Before finishing:

1. Re-read every changed README passage against the final repository state.
2. Compare Chinese and English headings and factual content for parity.
3. Check that anchor links, relative links, file paths, commands, and code fences are valid.
4. Run any repository-provided Markdown lint or link check that is available and relevant.
5. Review the final README diff for accidental unrelated rewrites.

## Report the Gate Result

State exactly one outcome in the final response:

- `README: created` — include the major sections established;
- `README: updated` — summarize the concrete facts synchronized in both languages;
- `README: unchanged` — give the evidence-based reason.

Do not imply that the Skill can run as a background hook. It is an end-of-turn workflow applied by Codex whenever this Skill is triggered.
