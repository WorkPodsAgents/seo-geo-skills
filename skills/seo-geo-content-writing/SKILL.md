---
name: seo-geo-content-writing
description: >-
  Write and edit web page copy that ranks in search and gets quoted in AI answers (SEO and GEO),
  then run a humanizer pass so it reads like a person wrote it, with no AI slop. Covers the page
  brief (intent, keywords, buyer questions, term ownership), answer-first sections, FAQ answers,
  quotable fact sentences with sources, bylines, internal link anchors, banned filler words, a
  humanizer checklist of AI writing tells, and illustration microcopy. Use for SEO content
  writing, SEO copywriting, landing page and service page copy, guides, FAQs, meta titles and
  descriptions, or when asked to humanize or de-slop text.
license: MIT
metadata:
  author: WorkPods.ai
  homepage: https://workpods.ai
  version: "1.1.0"
---

# SEO and GEO content writing

By WorkPods.ai. This skill is how we write pages that search engines rank and AI answers quote,
then edit them until they read like a person wrote them. It works for any business.

Google judges content by its quality, not by whether AI helped write it, but pages produced in bulk
mainly to rank break its scaled content abuse policy. Write fewer pages, each with facts only this
business can state.

The work has four steps: brief, draft, humanize, check. Do them in order. Skipping the brief is the
most common reason a page ranks for nothing.

The humanizer pass is adapted from [blader/humanizer](https://github.com/blader/humanizer) by Siqi
Chen (MIT licence). See the NOTICE file in this repository.

## Step 1: write the page brief

Before writing a word of copy, fill in this brief. Template and guidance:
[references/page-brief.md](references/page-brief.md).

```text
Page:            URL and page type (homepage, service, guide, comparison, tool)
Intent:          what the searcher wants to do or know, in one sentence
Primary term:    the one search term this page owns
Secondary terms: close variants this page also carries
Not this page:   terms other pages own, and which page owns each
Buyer questions: 4 to 6 real questions (People also ask, sales calls, support)
Facts available: each fact with its source and date
Author/reviewer: real names: as on the current page, or ask who for a new page
Supports:        the commercial page this guide links to (guides only)
```

If a fact, number or name you need is not in the brief's sources, leave it out or ask for it.
Never fill the gap with something plausible.

Without keyword or question data, ask for it. If you must proceed, pick the most likely term and
questions yourself, mark them "unverified" in the brief, and say so in your report so a person
can check them before the page ships.

Output Markdown with the title and description in front matter, unless the person's site uses
another format.

## Step 2: draft answer-first

### Openings

The first two sentences of the page and of every section answer the question that
section exists for, so they make sense if an AI answer quotes them alone. Put the primary term in
the H1, the first sentence and the title, written naturally.

Write the first sentence so it can be the only line a person sees. A lean layout shows each
section's heading, its first sentence and a visual, and folds the rest away (see the design
skill's lean-layout reference). So the first sentence answers the question on its own, in one
sentence, ideally 20 words or fewer. The second sentence sits in the fold and must still read
well straight after the first.

### Section size

About 40 to 120 words of body per section, one idea each. Most of it will sit in a fold, so
write it as the detail behind the answer, not a second introduction. Split a section that makes two points.
If the facts for a section run out before 40 words, leave it short or merge it into a neighbour,
and list the missing facts in your report. Never pad a section to reach a count.

### Headings

Commercial pages (homepage, services) use declarative H2s that state a capability.
Guides use the questions people search as H2s. Headings use sentence case.

### FAQ answers

4 to 6 questions on commercial pages. Each answer is 40 to 60 words and its first sentence
answers the question. Count the words. When the facts cannot fill 40 words without repeating
another answer, use fewer questions rather than padding; four good answers beat six thin ones.

### Quotable facts

State the business's own facts (hours, prices, dates, method) plainly; their source is the
business, recorded in the brief. Write third-party figures as plain sentences with a subject, a
number and a source, following the pattern "[Source] found in [month year] that [number] of
[group] [did what]." Prefer your own data and method; third-party figures support a point, they are
rarely the point.

### Never invent

Never invent facts, clients, logos, quotes, testimonials, prices, results, timelines, awards
or authors. If the page needs proof you do not have, say what is missing.

### Bylines

Keep the author and reviewer exactly as given or as on the current page. For a new page, ask who
wrote and who reviewed it. Never reassign who reviewed a page.

### Internal links

Link to the page that owns a related term, using that page's own term as the anchor text, inside
a sentence. You may change word order, capitals or plurals so it reads naturally ("preorder from
our Portland bakery" for the term "bakery preorder portland"), but keep its words. Never target
another page's term on this page; a short answer that links to the owner page is fine.

### Titles and descriptions

Title about 30 to 60 characters with the primary term near the start
and the brand at the end. Meta description about 70 to 160 characters that answers the intent.

### Banned words and phrases

Do not use: unlock, elevate, seamless, game-changer, revolutionize,
harness the power, delve, cutting-edge, best-in-class, world-class, leverage (as a verb),
synergy, empower, in today's fast-paced world, look no further. The humanizer reference lists the
wider set of AI tells.

### Illustration microcopy

When a section has an illustration, its text is a few labels, not
sentences: "Order placed 9:04 pm", "Out for delivery", "Delivered 6:42 am". A list in the copy
often becomes the visual, so keep each point short enough to work as a label. A stat plate
needs a figure, a label of two to four words and a source line. Mark invented sample
data "Example". Describe each visual for the designer in a short comment under the section, 25
words or fewer.

## Step 3: humanizer pass

Run the full pass in [references/humanizer.md](references/humanizer.md) over the whole draft:

1. Read it once and mark every AI tell, strongest first (contrasts like "not X but Y", one-line
   closers, staged openers, forced triads, dashes, inflated significance, stock AI words, bold
   labels, chatbot leftovers).
2. Rewrite each marked passage by stating the point plainly.
3. Re-check what humanizing breaks most often: facts, numbers, sources, keywords, heading intent,
   FAQ word counts and link anchors must all survive unchanged.
4. Search again for the tells that survive a first rewrite: contrasts, closers, triads, dashes and
   bold labels.

The final copy has no em dashes or en dashes.

## Step 4: check before handing over

- [ ] The primary term is in the title, H1 and first sentence; no other page's term is targeted.
- [ ] Every section's first two sentences answer it on their own.
- [ ] Sections are about 40 to 120 words; FAQ answers are 40 to 60 words (counted).
- [ ] Every number has a source and date; nothing is invented.
- [ ] Author and reviewer unchanged.
- [ ] Internal link anchors are the target pages' own terms.
- [ ] Title and description lengths are in range.
- [ ] No banned words, no em or en dashes, humanizer checklist passed.
- [ ] Illustration text is labels only, and sample data is marked "Example".

Report what you wrote, the word counts, any fact you left out for lack of a source, and the kinds
of AI tells the humanizer pass removed.

For page structure, schema and technical checks, use the companion skill
`seo-geo-website-design`. Sources: [references/sources.md](references/sources.md).
