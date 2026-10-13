---
name: handoff
description: Compact the current conversation into a handoff document for another agent to pick up. Use when the user asks for a handoff, session summary, or context to continue later.
argument-hint: "What will the next session be used for?"
disable-model-invocation: true
---

# handoff

Goal: write a handoff document so a fresh agent can continue the work.

Done when the handoff file is saved to the configured agent-context folder.

## Steps

1. **Read config**
   - Path: `~/.pi/agent/pi-mp-my-agent.json`.
   - Read `knowledge.agentContextPath` and `knowledge.folders.handoff`.

2. **Create the handoff note**
   - Folder: `<agentContextPath>/<handoff-folder>/` (usually `40-handoff/`).
   - Filename: `<yyMMddHHmm>-<slug>.md`.
   - Slug: lower-case, hyphenated summary of the topic.

3. **Write frontmatter**
   Include these fields:
   - `id`: same as the timestamp prefix.
   - `type`: `handoff`.
   - `audience`: `agent`.
   - `status`: `draft`.
   - `created`: ISO date.
   - `tags`: relevant tags.
   - `source`: `handoff`.

4. **Write the body**
   Include:
   - What was being done and why.
   - Decisions made, with links to related notes or artifacts.
   - Open questions and blockers.
   - Suggested next steps.
   - Suggested skills the next agent should invoke.

Do not duplicate content already captured in other artifacts (specs, plans, ADRs, issues, commits, diffs). Reference them by path or URL instead.

Redact any sensitive information, such as API keys, passwords, or personally identifiable information.

If the user passed arguments, treat them as a description of what the next session will focus on and tailor the doc accordingly.
