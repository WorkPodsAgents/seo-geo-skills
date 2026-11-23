---
name: seo-geo-website-design
description: >-
  Plan, build and check web pages that rank in search and get quoted in AI answers (SEO and GEO).
  Covers keyword-to-page mapping and the cannibalisation test, page anatomy for homepages, service
  pages, guides, comparison and tool pages, technical SEO (server HTML, titles, canonicals,
  JSON-LD, redirects, llms.txt, AI crawlers, agent-usable forms), calm design, motion that does
  not hurt Core Web Vitals, and a verification checklist. Use when designing or building a
  website, landing page or page template, planning a site structure, doing an SEO website
  redesign, writing a technical SEO checklist, or reviewing a page before launch.
license: MIT
metadata:
  author: WorkPods.ai
  homepage: https://workpods.ai
  version: "1.0.0"
---

# SEO and GEO website design

By WorkPods.ai. This skill is what we learned rebuilding our own site so that search engines rank
it, AI answers quote it, and AI agents can use it. It works for any business and any stack.

SEO here means ranking in classic search results. GEO (generative engine optimization) means being
cited or named in AI answers such as Google's AI Overviews, ChatGPT, Gemini and Perplexity. Both
reward the same base: one clear page per intent, every word in the HTML, and answers a machine can
lift without rewriting.

## How to use this skill

Work through the five steps in order. Each step names a reference file with the detail; load it
when you reach that step.

1. Map intent to pages. See [references/intent-and-page-plan.md](references/intent-and-page-plan.md).
2. Pick the page anatomy for the page type. See [references/page-anatomy.md](references/page-anatomy.md).
3. Build the technical layer. See [references/technical-seo.md](references/technical-seo.md) and
   [references/structured-data.md](references/structured-data.md).
4. Design and add motion without slowing the page. See
   [references/design-and-motion.md](references/design-and-motion.md).
5. Verify before you call the page done. See [references/verification.md](references/verification.md).

For the words on the page, use the companion skill `seo-geo-content-writing`. Sources for the
claims in this skill are in [references/sources.md](references/sources.md).

If you lack data you need (search volumes, the current top 10 for a query, the site's analytics),
ask the person for it or say what is missing. Never invent keyword volumes, rankings or results.

## Step 1: one page per search intent

A page should answer one search intent. Two pages chasing the same intent split their signals and
often both rank worse. Before building anything, write a term ownership table: each target search
term has exactly one owner page.

Decide whether two terms are one intent with the SERP overlap test. Pull the top 10 organic
results for each term in the target country and count the domains they share.

| Shared top-10 domains | Meaning | Action |
|---|---|---|
| 4 or more of 10 | Search engines treat them as one intent | One page targets both |
| 2 to 3 | Related | One page can carry the second as a secondary term |
| 0 to 1 | Different intents | Separate pages |

Without keyword data, pick a provisional primary term from the business's category, location and
main offer, and flag it as provisional until real data confirms it.

When an existing page competes with a more important page, retarget it to a term nobody owns
instead of letting the two fight. Then link pages in hub and spoke clusters: each supporting page
links to the page it supports, and every internal link uses the target page's own term as its
anchor text.

## Step 2: page anatomy by type

| Page type | H1 | H2s | Questions |
|---|---|---|---|
| Homepage | Category + audience + outcome | Declarative capabilities and differentiators | Only in a bottom FAQ of up to 6 |
| Service page | Names the service | Declarative capabilities | Only in a bottom FAQ of up to 6 |
| Guide | The question or topic | Questions, each answered in its first two sentences | The H2s are the questions |
| Comparison | "X vs Y" | Criteria, then a table | Bottom FAQ |
| Tool page | What the tool does | What it checks, how to use it | Bottom FAQ |

Commercial pages lead with positioning. Question headings on a homepage dilute what the page is
about, slow down a buyer who already knows what they want, and compete with the guides that own
those questions. FAQ answers are 40 to 60 words, and the first sentence answers the question.
Never invent questions: without search or customer data, derive them from the business's facts,
mark them provisional, and ship fewer than four if fewer hold up. Leave out any section or schema
property (proof, team, logo, founder, `sameAs`) whose facts are missing.

On every page type, the first two sentences of each section answer that section on their own.
AI answers quote short, self-contained passages, so write each section opening as if it will be
lifted out of the page.

## Step 3: the technical layer

The short list (detail in the references):

- Every word is in the server-rendered HTML. Nothing is hidden until a script runs. Many AI
  crawlers do not run JavaScript.
- One H1, no skipped heading levels.
- A unique title of about 30 to 60 characters and a meta description of about 70 to 160.
- One absolute, self-referencing canonical URL, or `noindex` for pages that should not rank.
- A visible breadcrumb on every page below the homepage, matched by `BreadcrumbList` JSON-LD.
- JSON-LD for the page type. `FAQPage` only when the FAQ is visible on the page.
- Bylines with a real author and reviewer who link to profile pages.
- Images with `alt`, `width` and `height`.
- Retired URLs return 301 to a successor or 410 when there is none, and internal links,
  canonicals, the sitemap and `llms.txt` change in the same release.
- Forms have real labels, so people and agents can fill them in.

## Step 4: calm design and motion that costs nothing

- Calm and uncluttered: short sections, generous space, one idea per section and per visual.
- One CTA colour, used for every primary action and for nothing else. Text links get a different
  colour.
- Illustrations act out the section's idea with a few labels, never paragraphs.
- Prefer a few large panels to grids of identical cards.
- Every text and background pair passes WCAG AA contrast, including small labels on dark themes.
- On phones, the section label and heading come before the illustration.
- Static content renders first. Animation loads after the `load` event and an idle callback, is
  off for reduced motion and data saver, and draws into fixed-size slots so layout never shifts.
  Each slot holds the finished icon as inline SVG, so a reader without motion sees it complete.

## Step 5: verify

Run the checklist in [references/verification.md](references/verification.md) on every page before
reporting it as done, and report the results with the numbers. Fix every failure. Report a gap
(a fact only the person can supply, such as a photo or a quote) instead of faking it. Default targets for a marketing
page in Lighthouse mobile: LCP 2.0 s or less, TBT 100 ms or less, CLS 0.05 or less. These are
stricter than Google's Core Web Vitals "good" thresholds on purpose, because lab runs on a fast
machine flatter real phones.

## What not to do

- Do not give two pages the same primary keyword, title or H1.
- Do not put buyer questions as H2s on a homepage or service page.
- Do not add `FAQPage` markup without a visible FAQ, or any markup that says something the page
  does not show.
- Do not render content only on the client, or hide it with CSS until a script adds a class.
- Do not invent facts, clients, logos, numbers, reviews or authors for a page. Leave a gap and say
  what is needed.
- Do not ship motion that moves layout, blocks the main thread at load, or ignores
  `prefers-reduced-motion`.
