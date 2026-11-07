# workspace-setup

A Claude skill that sets up the place where Claude will work on one piece of work: a claude.ai Project (custom instructions plus context documents), a Claude Code project folder (a `CLAUDE.md` and whatever else the folder needs), or both.

It is built on one rule: every fact lives in one place. A workspace links to its sources (a project manager, a notes vault, a repository, a design system) instead of copying them. When a copy cannot be avoided, it is marked as generated, with its source and date, and is regenerated rather than edited by hand.

## What it does

1. **Detects the target**: claude.ai Project, Claude Code folder, or both.
2. **Gathers what already exists** about the work (project manager, notes, repository, artifacts) before asking anything.
3. **Asks every decision question in one round**, each with a proposed answer and where it came from: purpose, which source wins for each kind of data, permissions in three tiers (without asking, after a yes, only when asked), routines started by a phrase, language and style.
4. **Drafts everything and shows it** before writing. Anything without a source is marked `PENDING`; nothing is invented.
5. **Offers a dry run** with a fresh agent that sees only the drafts, stating the cost before launching it.
6. **Delivers**: for claude.ai, the instructions to paste and the documents to upload, with the steps to create the Project (the skill cannot create it); for Claude Code, the files, written only after a yes.

It reuses the tools you already have instead of redoing their work: a CLAUDE.md template picker for the `CLAUDE.md`, a note-sync skill for a notes vault, an automation recommender for hooks and integrations, and an instruction-testing skill for the dry run. None of them is required.

## Local map

The skill holds the method; your setup goes in a **local map**: a short section, in your own instructions, that names your template picker, vault, project manager and style rules. In Claude Code, add a `workspace-setup local map` section to your user-level `CLAUDE.md`. Without a map, the skill discovers what the session can reach and offers to write one at the end. The format is in [`workspace-setup/references/local-map.md`](workspace-setup/references/local-map.md).

## Install

### Claude Code

Copy the `workspace-setup/` folder of this repository into your skills folder:

```bash
git clone https://github.com/alex20-create/workspace-setup-skill.git
mkdir -p ~/.claude/skills
cp -r workspace-setup-skill/workspace-setup ~/.claude/skills/
```

On Windows the skills folder is `%USERPROFILE%\.claude\skills\`. Start a new session so Claude picks up the skill.

### Claude apps

Download `workspace-setup.skill` from the latest release and upload it in the skills section of your Claude settings.

There is no hook and nothing runs on its own: the skill loads only when you ask for it.

## Use

Ask in your own words, for example:

- "Set up a workspace for my podcast in claude.ai."
- "Prepare the project folder for Claude Code."
- "Nuevo proyecto en claude.ai para la tesis."
- "Monta la carpeta del proyecto."

The skill replies in the language you write in.

## Files

| Path | What it holds |
|---|---|
| `workspace-setup/SKILL.md` | The six-step flow and the rules behind it |
| `workspace-setup/references/claude-ai-project.md` | Instructions in blocks, the sources map, generated copies, steps to create the Project |
| `workspace-setup/references/claude-code-folder.md` | Hand-off to a template picker, plain section order, permissions in settings, existing files |
| `workspace-setup/references/decision-questions.md` | The single batch of questions, with what each one is for |
| `workspace-setup/references/local-map.md` | Where the local map lives, its format, and discovery without one |
| `workspace-setup/evals/` | Test cases in the `claude plugin eval` layout |

## License

MIT. See [LICENSE](LICENSE).
