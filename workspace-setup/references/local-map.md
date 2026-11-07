# Local map

The skill holds the method; the local map holds the user's setup. Keeping them
apart lets the same skill work on any machine and keeps personal paths, names
and preferences out of a skill that may be shared.

## Where it lives

| Environment | Place |
|---|---|
| Claude Code | A `workspace-setup local map` section in the user-level `CLAUDE.md` (or a workspace-level one, if the setup is per workspace). |
| claude.ai, packaged skill | A `Local map for this install` section inserted into this skill's `SKILL.md` when it was packaged for one person. |
| claude.ai Project | The custom instructions of the Project being built or revised, if they name the tools below. The instructions of another Project the session happens to run in govern behaviour only, not this map. |

If more than one exists, read them all and, line by line, the most specific
wins: Project instructions, then the workspace `CLAUDE.md`, then the user-level
one, then the packaged section. Read `CLAUDE.md` files from disk where you can:
a copy loaded into the session at its start can predate an edit.

## What it holds

Only what this skill needs; anything else belongs elsewhere. A map packaged
for claude.ai may also carry rules shared by all of a user's skills; this skill
uses only the lines that bear on it.

```markdown
# workspace-setup local map
Read by the `workspace-setup` skill (section "Local map first"); it overrides the skill's defaults.
- CLAUDE.md template picker: `<skill name>`; template collection in `<path>`.
- House order of CLAUDE.md sections: <A, B, C...>.
- Notes vault: `<path>`; project notes in `<folder pattern>`; kept by `<note-sync skill>`.
- Project manager: <tool>, <database or page>.
- Automation recommender: `<skill name>`, for code repositories.
- Dry run of instructions: `<skill name>`.
- Drafts: <language and style rules>; gap marker `<PENDING word>`.
- Workspaces that show what works: <name>: <what makes it work>.
```

Leave out a line that has no answer, or mark it `PENDING` if the user means to
fill it later.

## Discovery, when there is no map

Look at what this session can actually reach, and match it to the roles above:

- **Skills**: the list of available skills. A skill whose description mentions
  CLAUDE.md templates is a template picker; one that syncs notes to a vault is a
  note-sync skill; one that recommends hooks, skills or MCP servers is an
  automation recommender; one that dry-runs instructions with a fresh agent is
  an instruction tester. If the session lists skills by name only, read their
  descriptions (a skill-listing tool, or each skill's own `SKILL.md`) before
  giving one a role; a name alone is a guess. Where a template picker keeps its
  template collection is that skill's business: record it if seen, but
  discovery does not need it.
- **Connectors**: project managers, document stores, design tools. Each is a
  candidate source for some kind of data. Where no tool lists connectors, infer
  them from the names of the tools the session offers.
- **Files**: in Claude Code, the user-level and workspace `CLAUDE.md`, the
  current folder, and any folder they point to (a vault, a template
  collection).

Say in the step 2 inventory what was found and what each piece was assumed to
be. Do not guess paths
that were not seen.

## Offering to write the map

At the end of a run that had to discover, offer to write the map with what was
found and what the user confirmed in step 3. Show the section first. Write it
only on a yes, and only in Claude Code, where the user-level `CLAUDE.md` is a
file this session can reach. In claude.ai, give the section as text and say
where it would go (Project instructions, or the user's own notes for the next
time the skill is packaged).
