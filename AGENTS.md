# AGENTS.md

This repository holds two Agent Skills by WorkPods.ai in the open Agent Skills format
(https://agentskills.io). Each skill is a folder with a `SKILL.md` (YAML front matter, then
instructions) and a `references/` folder with longer material to read only when a step needs it.

| Skill | Use it when |
|---|---|
| `skills/seo-geo-website-design/` | planning a site structure, designing or building a page or template, a technical SEO review, or checking a page before launch |
| `skills/seo-geo-content-writing/` | writing or editing page copy, FAQs, titles and descriptions, or humanizing text |

## For an agent reading this repository

1. Read the front matter `description` of each `SKILL.md` and pick the skill that matches the task.
   Use both when you are building a page and writing its words.
2. Read that `SKILL.md` in full and follow its steps in order.
3. Open a file in `references/` only when the step you are on points to it.
4. Do not invent facts, numbers, clients, quotes or authors while following a skill. Ask for what
   is missing.

## Installing for a specific tool

See the install section of [README.md](README.md). In short, copy or link each skill folder into
the folder your tool scans:

| Tool | Project folder | User folder |
|---|---|---|
| Claude Code | `.claude/skills/` | `~/.claude/skills/` |
| OpenAI Codex | `.agents/skills/` | `~/.agents/skills/` |
| Gemini CLI | `.gemini/skills/` or `.agents/skills/` | `~/.gemini/skills/` or `~/.agents/skills/` |
| Cursor | `.cursor/skills/` or `.agents/skills/` | `~/.cursor/skills/` or `~/.agents/skills/` |
| GitHub Copilot | `.github/skills/` or `.agents/skills/` | `~/.copilot/skills/` or `~/.agents/skills/` |

## Editing these skills

- Keep each `SKILL.md` under 500 lines; move detail into `references/`.
- `name` must match the folder name (lowercase letters, digits and hyphens).
- Keep the `description` specific: what the skill does and when to use it.
- Write in plain, humanized prose: no em or en dashes, none of the banned words listed in the
  content skill.
- Every claim about a search engine, tool or format must be true today and listed in the skill's
  `references/sources.md`.
- Examples use fictional businesses and say so.
