# claude.ai Project

A claude.ai Project has two parts that matter here:

- **Instructions**: text that reaches every conversation in the Project, in
  full. Keep it to what Claude must know every time.
- **Project knowledge**: uploaded files Claude can consult. When there is a lot
  of it, Claude may retrieve only the parts that look relevant, so a small,
  well-labelled set works better than a large pile.

Both stay as they were uploaded until someone changes them by hand. That is why
anything that changes often (status, task lists, figures) does not belong in
either: point to the source instead.

## Instructions: blocks with one job each

Instructions written as named blocks are easy for Claude to follow and easy for
the user to edit later, because each block has one job. XML-style tags work
well. A proven set:

| Block | What goes in it |
|---|---|
| `role` | Who Claude is in this Project and what the work is for; what it is not for. |
| `where_each_thing_lives` | One line per kind of data: the winning source, its link or path, and what Claude does there (read only, or edit after a yes). |
| `structure` | How the work is organised: phases, areas, naming, what a finished piece looks like. Only what is stable. |
| `routines` | Each trigger phrase and the steps it runs. |
| `permissions` | The three tiers: without asking, after a yes, only when asked. |
| `response_style` | Language, tone, formats to use and to avoid. |

Name the tags in the drafts' language if the user prefers (a Spanish Project
might use `rol`, `donde_vive_cada_cosa`, `estructura`, `rutinas`, `permisos`,
`forma_de_responder`); the local map may say which. Drop a block that would be
empty rather than filling it with generic advice.

Skeleton:

```xml
<role>
You help with <work>. Purpose: <one sentence>. Not for: <...>.
</role>

<where_each_thing_lives>
- Tasks and status: <source>, <link>. Read it at the start; never restate it here.
- Decisions: <source>, <link>.
- Design: <source>, <link>.
- Anything not listed: ask before assuming a source.
</where_each_thing_lives>

<structure>
...
</structure>

<routines>
- "<phrase>": 1) ... 2) ... 3) ...
</routines>

<permissions>
- Without asking: ...
- After a yes: ...
- Only when asked: ...
</permissions>

<response_style>
...
</response_style>
```

Writing them:

- Say why a rule exists when it is not obvious; Claude applies a reason better
  than a bare order.
- Each fact appears once. If two blocks need it, one states it and the other
  points to it.
- No secrets, keys or passwords. No personal data the work does not need.
- The gap marker from `SKILL.md` (`PENDING: <what is missing>`, or its
  equivalent in the drafts' language) for anything without a source.

## Context documents: a map, not a copy

The usual context document is one **map**: a short file listing the sources and
how to reach them, without copying their content.

```markdown
# <Work> sources map

| Kind of data | Source | Link | Notes |
|---|---|---|---|
| Tasks and status | <project manager> | <url> | Read at session start |
| Decisions | <vault note> | <path> | Settled ones only |
| Design system | <design source> | <url> | Tokens and components |
```

A source the Project can reach only through the user's linked computer gets its
full path in the map and a note that it is readable only in a linked chat.

Add more documents only when a source cannot be reached from the Project at all
(no connector, no web access) and Claude needs the content to work. Such a copy
starts with a generated header and is replaced, never edited, when the source
changes:

```markdown
> Generated from <source> (<link or path>) on <YYYY-MM-DD>.
> Do not edit by hand; regenerate from the source.
```

If the user would have to refresh a copy so often that it is always stale, say
so and suggest connecting the source instead.

## Delivery

Give the user:

1. The instructions as one block, ready to paste.
2. Each context document as a file to upload, or as a block to save as a
   `.md` file.
3. The steps, said plainly, because this skill cannot create the Project:
   1. In claude.ai, open **Projects** and create a new project with a name and a
      short description.
   2. Open the project's instructions setting and paste the instructions.
   3. Add the context documents to the project's knowledge (upload the files).
   4. Make sure the connectors the instructions rely on are enabled when
      chatting in the Project.
   5. Start a conversation with one of the routine phrases to check it works.

Interface labels change over time; describe the step by what it does if a label
differs.
