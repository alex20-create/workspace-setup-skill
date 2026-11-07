---
name: workspace-setup
description: 'Sets up a workspace where Claude can work well on one piece of work: a claude.ai Project (custom instructions plus context documents), a Claude Code project folder (CLAUDE.md and whatever else the folder needs), or both. It gathers what already exists about the work before asking anything, asks every decision question in one round, shows the drafts before writing, links to the sources instead of copying them, and marks anything without a source as PENDING. Use it whenever the user wants to prepare a place for Claude to work on something, even if they only say they are starting something new: "set up a workspace", "create a project", "prepare the project folder", "nuevo proyecto en claude.ai", "monta la carpeta del proyecto", "prepara el espacio de trabajo". Not for picking a CLAUDE.md template on its own, improving an existing CLAUDE.md, or installing plugins and connectors.'
---

# Workspace Setup

Builds the place where Claude will work on one piece of work, so that every new
conversation starts already knowing what the work is, where its facts live and
what Claude may do on its own. There are two kinds of workspace:

- **A claude.ai Project**: custom instructions plus context documents uploaded
  to the Project.
- **A Claude Code project folder**: a `CLAUDE.md` and whatever else the folder
  needs for Claude to work well in it.

Some work needs both. The skill gathers, asks once, drafts, tests if the user
wants and delivers. It does not replace the tools that already own part of the
job: a CLAUDE.md template picker writes the CLAUDE.md, a note-sync skill keeps a
notes vault, an automation recommender proposes hooks and integrations. Where
those exist, this skill calls them as steps instead of redoing their work.

## The rule underneath everything

Every fact lives in one place. A workspace points to its sources (a project
manager, a notes vault, a repository, a design system); it does not copy them.
A copy goes stale the day its source changes, and from then on Claude acts on
the wrong version without knowing it. When a copy cannot be avoided (the
Project cannot reach the source, for instance), it is marked as generated, with
its source and date, and nobody edits it by hand: it is regenerated from the
source.

Two more rules follow from the same idea:

- **Nothing invented.** A fact with no source goes into the draft as
  `PENDING: <what is missing>` (or the same word in the drafts' language), never
  as a plausible guess. A wrong fact in standing instructions misleads every
  future conversation, and nobody rereads instructions looking for it.
- **Nothing persisted without asking.** No file, page, note or repository
  change before the user has seen the draft and said yes. Reading is free;
  writing waits.

Reply in the language the user writes in. The drafts are written in the
language the user chooses in step 3, which can differ per target (a repository's
rules may require English while the Project instructions do not).

## Local map first

The skill is generic; the user's setup is not. Before step 1, look for a local
map that names the concrete tools and places. It can be a section titled
`workspace-setup local map` in the user's own instructions (a `CLAUDE.md` in
Claude Code, read from disk), a section titled `Local map for this install` in
this file (added when the skill was packaged for one person's claude.ai
account), or the custom instructions of the current claude.ai Project, if they
name these things. Where several exist, the most specific wins line by line;
`references/local-map.md` gives the order.

A map can name: the CLAUDE.md template picker and where its template collection
lives; the notes vault and where project notes go; the project manager where
work is tracked (a Notion database, for example); the automation recommender and
the skill used to dry-run instructions; the house order of sections in a
CLAUDE.md; language and style rules for drafts; and existing workspaces that
show what works. Whatever the map says overrides the defaults in this skill.

With no map, discover: list the connectors, skills and file access this session
has, and note which of the roles above each one could fill. Use what you find,
say what you assumed, and at the end (step 6) offer to write a map so the next
run does not have to discover again. `references/local-map.md` has the format
and the discovery checklist.

## 1. Detect the target

Decide whether the user wants a claude.ai Project, a Claude Code folder, or
both, from what they said and from where you are running:

- "Project in claude.ai", "project instructions", "knowledge" point to a
  Project; "folder", "repo", "CLAUDE.md" point to Claude Code.
- In claude.ai with no file access, a Claude Code folder can still be the
  target, but it is delivered as text for the user to save.
- In Claude Code, both targets can be delivered; the Project still has to be
  created by hand.

If it is still unclear, do not stop to ask: gather for both, and make the target
the first question of the batch in step 3.

## 2. Gather what already exists

Before asking anything, read what already exists about this work, so that the
questions in step 3 arrive with proposed answers instead of blank fields. Look
in every source the map or discovery turned up:

- the project manager: the item or page for this work, its status, its links;
- the notes vault: a project note, decisions, open questions;
- the repository or folder: README, any existing `CLAUDE.md` or `AGENTS.md`,
  manifest files (`package.json`, `pyproject.toml` and the like), the layout;
- claude.ai: artifacts, an existing Project's instructions (where the session
  can reach them), a design system;
