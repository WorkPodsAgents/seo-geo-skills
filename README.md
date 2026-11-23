# SEO and GEO skills for Claude, Codex and other AI agents

Two open-source agent skills by [WorkPods.ai](https://workpods.ai) that teach an AI agent how to
build websites that rank in search (SEO) and get cited in AI answers (GEO), and how to write the
copy for them without AI slop. They follow the open [Agent Skills](https://agentskills.io) format,
so the same folders work as Claude skills, Codex skills, Gemini CLI skills, Cursor skills and
GitHub Copilot skills.

We wrote them from what we learned rebuilding our own site. They work for any business and any
stack.

| Skill | What it does |
|---|---|
| [`seo-geo-website-design`](skills/seo-geo-website-design/SKILL.md) | SEO website design from the page plan up: one page per search intent, the SERP overlap test for keyword cannibalisation, page anatomy for homepages, service pages, guides, comparison and tool pages, a technical SEO checklist (server HTML, titles, canonicals, JSON-LD, redirects, AI crawlers, llms.txt, agent-usable forms), calm design, motion that keeps Core Web Vitals green, and a verification checklist. |
| [`seo-geo-content-writing`](skills/seo-geo-content-writing/SKILL.md) | SEO content writing and SEO copywriting: the page brief, answer-first sections that AI answers can quote, FAQ answers, sourced facts, bylines and internal link anchors, then a humanizer pass that removes AI writing tells while keeping facts and keywords intact. |

Use them together when you build a page: the design skill for structure and the technical layer,
the writing skill for the words.

## Install

### Claude Code

As a plugin from this repository's marketplace:

```text
/plugin marketplace add WorkPodsAgents/seo-geo-skills
/plugin install seo-geo-skills@seo-geo-skills
```

Or from a shell: `claude plugin marketplace add WorkPodsAgents/seo-geo-skills`, then
`claude plugin install seo-geo-skills@seo-geo-skills`.

Or copy the skill folders yourself, into `~/.claude/skills/` for all your projects or
`.claude/skills/` for one project:

```bash
git clone https://github.com/WorkPodsAgents/seo-geo-skills.git
cp -r seo-geo-skills/skills/* ~/.claude/skills/
```

Docs: [skills](https://code.claude.com/docs/en/skills),
[plugin marketplaces](https://code.claude.com/docs/en/plugin-marketplaces).

### Claude apps (claude.ai and desktop)

Turn on code execution in Settings, then zip each skill folder so the folder itself is at the top
of the zip, and upload it under Customize > Skills > + > Create skill > Upload a skill.

```bash
cd seo-geo-skills/skills
zip -r seo-geo-website-design.zip seo-geo-website-design/
zip -r seo-geo-content-writing.zip seo-geo-content-writing/
```

Docs: [using skills in Claude](https://support.claude.com/en/articles/12512180).

### OpenAI Codex

Copy the folders into `~/.agents/skills/` (all projects) or `.agents/skills/` in a repository:

```bash
mkdir -p ~/.agents/skills
cp -r seo-geo-skills/skills/* ~/.agents/skills/
```

Docs: [Codex skills](https://developers.openai.com/codex/skills).

### Gemini CLI

```bash
gemini skills install https://github.com/WorkPodsAgents/seo-geo-skills.git --path skills/seo-geo-website-design
gemini skills install https://github.com/WorkPodsAgents/seo-geo-skills.git --path skills/seo-geo-content-writing
```

Or copy the folders into `~/.gemini/skills/` or `.gemini/skills/` (`.agents/skills/` also works).
Docs: [Gemini CLI skills](https://geminicli.com/docs/cli/skills/).

### Cursor

Copy the folders into `.cursor/skills/` in a project or `~/.cursor/skills/` for all projects.
Cursor also reads `.agents/skills/` and `.claude/skills/`. Docs:
[Cursor skills](https://cursor.com/docs/context/skills).

### GitHub Copilot

With GitHub CLI 2.90 or later (`gh skill` is in public preview):

```bash
gh skill install WorkPodsAgents/seo-geo-skills --all
```

Or copy the folders into `.github/skills/` in a repository, or `~/.copilot/skills/` for all your
projects. Skills work in Copilot CLI, the Copilot cloud agent and agent mode in VS Code. Docs:
[about agent skills](https://docs.github.com/en/copilot/concepts/agents/about-agent-skills),
[VS Code agent skills](https://code.visualstudio.com/docs/copilot/customization/agent-skills).

### Any agent, with one command

The open-source [`skills`](https://github.com/vercel-labs/skills) installer copies the skills into
the right folder for Claude Code, Codex, Cursor, Gemini CLI, Copilot and others:

```bash
npx skills add WorkPodsAgents/seo-geo-skills
```

### ChatGPT and other chat assistants without skills

Paste the contents of a `SKILL.md` into the custom instructions of a project or custom GPT (or at
the start of a chat), then paste a file from its `references/` folder when the steps point to it.
The skills are plain Markdown, so nothing else is needed.

## How the skills load

Each `SKILL.md` starts with a short `name` and `description`. The agent reads only those until a
task matches, then reads the full `SKILL.md`, and opens the files in `references/` only when a step
needs them. That keeps the agent's context small. See [AGENTS.md](AGENTS.md) for how other agents
should use this repository.

## What is inside

```text
skills/
  seo-geo-website-design/
    SKILL.md
    references/
      intent-and-page-plan.md   keyword-to-page mapping and the SERP overlap test
      page-anatomy.md           section order by page type, FAQs, bylines
      technical-seo.md          crawlability, redirects, AI crawlers, llms.txt, forms
      structured-data.md        JSON-LD by page type, with examples
      design-and-motion.md      calm design, contrast, deferred motion with reference code
      verification.md           the checklist to run before a page ships
      sources.md                where each claim was checked
  seo-geo-content-writing/
    SKILL.md
    references/
      page-brief.md             the brief template and a worked example
      humanizer.md              the AI writing tells and the review checklist
      sources.md
```

## Credits

The humanizer pass in `seo-geo-content-writing` is adapted from
[blader/humanizer](https://github.com/blader/humanizer) by Siqi Chen (MIT licence), which is based
on Wikipedia's [Signs of AI writing](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing).
See [NOTICE](NOTICE).

## Licence

MIT, copyright WorkPods.ai. See [LICENSE](LICENSE).

## About WorkPods.ai

WorkPods.ai is an AI SEO agency. We also publish
[Agent Ready](https://github.com/WorkPodsAgents/agent-ready), a free tool that checks a site for
SEO, GEO and AI agent readiness. Questions or fixes: open an issue, or write to
yours@workpods.ai.
