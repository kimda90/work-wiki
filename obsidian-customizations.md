# Work Wiki

It uses:

```text
Obsidian + Markdown + Git + Codex/agent
```

Purpose:

```text
Capture messy work notes
→ let an agent digest them
→ maintain clean documentation
→ preserve decisions, tasks, risks, questions, and learnings
```

Core structure:

```text
raw/        human notes, never rewritten
wiki/       durable agent-maintained knowledge
generated/  briefs, summaries, reports
templates/  reusable note formats
skills/     agent workflows/prompts
AGENTS.md   rules for how agents maintain the wiki
index.md    navigation map
log.md      append-only activity history
```

Core agent skills:

```text
digest-raw-notes   turns notes into structured wiki updates
daily-brief        summarizes what matters before work
prepare-meeting    creates meeting context and questions
lint-wiki          finds stale, duplicate, or contradictory docs
map-codebase       documents repos once you get access
```

Governance approach:

```text
Keep it lightweight.
Use one agent with different skills.
Do not build client-specific agent roles yet.
Raw notes are source of truth.
Agent outputs are drafts until reviewed.
Important claims need provenance.
Humans own decisions and external actions.
```

Obsidian role:

```text
Human capture and browsing layer.
Daily notes go in raw/daily.
Meeting notes go in raw/meetings.
Agents update wiki/ and generated/.
```

The main idea is to create a **portable personal work-memory system** that helps you onboard, remember context, prepare for meetings, document technical discoveries, and later prototype agentic documentation workflows for real projects.

# Configure Obsidian
Configure Obsidian as the **human capture/browser layer**. Let Codex/agents handle digestion outside Obsidian.

## 1. Open the generated folder as a vault

In Obsidian:

```text
Open vault
→ Open folder as vault
→ select work-wiki/
```

This should be the folder that contains:

```text
AGENTS.md
README.md
index.md
log.md
raw/
wiki/
generated/
templates/
skills/
```

Obsidian works well for this because the vault is just Markdown files plus metadata/properties, and its core plugins include File Explorer, Search, Graph View, Daily Notes, Templates, Backlinks, Properties View, and more. ([Obsidian][1])

## 2. Turn on the useful core plugins

Go to:

```text
Settings → Core plugins
```

Enable:

```text
Daily notes
Templates
Properties view
Backlinks
Outgoing links
Graph view
Search
Quick switcher
Command palette
File recovery
Canvas optional
Bases optional
```

Do **not** start with many community plugins. The core setup is enough.

## 3. Configure Daily Notes

Go to:

```text
Settings → Daily notes
```

Set:

```text
Date format:
YYYY-MM-DD

New file location:
raw/daily

Template file location:
templates/daily-note.md
```

Daily Notes is a core plugin that creates or opens a note based on today’s date, and Obsidian lets you set both the destination folder and a template for those notes. ([Obsidian Help][2])

Suggested hotkey:

```text
Settings → Hotkeys → Open today's daily note
Ctrl+Shift+D
```

Now your normal daily capture flow is:

```text
Ctrl+Shift+D
→ write messy notes
→ later run Codex digest
```

## 4. Configure Templates

Go to:

```text
Settings → Templates
```

Set:

```text
Template folder location:
templates
```

Then use templates manually for meetings or structured notes:

```text
Command palette → Templates: Insert template
```

Use:

```text
templates/meeting-note.md
templates/daily-note.md
templates/concept.md
templates/workflow.md
templates/decision-adr.md
```

For your workflow, templates are mainly for **raw capture** and occasional manual structured notes. The agent should create most `wiki/` pages.

## 5. Configure Files & Links

Go to:

```text
Settings → Files and links
```

Recommended settings:

```text
Default location for new notes:
In the folder specified below

Folder to create new notes in:
raw/project-notes

New link format:
Shortest path when possible

Use [[Wikilinks]]:
Enabled

Default location for new attachments:
In the folder specified below

Attachment folder path:
raw/screenshots
```

