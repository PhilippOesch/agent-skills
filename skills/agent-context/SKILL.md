---
name: agent-context
description: Save and retrieve agent-generated knowledge in the configured Obsidian agent-context folder. Use when writing plans, research, reference material, handoff notes, or looking up stored knowledge.
---

# agent-context

Goal: keep agent-generated knowledge in one configured place outside the current repo, using consistent naming and frontmatter.

Done when the correct file exists in `<agentContextPath>/<folder>/` with valid frontmatter.

## Steps

1. **Read config**
   - Path: `~/.config/agent-context-config.json`.
   - Read `knowledge.agentContextPath` and `knowledge.folders`.

2. **Choose folder**
   - `plan` → `10-plans/`
   - `research` → `20-research/`
   - `reference` → `30-reference/`
   - `handoff` → `40-handoff/`
   - `inbox` → `00-inbox/` for unsure or unprocessed output.
   - `archive` → `99-archive/` for outdated notes.

3. **Name the file**
   - Pattern: `<yyMMddHHmm>-<slug>.md`.
   - Timestamp: `yyMMddHHmm` (10 digits, sortable, human-readable date).
   - Slug: lower-case, hyphenated title. Keep it short.

4. **Write frontmatter**
   Include these fields:
   - `id`: same as the timestamp prefix.
   - `type`: one of the folder keys above.
   - `audience`: `both` (default), `agent`, or `human`.
   - `status`: `draft` (default), `review`, `final`, or `archived`.
   - `created`: ISO date.
   - `tags`: list of relevant tags.
   - `source`: prompt or skill that produced the note.

5. **Save the body**
   - Write the content after the frontmatter.
   - Do not write to the user's curated `zettelkasten/` unless explicitly asked.

## Lookup

- When the user asks to "look up" something, search `<agentContextPath>` first.
- Move outdated notes to `archive` rather than deleting.
