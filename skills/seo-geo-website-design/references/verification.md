# Verification checklist

Run this on every page before calling it done. Report each item as passed or failed, with the
measured numbers. A page with any failure is not done.

## Contents

- Intent and content
- HTML and crawlability
- Structured data
- Links
- Speed and stability
- Accessibility and design
- Agents and AI answers
- Free tools

## Intent and content

- [ ] The page owns one primary term, and no other page targets it (check the ownership table).
- [ ] The primary term is in the title, H1 and first sentence.
- [ ] Every section's first two sentences answer it on their own.
- [ ] Commercial pages use declarative H2s and a bottom FAQ of 4 to 6; guides use question H2s.
- [ ] FAQ answers are 40 to 60 words, first sentence answers.
- [ ] Every number has a source and date; nothing is invented.
- [ ] Author and reviewer are real people, unchanged from the source.

## HTML and crawlability

- [ ] With JavaScript disabled (or with `curl`), every word of the page is present and readable.
- [ ] No CSS hides content unless a script-added class gates it.
- [ ] Exactly one H1; no skipped heading levels.
- [ ] Title about 30 to 60 characters, description about 70 to 160, both unique on the site.
- [ ] One absolute self-referencing canonical, or `noindex` for pages that should not rank.
- [ ] The page is in the sitemap (if indexable) and `llms.txt` links are current.
- [ ] `og:title`, `og:description` and a 1200 x 630 `og:image` are present.
- [ ] Every image has `alt`, `width` and `height`.

## Structured data

- [ ] JSON-LD parses and has `"@context": "https://schema.org"`.
- [ ] The types match the page type (structured-data.md), with `BreadcrumbList` below the homepage.
- [ ] `FAQPage` only if a visible FAQ shows the same questions and answers.
- [ ] Google's Rich Results Test and the Schema Markup Validator report no errors.

## Links

- [ ] No internal link returns a redirect or an error; every `#anchor` target exists.
- [ ] The page is linked from at least three other pages, including its hub, and is within two or
      three clicks of the homepage.
- [ ] Guides link to the commercial page they support.
- [ ] Internal anchor text uses the target page's own term.
- [ ] Retired URLs return 301 to a successor or 410.

## Speed and stability

Run Lighthouse in mobile mode (the default emulates a mid-range phone on a slow 4G connection with
a 4x CPU slowdown) at least three times and report the median:

- [ ] LCP 2.0 s or less.
- [ ] TBT 100 ms or less (TBT is the lab stand-in for INP).
- [ ] CLS 0.05 or less.
- [ ] JavaScript loaded before `load` is within the up-front budget (about 5 KB gzip on marketing
      pages); deferred JavaScript is within its agreed budget.
- [ ] Once the site has real traffic, check field data (Chrome UX Report in PageSpeed Insights or
      Search Console): LCP 2.5 s, INP 200 ms and CLS 0.1 or better at the 75th percentile.

## Accessibility and design

- [ ] Every text and background pair passes WCAG AA (4.5:1 normal text, 3:1 large text and UI).
- [ ] One CTA colour for every primary action, used for nothing else.
- [ ] Keyboard: every interactive element is reachable and visibly focused.
- [ ] Animation is off with `prefers-reduced-motion: reduce` and with data saver.
- [ ] With motion off, every motion slot shows its finished SVG, not an empty box, and meaningful
      labels are HTML text.
- [ ] On a 390 px wide phone: no horizontal scroll, nothing clipped, label and heading above each
      illustration.
- [ ] Zero console errors.

## Agents and AI answers

- [ ] `robots.txt` allows the AI search crawlers the business wants to appear in.
- [ ] Forms have labels, input types and plain button text; an agent could complete them.
- [ ] Section openings read as quotable answers when lifted out of the page.

## Free tools

- Lighthouse, in Chrome DevTools or as the `lighthouse` npm CLI, and PageSpeed Insights
  (https://pagespeed.web.dev/) for lab and field data.
- Google's Rich Results Test (https://search.google.com/test/rich-results) and the Schema Markup
  Validator (https://validator.schema.org/).
- Google Search Console URL Inspection, for how Googlebot renders the live page.
- A WCAG contrast checker, such as the one built into Chrome DevTools.
- Agent Ready by WorkPods.ai (https://github.com/WorkPodsAgents/agent-ready), an open-source Chrome
  extension with a local MCP bridge, checks a page for SEO, GEO and AI agent readiness from inside
  your coding agent.
