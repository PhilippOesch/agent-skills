---
name: mermaid
description: Generate a self-contained HTML page rendering a mermaid diagram.
disable-model-invocation: true
---

Scaffold a mermaid diagram as a single self-contained HTML page — mermaid loaded from CDN, opened directly in a browser.

**Temp folder:** `${TMPDIR:-/tmp}/mermaid-skill/` — intermediate artifacts are written here and cleaned up automatically.

1. **Pick the type.** Choose the keyword from the toolbox below — use the one the request names; if none obviously fits, ask me. Done when you have a keyword.
2. **Write the mermaid source and a 1–3 sentence description.** The description must explain what the diagram shows well enough to be understood without reading the source. Done when the source starts with the chosen keyword, covers everything requested, and the description is present.
3. **Validate and auto-correct.** Pipe the source into the CLI for a dry-run parse:

```bash
printf '%s\n' "$source" | npx @mermaid-js/mermaid-cli -o - -e svg -q > /dev/null --input -
```

Exit 0 → valid, proceed to step 4. Exit 1 → capture stderr, inspect the parse error, apply a targeted fix, and retry. Auto-fix at most 3 times. After 3 failed attempts: write the raw source to `${TMPDIR:-/tmp}/mermaid-skill/<kebab-case-name>.mmd`, show the stderr output, and ask me for the corrected source; then re-enter validation. Done when `mmdc` exits 0.
4. **Render the page.** Ensure `docs/diagrams/` exists in the current working directory, then copy `template.html` (next to this file) to `docs/diagrams/<kebab-case-name>.html`, replacing `{{TITLE}}`, `{{DIAGRAM}}`, and `{{DESCRIPTION}}`. Done when the file exists and no placeholders remain. Then give me the path and offer to `open` it.

## Toolbox

| Keyword                                                                    | Draws                                            |
| -------------------------------------------------------------------------- | ------------------------------------------------ |
| `flowchart`                                                                | processes, decisions, dependencies               |
| `sequenceDiagram`                                                          | messages between actors over time                |
| `classDiagram`                                                             | UML classes and relationships                    |
| `stateDiagram-v2`                                                          | states and transitions                           |
| `erDiagram`                                                                | entities and relationships (data models)         |
| `gantt`                                                                    | project schedule: tasks, durations, dependencies |
| `journey`                                                                  | user journey with satisfaction scores            |
| `pie`                                                                      | proportions of a whole                           |
| `quadrantChart`                                                            | items positioned on two axes                     |
| `requirementDiagram`                                                       | requirements and their verification links        |
| `gitGraph`                                                                 | branches, commits, merges                        |
| `C4Context` / `C4Container` / `C4Component` / `C4Dynamic` / `C4Deployment` | software architecture at increasing zoom         |
| `mindmap`                                                                  | hierarchical brainstorm                          |
| `timeline`                                                                 | chronological events                             |
| `sankey-beta`                                                              | flows sized by magnitude                         |
| `xychart-beta`                                                             | bar and line charts                              |
| `block-beta`                                                               | labeled block layouts                            |
| `packet-beta`                                                              | network packet structure                         |
| `kanban`                                                                   | board columns with cards                         |
| `architecture-beta`                                                        | cloud/service architecture                       |
| `radar-beta`                                                               | multi-axis comparison                            |

Syntax details for a keyword: context7 `/mermaid-js/mermaid`, or https://mermaid.js.org/intro/
