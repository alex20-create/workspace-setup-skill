# Claude Code project folder

What a folder needs for Claude to work well in it is usually small:

- **`CLAUDE.md`** at the folder root. Claude Code loads it at the start of every
  session, so it carries what Claude must know every time: what the work is,
  where each kind of data lives, how to run things, the permissions and the
  routines.
- **`.claude/settings.json`**, optional: permission rules that enforce part of
  the three tiers (see below).

Nothing else by default. Hooks, skills, slash commands and MCP servers are the
automation recommender's field (step 6 offers it); proposing them here would
duplicate it.

## CLAUDE.md through the template picker

When the local map names a CLAUDE.md template picker, or discovery found one
(a skill whose description covers choosing CLAUDE.md templates), it writes the
CLAUDE.md. Hand it:

- the target folder's path;
- the purpose and the "not for" from step 3;
- the source of truth for each kind of data, with links or paths;
- the three permission tiers and the routines;
- the language and style choices;
- the inventory from step 2, including any existing `CLAUDE.md`, `AGENTS.md` or
  README it should migrate from or respect.

Let it choose, compare and fill the template. Then check its draft against the
rules of this skill before showing it: one place per fact, links instead of
copies, the gap marker for gaps, and the house order of sections if the map or
the user's own instructions give one. Report any mismatch with the template
picker's draft to the user rather than silently rewriting it.

## CLAUDE.md without a template picker

Write it directly. Use the house order of sections from the local map or the
user's own instructions; without one, this plain order:

1. **Stack**: what the work is made of (languages, frameworks, tools), or for
   non-code work, the medium and tools.
2. **Commands**: how to run, test, build; or the equivalent fixed actions.
3. **Conventions**: naming, structure, language of persisted text, and the
   "where each thing lives" table.
4. **Permissions and routines**: the three tiers and each trigger phrase.
5. **Current state**: a pointer to where status lives, not the status itself.
6. **Pending**: the `PENDING` items, until they get a source.

When the house order from the map has no section for permissions and routines,
put them in the closest one (usually Conventions) rather than adding a section
the house order lacks.

A short CLAUDE.md that points well beats a long one that restates. If a section
would only repeat a source, replace it with the link.

## Permissions in settings

The three tiers map only partly onto Claude Code's permission rules:

| Tier | In `.claude/settings.json` | In `CLAUDE.md` |
|---|---|---|
| Without asking | `allow` rules for the exact commands (tests, build, read-only git) | Listed as allowed |
| After a yes | `ask` rules for commands that change things | Listed, with "ask first" |
| Only when asked | `deny` only for what must never run unprompted | Listed; settings cannot tell "asked" from "not asked" |

Offer the settings file as an option, show it as a draft like everything else,
and keep rules narrow (a specific command, not a whole tool). Personal or
machine-only rules go in `.claude/settings.local.json`, which should not be
committed.

## Existing files

Never overwrite an existing `CLAUDE.md`, settings file or README. Show the
proposed change as a diff, say what is kept and what moves, and write only on a
yes. User-written content in an existing CLAUDE.md is kept unless the user says
otherwise.

## Tracked or local

Whether the `CLAUDE.md` is committed is the user's choice, and it matters most
in a public repository: a committed file is published with the next push. The
alternative is a local file kept out of git (Claude Code also reads a
`CLAUDE.local.md`, meant for that). Step 3 asks this for every Claude Code
folder.

## Generated copies in a folder

If a file in the folder must copy content from elsewhere, it starts with:

```markdown
<!-- Generated from <source> (<link or path>) on <YYYY-MM-DD>.
     Do not edit by hand; regenerate from the source. -->
```

and the CLAUDE.md says which files are generated and how to regenerate them.

## Delivery

After the user approves the drafts: write each file and list every path
written. Committing, pushing or opening a pull request happens only if the user
asks. The follow-up offers (note-sync, automation recommender, local map) are
in step 6 of `SKILL.md`.
