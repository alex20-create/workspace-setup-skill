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
- the purpose and the "not for" from step 3, with how long the work will be
  kept up and whether a record of its decisions already exists;
- the source of truth for each kind of data, with links or paths;
- the three permission tiers and the routines, and whether the `CLAUDE.md` is
  committed or kept local;
- the language and style choices;
- the inventory from step 2, including any existing `CLAUDE.md`, `AGENTS.md` or
  README it should migrate from or respect;
- what the map says about the `CLAUDE.md` itself: the house order of sections,
  a starting template, a size budget.

Let it choose, compare and fill the template. Its own list-and-confirm step
folds into step 4: its reasons for the choice are shown with the draft, once.
Then check its draft against the rules of this skill before showing it: one
place per fact, links instead of copies, the gap marker for gaps, the house
order of sections if the map or the user's own instructions give one, and the
rules in "Keeping it light" below. Report any mismatch with the template
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
5. **Current state**: what is true now and cannot be read from the files,
   plus a pointer to where status lives; not the status itself, and no history.
6. **Pending**: the `PENDING` items, until they get a source.

When the house order from the map has no section for permissions and routines,
put them in the closest one (usually Conventions) rather than adding a section
the house order lacks.

A short CLAUDE.md that points well beats a long one that restates. If a section
would only repeat a source, replace it with the link.

## Keeping it light

Claude Code loads the whole `CLAUDE.md` into every session of the folder,
whether or not the session needs what it says. Every line is paid for each
time, so these rules apply to any draft, whoever wrote it:

- **A budget in bytes, not lines.** A few very long lines weigh as much as many
  short ones, and a line limit does not see them. Use the figure the map or the
  user's instructions give; without one, aim for 8 KB or less (about 2,000
  tokens) and treat 10 KB as the ceiling. Measure the draft and state its size
  when showing it. Over the ceiling, say what would move out and where.
- **Current state is the present only.** Tasks and progress stay in the source
  that won them in step 3, behind its link. What merged or closed does not pile
  up in the `CLAUDE.md` either: it goes to one history file in the folder
  (`docs/history.md`, for example, or the one a history template set up) and
  the `CLAUDE.md` keeps one line saying when to read it.
- **Long procedures live in their own file.** Anything longer than about five
  lines (how to log a history entry, how to publish, how to rebuild something)
  gets a file and a one-line pointer that says when to read it.
- **Nothing that already loads from above.** A user-level `CLAUDE.md` and the
  `CLAUDE.md` of any folder that contains this one load too. Read them, leave
  out what they already say, and tell the user what was left out and where it
  lives. In a folder several people share, a user-level file is one person's:
  what the whole team needs stays in the folder's `CLAUDE.md`.
- **Nothing about the tool.** Template sections that explain how Claude Code
  works in general (tables of context or memory layers) are not about this
  work, and instructions to mirror the file's content somewhere else that also
  loads every session break the one-place rule. Leave both out.
- **Rules for one area go with that area.** Detail that matters only when
  touching one part of the work goes to its own file, with a pointer such as
  "before touching the export, read `docs/export.md`", or to a rule file under
  `.claude/rules/` with `paths` in its frontmatter, which loads only when
  matching files are worked on.
- **The rule travels in the file.** A `CLAUDE.md` rarely starts large; it grows
  session by session, as each one records what it did. Put the budget and the
  two rules on current state and procedures in an HTML comment at the top of
  the file, where whoever edits it next will see them. Claude Code strips
  block-level HTML comments before loading the file, so the comment costs
  nothing per session.

When the folder already has a `CLAUDE.md` over the budget, do not trim it
silently: state its size, name what is history, procedure or repetition, and
propose where each part would go ("Existing files" below still applies).

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

## Plugins only this folder needs

A plugin enabled for the whole user account adds its skills and tools to every
session in every folder. This skill does not choose or install plugins, but
when one comes up that only this work needs (the user names it in step 3, or
accepts it from the automation recommender in step 6), say that it can be
enabled for this folder alone: `enabledPlugins` in `.claude/settings.json` if
everyone who works in the folder should get it, or in
`.claude/settings.local.json` for this user only.

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
folder. When the folder is not a repository, say so in the step 2 inventory
and leave the question open: there is nothing to commit to yet, and creating a
repository is the user's decision.

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
