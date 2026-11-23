# Page anatomy by type

The section order and heading style for each kind of page, and why.

## Contents

- Rules for every page
- Homepage
- Service page
- Guide
- Comparison page
- Tool page
- FAQ blocks
- Bylines, dates and sources

## Rules for every page

- One H1 that carries the page's primary term.
- The first two sentences of every section answer that section without the rest of the page. AI
  answers lift short passages; a section that needs its neighbours to make sense is not quotable.
- One idea per section, about 40 to 120 words of body text. Long pages are fine; long sections
  are not.
- Headings in sentence case and written as statements or questions, never as slogans.
- A visible breadcrumb at the top of every page below the homepage.
- A clear primary action (one CTA style) near the top and again at the end.

## Homepage

Lead with positioning. A buyer arriving on the homepage wants to know what you are, who it is for
and what it gets them, in that order.

1. **Hero.** H1 = category + audience + outcome ("The family bakery that supplies Austin
   restaurants with bread baked that morning", in a fictional example). Under it, one entity
   sentence that states plainly what the business is, where it works and what it does. Then the
   primary CTA and proof that exists (customer logos, a real rating, an award with its year).
2. **Capability sections.** Each H2 is a declarative statement of a capability or differentiator
   ("Bread delivered before 7 am", not "Why choose us?"). Each section opens with two quotable
   sentences, then shows what only this business can say: its own data, its method, its people.
   Third-party statistics support the point; they are never the whole answer.
3. **How it works.** The steps in the order a customer lives them.
4. **Pricing or how to start**, if the business publishes it.
5. **Who does the work.** Named people with roles, linking to profile pages.
6. **FAQ.** 4 to 6 real buyer questions (see FAQ blocks).
7. **Closing CTA.**

Why no question H2s here: question headings dilute the entity signal (what the page is about),
slow down high-intent visitors, and compete with the guides that should own those questions.

## Service page

The same shape as the homepage, narrowed to one service.

1. H1 names the service and the outcome.
2. Entity sentence and CTA.
3. Declarative H2s: what is included, how it is delivered, what makes it different, what it
   costs or how pricing works.
4. Links to the guides that support this service, using their own terms as anchors.
5. FAQ of 4 to 6 questions, then the closing CTA.

## Guide

Guides own informational questions, so here the headings are questions.

1. H1 states the topic or the main question.
2. A short answer paragraph right under the H1: two or three sentences that a reader could stop
   after.
3. A table of contents for anything longer than a few sections.
4. H2s phrased as the questions people search, each answered in its first two sentences, then the
   detail.
5. Pull figures with their source and date, tables for anything compared on more than two
   attributes, and a list of sources at the end.
6. A byline with a named author and reviewer, the published and updated dates.
7. A link to the commercial page the guide supports.

Comfortable reading: a measure of about 60 to 80 characters per line, generous line height, and
figures that break up long text.

## Comparison page

For "X vs Y" and "best X" intents.

1. H1 is the comparison as people search it.
2. A two to three sentence verdict up front: who should pick which, and why.
3. The criteria, each as an H2 with a short answer.
4. A comparison table with the same rows for every option. Use plain words in cells, not ticks
   alone, so the table reads without colour.
5. If you are one of the options, disclose it near the top and state your method.
6. FAQ, sources, updated date.

## Tool page

For people who want to do something now (a checker, a calculator, a generator).

1. H1 says what the tool does.
2. The tool itself, or the install or launch step, above the fold.
3. What it checks or produces, as declarative H2s.
4. Privacy: what data it reads and where it goes.
5. FAQ and a link to the related service ("Want a person to check it?").

## FAQ blocks

- 4 to 6 questions on commercial pages. More becomes a guide.
- Questions as buyers type them. Take them from "People also ask", sales calls and support
  tickets, never invented to stuff keywords.
- Each answer is 40 to 60 words and its first sentence answers the question directly.
- Do not repeat a question another page owns; link to that page instead.
- Render answers in the HTML. A `<details>` element is fine because the text stays in the DOM.
- Add `FAQPage` JSON-LD only when the questions and answers in it match the visible ones
  word for word.

## Bylines, dates and sources

- Author and reviewer are real people with profile pages (`Person` with `sameAs` links to their
  public profiles). Never reassign a page's reviewer to someone who did not review it.
- Show "Published" and "Updated" dates, and put the same values in the JSON-LD.
- Every number carries its source and date, in the text or as a source line under the figure.