This makes accidental new notes land in `raw/`, not `wiki/`.

That matters because:

```text
raw/  = human/source notes
wiki/ = durable agent-maintained knowledge
```

## 6. Configure Properties for agent readability

Go to:

```text
Settings → Editor → Properties in document
```

I recommend:

```text
Source
```

Obsidian properties are stored as YAML at the top of Markdown files, and properties can hold structured data such as text, links, dates, checkboxes, numbers, lists, and tags. ([Obsidian][3])

Using `Source` keeps the YAML visible:

```yaml
---
type: workflow
title: Workflow Overview
status: evolving
confidence: low
tags:
  - workflow
  - onboarding
---
```

That is better for Codex and easier to diff in Git.

## 7. Pin the important files

Open these files and pin/bookmark them:

```text
index.md
log.md
raw/daily/YYYY-MM-DD.md
wiki/open-questions/onboarding-questions.md
wiki/tasks/follow-ups.md
wiki/risks/project-risks.md
generated/onboarding-briefs/week-1-brief.md
```

Use `index.md` as your home page.

A good workspace layout:

```text
Left pane:
File explorer

Center:
Current note

Right pane:
Backlinks
Outgoing links
Properties
```

## 8. Optional: install Obsidian Git

This is optional. Since you are technical, it may be useful.

Community plugin:

```text
Settings → Community plugins
→ Browse
→ search “Git”
→ install Obsidian Git
```

The Obsidian Git plugin can commit, pull, push, show diffs, and provide a source-control view inside Obsidian. ([GitHub][4])

Suggested settings:

```text
Auto pull on startup:
enabled

Auto commit-and-sync:
disabled at first

Source control view:
enabled
```

I would keep commits manual in the beginning:

```text
Command palette → Git: Commit all changes with specific message
```

If you are on Linux, prefer the Obsidian AppImage or a normal package with filesystem access if you use Git integration; the Obsidian Git plugin notes limitations with Snap and recommends avoiding Flatpak for advanced setups. ([GitHub][4])

## 9. Do not edit these manually unless needed

In Obsidian, treat these as mostly agent-maintained:

```text
wiki/
generated/
index.md
log.md
```

You can read and lightly correct them, but your main human writing should go here:

```text
raw/daily/
raw/meetings/
raw/project-notes/
raw/references/
```

That keeps the system clean.

## 10. Recommended daily workflow

Morning:

```text
Open generated/onboarding-briefs/ or latest daily brief
Review open questions and follow-ups
```

During work:

```text
Write everything quickly into raw/daily/YYYY-MM-DD.md
Use raw/meetings/ for meeting notes
Paste links, commands, errors, questions, names, decisions
```

End of day, in terminal/Codex:

```text
Digest the newest files in raw/. Update the wiki, generated briefs, open questions, tasks, risks, learnings, index.md, and log.md. Do not modify raw notes. Return a concise changelog.
```

Then review in Obsidian.

Commit:

```bash
git status
git add .
git commit -m "Digest notes YYYY-MM-DD"
```

## Minimal setup summary

Configure only this first:

```text
Open work-wiki/ as vault
Enable Daily Notes
Enable Templates
Set Daily Notes folder to raw/daily
Set Daily Notes template to templates/daily-note.md
Set Templates folder to templates
Set new notes folder to raw/project-notes
Set attachments folder to raw/screenshots
Set Properties display to Source
Use index.md as home
```

That is enough to make Obsidian useful without overbuilding.

[1]: https://obsidian.md/help/plugins "Core plugins - Obsidian Help"
[2]: https://help.obsidian.md/plugins/daily-notes "Daily notes - Obsidian Help"
[3]: https://obsidian.md/help/properties "Properties - Obsidian Help"
[4]: https://github.com/Vinzent03/obsidian-git "GitHub - Vinzent03/obsidian-git: Integrate Git version control with automatic commit-and-sync and other advanced features in Obsidian.md · GitHub"
