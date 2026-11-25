# Lean layout

A page can answer every buyer question for search engines and AI answers and still look calm to a
person. All the text stays in the HTML; only the amount shown before someone opens a fold
changes.

Live examples: [workpods.ai/geo](https://workpods.ai/geo) (a service page) and
[the agencies Agent Readiness Index](https://workpods.ai/agent-readiness-index/agencies) (a data
page with tables). Open either one on a phone, then view the source.

## Contents

- Headings and answer sentences stay fixed
- Hero
- Sections
- Lists, numbers and tables
- Boxes and borders
- FAQ
- What is safe to fold, and what is not
- Checking it in the build
- Redesigning an existing page

## Headings and answer sentences stay fixed

Headings, the one or two sentences that answer each section, and FAQ answers are written for
ranking and for being quoted. A layout change never edits them. If a design only works once a
heading or an answer sentence is reworded, change the design.

Everything else on the page can move: into a visual, into a fold, or into a caption.

## Hero

The hero shows four things:

1. The H1, at most two lines on a 390 px phone.
2. One line under it, 20 words or fewer. This is the page's first answer sentence.
3. The primary CTA.
4. Proof, only if it is real.

Leave out secondary links, small print under the button and any fold. If the page's opening answer has a
second sentence, it goes into the first section's fold.

When the next step needs an input anyway (a website, a postcode), put that box in the CTA instead
of a bare button. Carry the value to the next page in the URL so the visitor never types it twice.

## Sections

Each section shows:

1. Its heading.
2. One answer sentence. Keep it to 20 words where you can; a longer line is fine only if it is
   one sentence.
3. One visual that makes the section's point in short labels instead of full sentences.
4. A native `<details>` holding the rest: the second answer sentence, the supporting prose, the
   plain version of any list the visual drew, and the source notes.

The summary line of the fold can say "Details" or "Read more". Keep it the same across the site.

On a phone the order is heading, answer sentence, visual, fold.

## Lists, numbers and tables

- **Lists become visuals.** Three to six points become chips, rows with icons, or numbered steps
  on a line. The plain list goes into the fold, so it is still in the text.
- **Numbers become stat plates.** A big figure, a label of two to four words, and the source as a
  small caption under it. Never show a zero count as a stat.
- **Chart captions stay short and specific.** "Agencies that pass, by check" beats a sentence
  explaining the chart. Labels are at least 11 px on a phone.
- **Tables show what matters first.** Show the top rows and fold the rest into `<details>`. The
  table stays a table in the HTML.
- **Phones keep the columns.** Do not turn each row into a card with every column name repeated.
  Show short column heads once, put the row name across the full width, and set the answers side
  by side under it, with a thin line between rows. Mark cells with a symbol and a word
  ("✕ Not offered"), so the table reads without colour.

## Boxes and borders

One border level per section. A panel can hold content, but never a card inside a panel, or a
card inside a card. On a phone, prefer dividers, lines and dots to boxes; nested boxes eat the
width and make a short section look long.

Steps read well as one thin line with a dot per step and the step name and timing on one line
("Audit · 3 working days"). The step that matters most gets a filled dot, not a filled panel.

## FAQ

The FAQ starts collapsed: each question is a `<summary>`, each answer sits in its `<details>`.
The answers keep their 40 to 60 words and stay word for word identical to the `FAQPage` JSON-LD.

## What is safe to fold, and what is not

Google's mobile-first indexing guidance allows content in tabs, accordions and expandable
sections, as long as it is in the page's HTML and matches what the desktop page has. Google's
John Mueller and Gary Illyes have said such content gets full weight. A 2022 SEO test disagreed,
and Google has said it may not use folded text in search snippets. Links to each are in
[sources.md](sources.md). That is why the answer sentence
always stays visible: it is the line most likely to be quoted.

Safe:

- Native `<details>` and `<summary>`. The text is in the DOM, readable with JavaScript off.
- Tabs and accordions whose panels are all in the server-rendered HTML.
- A visual that is `aria-hidden="true"` when the same words are also in the text or the fold.

Not safe:

- Text a script fetches or injects only when someone clicks.
- `display: none` that only a script removes. A crawler that runs no JavaScript sees nothing.
- Words painted on a canvas or baked into an image, with no HTML copy.

Also keep every word in the machine-readable copies: the page's Markdown alternate, if you
publish one, and `llms-full.txt`. Those copies have no folds at all.

## Checking it in the build

People slide back into long visible text unless the build stops them. Run this check on the
prerendered HTML of every page:

1. For each section, count the visible paragraphs: text blocks that are not inside `details`,
   `figure`, `nav`, `form`, `noscript`, an element marked as a visual (for example `[data-art]`),
   or `[aria-hidden="true"]`. Fail when there is more than one.
2. Fail when a visible line is over 20 words and is more than one sentence.
3. Fail when a list (`ul`, `ol`) is shown as plain text outside a visual.
4. Fail when the hero holds more than the H1, one line, the CTA and proof.

Use one sentence splitter for both the check and the page code that picks the first sentence.
Two splitters will disagree on abbreviations ("Dr.", "vs.") and quotes, and the check will fail
pages that look right.

Exempt pages where long text is the point, such as terms and privacy, by name.

## Redesigning an existing page

Before you change anything, save the built HTML. After the change, compare:

- every heading's text, byte for byte;
- the first two sentences of every section, byte for byte;
- every FAQ question and answer.

Any difference is a failure, unless the person asked for that wording change. Then report the
visible word count before and after, for the hero and for everything above the FAQ. The visible
count should drop a lot while the word count in the HTML stays the same.