- handoff, memory or session-log files the setup keeps, checked against the
  live state (they go stale);
- this conversation: what the user has already said.

Only read. Then write a short inventory and show it with the questions: each
source, what kind of data it holds (tasks, decisions, specs, design tokens,
code), and any contradiction (two places, or two files within one source,
claiming different things about the same fact). The inventory is what step 3
asks about and what the drafts link to. If a source the map names or discovery found cannot be reached in this session (an
existing claude.ai Project's instructions, often), say so in the inventory; do
not fill the gap from memory.

## 3. Ask every decision question in one round

Ask once, with everything, because a drip of questions costs the user more than
one well-prepared batch. `references/decision-questions.md` has the template.
The batch covers:

1. **Target**, only if step 1 left it open.
2. **Purpose**: what this workspace is for, and what it is not for. For a
   claude.ai Project, also its name and one-line description.
3. **Source of truth per kind of data**: for each kind found in the inventory,
   which source wins. The "where each thing lives" part of the drafts is built
   from this answer. For a claude.ai Project, also how the Project reaches each
   source: a connector or synced integration (stays current), a link it can
   open, or a generated copy uploaded to it.
4. **Permissions, in three tiers**: what Claude does without asking, what it
   does after a yes, and what it does only when asked. For a Claude Code
   folder, also whether to enforce part of them in the folder's permission
   settings, and whether the `CLAUDE.md` is committed or kept local.
5. **Routines**: phrases that start a fixed routine ("open the session", "close
   the day") and what each one runs.
6. **Language and style**: language of the drafts and of the replies, tone,
   formats to use or avoid.

For each question, propose an answer drawn from the inventory or the map and
say where it came from; the user confirms or corrects. Where nothing supports a
proposal, leave the answer open instead of guessing. If the user already
answered something in their request, show it as settled rather than asking
again. A structured question tool may be used if it fits the whole batch in one
round; if it limits the number of questions, ask in a single message instead.

## 4. Draft and show

Write every deliverable in full and show it before writing anything anywhere:

- **claude.ai Project**: follow `references/claude-ai-project.md`. The
  instructions, plus the context documents (usually one: a map of links to the
  sources).
- **Claude Code folder**: follow `references/claude-code-folder.md`. The
  `CLAUDE.md` comes from the template picker the map names or discovery
  found: hand it the target
  folder and the answers from step 3, and let it choose and fill the template;
  template choice is its job, not this skill's. Without a template picker, write
  the CLAUDE.md directly, in the house order of sections from the map or the
  user's own instructions, or in the
  plain order the reference gives if there is no map.

Mark every gap `PENDING` and every unavoidable copy with its generated header.
List the PENDING items under the drafts, so the user sees at a glance what still
needs a source. Revise until the user is satisfied, showing each revision again
in full or as a clear diff.

## 5. Offer a test

Offer to dry-run the drafts with a fresh agent that has no conversation
context: it gets only the drafts and a realistic first request ("pick up where
we left off", "add the export feature"), and reports every doubt, contradiction
or missing fact it runs into. The author cannot see these gaps, because the
author already knows the context the drafts forgot to state.

Use the instruction-testing skill the map names (a skill improver with a
clean-subagent dry run, for example). If that skill accepts only skills as
targets, follow its protocol directly: launch one subagent with the drafts and
the request, no other context, and ask for its doubts. Before launching, state
the estimated cost, taking the reference figure from the instruction-testing
skill if it gives one and saying whose figure it is, and launch only on a yes. Where
there are no subagents (claude.ai), say that a clean test is not possible here
and offer it for a Claude Code session.

Fix what the test finds that is real, show the changes, and move on.

## 6. Deliver

**claude.ai Project.** This skill cannot create a Project; say so plainly.
Deliver:

- the instructions as one block, ready to paste;
- each context document as a file to upload (or a block to save as one);
- the steps from `references/claude-ai-project.md` to create the Project, paste
  the instructions and upload the documents.

**Claude Code folder.** Write the files only after an explicit yes to the shown
drafts, list every path written, and do not commit unless asked.

Then offer, one at a time and only where the map or discovery found the tool:

- the note-sync skill, to create or update this work's note in the vault, if
  the vault's conventions give this kind of work a note (the map may say which
  kinds do);
- the automation recommender, when the folder is a code repository;
- writing a local map, if this run had to discover its tools.

## What this skill does not do

- Create a claude.ai Project or upload files to one.
- Choose or adapt CLAUDE.md templates: the template picker does.
- Install plugins, connectors, hooks or MCP servers: the automation recommender
  proposes those, and the user decides.
- Edit the sources it links to. If a source is wrong, the skill says so and the
  user fixes it there.
