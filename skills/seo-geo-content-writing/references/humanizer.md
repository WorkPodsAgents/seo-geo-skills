# Humanizer pass

Adapted from [blader/humanizer](https://github.com/blader/humanizer) by Siqi Chen, version 3.1.0,
MIT licence (notice at the end of this file). The original patterns come from Wikipedia's
["Signs of AI writing"](https://en.wikipedia.org/wiki/Wikipedia:Signs_of_AI_writing), maintained
by WikiProject AI Cleanup. WorkPods.ai shortened the examples and added the rules for web copy:
what the pass must never change on an SEO page.

## Contents

- Why AI text sounds the way it does
- What the pass must never change
- How to run the pass
- A. Staging instead of stating (act on one sighting)
- B. Rhythm by rule
- C. Inflation and borrowed authority
- D. Formatting by rule
- E. Leftovers from the chat and the draft
- When not to act
- Review checklist
- Licence

## Why AI text sounds the way it does

A language model picks the most likely next word, so by default it makes the choice that suits the
widest range of readers. A person writes for one reader and one subject, so their choices are
uneven and specific. Every tell below is a default choice: staging (signalling importance instead
of adding a fact), rhythm by rule (triads and dashes everywhere), inflation, formatting by rule,
and leftovers from a chat.

Every sentence you keep must add something the reader did not already have. A tell counts in
proportion to how rarely a careful writer would make it on purpose. Patterns 1 to 5 justify an
edit on one sighting; a pattern marked *weak alone* needs other tells nearby.

## What the pass must never change

On a web page the humanizer edits style, never substance. Keep exactly:

- every fact, number, date, source line, name and quote;
- the primary and secondary terms where they appear in the title, H1, first sentence and headings;
- each heading's intent (a question H2 stays a question; a declarative H2 stays declarative);
- FAQ answer lengths of 40 to 60 words (recount after editing);
- internal link targets and their anchor text;
- author and reviewer names;
- code, commands, URLs, front matter and structured data.

Do not add a fact, name, number or citation that is not in the brief.

## How to run the pass

1. **Mark.** Read the whole text once and mark every tell, strongest first. Look at paragraph shape
   as well as sentences: a contrast split over two sentences, or the same closer after every
   section, is the same tell at a larger scale.
2. **Rewrite.** State each point directly. You may shorten, merge, split and restructure, but keep
   every supported claim.
3. **Check.** Read it aloud. Compare against the "never change" list. Search again for the tells
   that survive a first rewrite: contrasts (1), closers (2), triads (6), dashes (8) and bold labels
   (19).
4. **Finish.** If a sentence stays awkward, rewrite the paragraph around its main point. Vary
   sentence length.

Voice: marketing and reference copy stays plain and specific. If the person gives a writing sample,
match its sentence length, word choice and punctuation; the sample overrides these rules.

## A. Staging instead of stating (act on one sighting)

**1. Not X but Y.** "Not just X, but Y", "it's not X, it's Y", "X rather than Y", the same contrast
split over two sentences, or a clipped tail ("..., no guesswork"). The negative half names
something nobody claimed so the positive half sounds bigger. State the point. Keep a contrast only
when the negative half corrects a belief the reader really holds.
> Before: It's not just a bakery, it's a neighbourhood ritual.
> After: Most of our customers come in at least twice a week.

**2. One-line closers and dramatic fragments.** A one-sentence paragraph that restates the one
before ("That's the difference."), a line naming what an example showed, a row of fragments ("No
shortcuts. No compromises."), a word in capitals. Cut the closer, or replace it with a new fact.

**3. Sayings that sound deep.** "At its core", "the real question is", "X is the language of Y".
Replace with the specific claim.

**4. Staged run-up.** "Let's dive in", "Here's the thing", "Here's what you need to know", a
standalone "Honestly?". Delete the run-up and start with the point.

**5. Arguing with no one.** "To be clear", "This isn't about", "You might think... but", "A
tempting approach would be". Remove the defence; state any real claim it holds.

## B. Rhythm by rule

**6. Forced triads.** Three items, three examples or three short sentences because three sounds
complete. Keep three only when there are three real things.
> Before: Fresh, local and handcrafted bread for every occasion.
> After: Bread baked overnight from Texas-milled flour.

**7. Repeated sentence openings.** Several sentences in a row starting with the same subject.
Merge or vary them.

**8. Dashes as the universal connector.** No em dashes (—) or en dashes (–) in the final copy,
including spaced hyphens or `--` used as dashes. Use a period, comma, colon or parentheses, or
rewrite. Leave hyphens in compound words, code and URLs alone.

**9. Stacked qualifiers.** "Could potentially", "may arguably", "in some cases it might". Keep one
qualifier where the source supports doubt. *Weak alone.*

**10. Hyphenated pairs after the noun.** "The process is well-documented" becomes "the process is
well documented". Keep the hyphen before a noun. *Weak alone.*

**11. Passive voice and missing subjects.** "No setup needed." Say who does what. *Weak alone.*

## C. Inflation and borrowed authority

**12. Overused AI words.** actually, additionally, align with, bolstered, crucial, deep dive, delve,
enduring, enhance, garner, highlight (verb), interplay, intricate, key (adjective), landscape
(abstract), meticulous, pivotal, quietly, robust (figurative), showcase, tapestry, testament,
underscore (verb), valuable, vibrant. In web copy add: unlock, elevate, seamless, game-changer,
revolutionize, harness the power, cutting-edge, best-in-class, world-class, empower, leverage (verb).

**13. Inflated significance.** "Marks a pivotal moment", "plays a key role", "setting the stage
for", "the future looks bright". Keep the fact, drop the significance, end on the last concrete
fact.

**14. Vague connection.** "Associated with", "linked to", "tied to". Name the relationship, or keep
the vague wording if the source does not say.

**15. Shallow -ing riders.** "..., ensuring quality", "..., reflecting our commitment to", "...,
fostering community". Cut the rider unless the source supports it.

**16. Sales language.** nestled, in the heart of, rich (figurative), renowned, breathtaking,
stunning, must-visit, diverse array, commitment to. State what the thing is.
> Before: Nestled in the heart of Austin, our renowned bakery offers a stunning array of breads.
> After: The bakery is on East 6th Street in Austin and bakes 14 kinds of bread daily.
> (The address and the count must come from the brief.)

**17. Borrowed authority.** "Experts agree", "industry reports show", a list of outlets. Name the
real source and what it said, or cut the claim.

**18. Avoiding is, are and has.** "Serves as", "stands as", "boasts", "features", "offers". Use
is, are and has.

## D. Formatting by rule

**19. Bold as decoration.** Bold on every item, lists where each line starts with a bold label and
a colon. Remove the bold; turn label lists into prose when the labels add nothing.

**20. Decorative headings.** Title Case Headings, emojis or arrows in headings, a rule between
every section, headings written for effect. Use sentence case and name what the section holds.

**21. Curly quotes** where the format uses straight quotes. *Weak alone.*

## E. Leftovers from the chat and the draft

**22. Chatbot residue.** "Great question!", "I hope this helps", "Let me know if", "Here is a".
Remove the wrapper, keep the content.

**23. Knowledge-limit disclaimers.** "As of my last update", "based on available information",
"while details are limited", followed by a guess. State what the source does not show, or cut.

**24. Heading repeated in the first sentence.** "## Delivery / Delivery matters." Cut the repeat.
On an SEO page the first sentence must answer the heading, not echo it.

**25. Writing about the document.** "This page covers", "the table below compares", "we compiled".
Write about the subject.

**26. Re-explaining what the reader knows.** In replies and follow-up copy, lead with the decision.

## When not to act

Leave a watched phrase alone inside a quotation, a product or proper name, or a passage that
discusses the phrase. One tell alone is weak evidence; several together are the signal. Keep
details that carry the writer's voice: a specific address, an unusual fact, a real aside.

## Review checklist

Run this after the rewrite and before handing over.

- [ ] No "not X but Y" contrasts, split or clipped.
- [ ] No one-line closers, fragment rows or staged openers.
- [ ] No forced triads; every list of three has three real items.
- [ ] No em dashes or en dashes.
- [ ] No words from the overused and banned lists.
- [ ] No inflated significance, -ing riders, sales language or unnamed authorities.
- [ ] No bold labels, Title Case headings, emojis or chatbot leftovers.
- [ ] Every fact, number, source, name and quote is still there and unchanged.
- [ ] Primary term still in title, H1 and first sentence; heading intents unchanged.
- [ ] FAQ answers recounted: 40 to 60 words each.
- [ ] Link targets and anchors unchanged; author and reviewer unchanged.
- [ ] Read aloud once more: does any sentence still sound generated? Rewrite it.

## Licence

The humanizer patterns in this file are adapted from blader/humanizer
(https://github.com/blader/humanizer), distributed under this licence:

```text
MIT License

Copyright (c) 2025 Siqi Chen

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.
```
