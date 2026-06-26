---
name: bootstrap-work-wiki
description: "Create or adapt a local-first Obsidian-compatible work wiki with raw/wiki/generated/templates/skills structure. Use whenever the user asks to bootstrap, scaffold, clone, configure, personalize, or make a work wiki, project memory vault, agent-maintained knowledge base, or Obsidian work vault, including requests to create reusable work-wiki bootstrap instructions."
---

# Bootstrap Work Wiki

Use this skill to create or adapt a work wiki for a person, team, project, or client. The target outcome is a local-first Markdown vault with immutable raw notes, durable synthesized wiki pages, generated artifacts, templates, repo-scoped skills, navigation, and an operation log.

If `generated/bootstrap/work-wiki-bootstrap.md` is available, read it and use it as the canonical scaffold specification. If it is not available, follow this skill directly.

## Configuration Interview

Ask for missing configuration in one compact numbered block. The goal is to get enough detail to scaffold the vault without inventing project facts.

1. Target path and wiki name.
2. Owner name, role, organization, and timezone.
3. Current project, client, product, or domain focus.
4. Starting source material: raw notes, meeting notes, references, screenshots, transcripts, or repositories.
5. Privacy constraints, secrets policy, and sources that should not be copied.
6. Desired wiki domains beyond the default set.
7. Core skills to install: digest raw notes, daily brief, prepare meeting, lint wiki, map codebase, bootstrap work wiki.
8. Whether to create an Obsidian-ready vault and `.agents/skills` symlink.
9. The first useful output after bootstrap: digest, daily brief, onboarding brief, meeting prep, or codebase map.

If the user has already supplied enough context, infer the configuration and continue. Use `unknown` or `TODO` for anything not supplied. Do not block on details that can safely be filled later.

## Default Structure

Create this top-level model:

- `raw/`: immutable source notes and files.
- `wiki/`: durable, agent-maintained knowledge pages with frontmatter.
- `generated/`: derived briefs, reports, reviews, diagrams, and summaries.
- `templates/`: copy-ready source-note and wiki-page templates.
- `skills/`: Codex-style skill folders.
- `.agents/skills`: symlink or fallback pointer to `skills/`.
- `index.md`: navigation map.
- `log.md`: append-only operation log.
- `AGENTS.md`: vault operating rules for agents.
- `README.md`: short human-facing explanation.

Default wiki domains:

- `context`
- `people`
- `projects`
- `product`
- `workflows`
- `architecture`
- `frontend`
- `backend`
- `integrations`
- `infrastructure`
- `data`
- `agents`
- `decisions`
- `glossary`
- `open-questions`
- `tasks`
- `risks`
- `learnings`

## Build Workflow

1. Inspect the target path if it exists. Preserve existing files unless the user explicitly asks to replace them.
2. Create missing directories and `.gitkeep` files for empty directories.
3. Create or update `AGENTS.md` with the raw/wiki/generated model, knowledge standards, and non-negotiable rules.
4. Create `README.md`, `index.md`, and `log.md`.
5. Create templates for daily notes, meeting notes, concepts, systems, workflows, decisions, questions, tasks, risks, learnings, and digest reports.
6. Create seed wiki pages with required frontmatter. Keep seed claims generic unless sourced from the user-provided configuration or copied raw material.
7. Create core skills:
   - `digest-raw-notes`
   - `daily-brief`
   - `prepare-meeting`
   - `lint-wiki`
   - `map-codebase`
   - `bootstrap-work-wiki`
8. Copy user-provided source material into the relevant `raw/` directories without rewriting the content.
9. Add Obsidian wiki links in `index.md` for seed pages and skills.
10. Append a bootstrap entry to `log.md` with timestamp, files created, configuration source, and unresolved unknowns.
11. Verify the result before responding.

## Required Wiki Frontmatter

Every Markdown file under `wiki/` needs at least:

```yaml
---
type: concept
title: ""
description: ""
tags: []
timestamp: YYYY-MM-DDTHH:mm:ss-03:00
status: draft
confidence: low
source_count: 0
related: []
---
```

Use the configured user's actual timezone offset when replacing the timestamp placeholder.

Allowed `type` values: `context`, `person`, `project`, `product`, `concept`, `workflow`, `system`, `architecture`, `frontend`, `backend`, `integration`, `infrastructure`, `data`, `agent`, `decision`, `glossary`, `open-question`, `task`, `risk`, `learning`, `report`.

Allowed `status` values: `draft`, `evolving`, `stable`, `superseded`, `archived`.

Allowed `confidence` values: `low`, `medium`, `high`.

## Safety Rules

- Never delete or destructively rewrite files under `raw/`.
- Do not invent organization, project, repository, stakeholder, stack, or product facts.
- Treat unknowns as open questions.
- Keep confidential or sensitive information only if the user provided it or it already exists in raw sources.
- Do not inspect or map external repositories during bootstrap unless the user explicitly asks for that additional step.
- If the target directory is non-empty, prefer additive changes and report conflicts.

## Verification Checklist

Before finishing, verify:

- Required top-level files exist.
- Required directories exist.
- `.agents/skills` points to `skills/` or a fallback note exists.
- Every `wiki/*.md` file has required frontmatter.
- Every core skill has `SKILL.md` with `name` and `description`.
- `index.md` links to seed pages and core skills.
- `log.md` contains a bootstrap entry.
- Raw source files were not modified.

## Response Format

Return:

- Files and directories created.
- Files updated.
- Configuration values used.
- Unknowns left as placeholders or open questions.
- Any conflicts or skipped actions.
- Suggested first prompts for the user.
