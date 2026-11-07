# Decision questions

The single batch of step 3. Send it in one round (one message, or one call of a
structured question tool that holds it all): the inventory first, then
the questions, each with a proposed answer and where the proposal came from.
The user should be able to reply "all fine except 4" and be done.

Leave out what step 1 or the user's request already settled; show it as settled
at the top instead, so the user can still correct it.

## Template

```
What I found
- <source>: <what kind of data it holds>  (<link or path>)
- <source>: ...
- Contradiction: <source A> says <x>, <source B> says <y>.
- Could not read: <source the map names or discovery found>, because <reason>.

Questions (proposed answer in each; change what is wrong)

1. Target: <claude.ai Project | Claude Code folder | both>.
   Proposed: <...>, because <...>.

2. Purpose: what is this workspace for, and what is it not for?
   Proposed: "<one sentence>". Not for: <...>.
   claude.ai Project only: name "<...>", description "<one line>".

3. Which source wins for each kind of data?
   (one row per kind the inventory found; these rows are only examples)
   - Tasks and status: <source>
   - Decisions and their reasons: <source>
   - Specs / design: <source>
   - Code and how to run it: <source>
   - <other kind found>: <source>
   - claude.ai Project only: how it reaches each source
     (connector | link | generated copy uploaded).

4. Permissions
   a. Without asking: <...>
   b. After a yes: <...>
   c. Only when asked: <...>
   - Claude Code folder only: also enforce part of this in
     .claude/settings.json? Proposed: <yes, narrow rules | no>.
   - Claude Code folder only: CLAUDE.md committed or kept local?
     Proposed: <committed | local>, because <...>.

5. Routines that start with a phrase
   - "<phrase>": <what it runs>
   - Any others?

6. Language and style
   - Drafts in: <language, per target if they differ>.
     Replies in: <the user's language | fixed language>.
   - claude.ai Project only: block tag names in <language>.
   - Tone and format: <...>
```

## What each question is for

**1. Target.** Decides which reference file the drafts follow and what the
delivery looks like. Ask only when step 1 could not decide.

**2. Purpose.** Becomes the role or opening of the instructions. The "not for"
half matters as much: it stops a Project for a newsletter from being used to
plan the whole business, and tells Claude when to say "this belongs elsewhere".

**3. Source of truth per kind of data.** The core of the workspace. Every kind of
data gets exactly one winning source; the drafts link to it and never restate
its content. Propose from the inventory: where a kind of data already lives and
is kept up to date is usually the right answer. Flag any kind that lives in two
places and ask which one wins; the other becomes a link or goes away.

**4. Permissions in three tiers.** What separates a helpful workspace from one
that either asks about everything or acts too freely. Typical proposals:

- *Without asking*: read any source; search; draft text in the chat; run
  read-only commands such as tests or a build.
- *After a yes*: create or change a file, page, note or task; install a
  dependency; commit.
- *Only when asked*: push, publish, send messages, delete anything, spend money.

Adjust to what the inventory shows (a vault the user curates by hand belongs in
"after a yes" even for small edits).

**5. Routines.** Fixed sequences the user starts with a short phrase, such as
opening a session by reading the status page, or closing it by writing a summary
to the vault. Propose only routines something already supports: a session log
or status page for this work, or routine skills the user has installed for every
project (say which kind each proposal is). Do not invent a ritual the user never
asked for.

**6. Language and style.** The drafts' language can differ from the replies'
(instructions in English, replies in the user's language, for instance). Ask
about formats to avoid as well as to use: tables, headings, length, labels.

## Proposing without inventing

A proposal needs a source: a file, a page, the map, something the user said,
or the typical defaults in this file (say so when a proposal is one).
When there is none, write "no proposal" and leave the field open. An open field
the user fills in costs a few seconds; a plausible wrong default the user skims
past costs every future conversation.
