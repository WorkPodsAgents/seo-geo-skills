# Technical SEO and GEO

What every public page needs so search engines index it, AI answers can quote it and AI agents can
use it. Checked against search engine documentation in November 2026; see sources.md.

## Contents

- Server HTML first
- Headings, title and description
- Canonical, indexing and the sitemap
- Breadcrumbs
- Bylines and dates
- Images
- Retiring and moving URLs
- Search Console and Bing Webmaster Tools
- robots.txt and AI crawlers
- llms.txt
- Forms people and agents can use

## Server HTML first

- Every word a person can read is in the HTML the server sends. Prerender or server-render
  marketing pages; do not build them only in the browser.
- Google renders JavaScript in a later step that can take longer than the first crawl. Most AI
  crawlers do not run JavaScript at all (Vercel's 2024 study found none of the major ones did,
  apart from Gemini via Googlebot and Applebot). Content that needs a script may be invisible to
  them.
- No stylesheet hides content (`opacity: 0`, `visibility: hidden`, `display: none` on body copy)
  unless the rule only applies once a script has added a class. Tabs, accordions and `<details>`
  are fine when the text stays in the DOM.
- Test by loading the page with JavaScript disabled, or by fetching it with `curl`, and reading it.

## Headings, title and description

- One H1 per page, with the primary term. Headings go in order (H2 under H1, H3 under H2) without
  skipping a level.
- Title: unique, about 30 to 60 characters, primary term near the start, brand at the end. Google
  sets no length limit but cuts long titles to fit the screen and may rewrite titles that do not
  match the page.
- Meta description: unique, about 70 to 160 characters, answering the intent. Google may show
  other text from the page instead.
- No two pages share a title, H1 or primary term.

## Canonical, indexing and the sitemap

- Each indexable page has one absolute, self-referencing canonical:
  `<link rel="canonical" href="https://example.com/page">`.
- Pages that should not rank (thank-you pages, drafts, internal search) carry
  `<meta name="robots" content="noindex">` and stay out of the sitemap.
- The XML sitemap lists every indexable page and nothing else. Update it in the same release as
  any page change.
- Give every page an `og:title`, `og:description` and a 1200 x 630 `og:image` so shares and chat
  previews look right.

## Breadcrumbs

Show a visible breadcrumb (Home > Section > Page) on every page below the homepage and mark it up
with `BreadcrumbList`. Google shows breadcrumbs in desktop results only since January 2025, but the
trail still helps people, crawlers and the page's internal linking.

## Bylines and dates

- Guides and articles show a named author and, where there is one, a named reviewer. Both link to
  profile pages that say who they are, with links to their public profiles.
- Show the published and updated dates and use the same values in the JSON-LD.
- Google strongly encourages accurate authorship information such as bylines. Never invent an
  author or credit a reviewer who did not review the page.

## Images

- Every `<img>` has `alt` text that describes it (empty `alt=""` for purely decorative images).
- Every image has `width` and `height` attributes, or a CSS `aspect-ratio`, so the browser reserves
  its space and layout does not shift.
- Serve modern formats (AVIF or WebP) at the displayed size, lazy-load images below the fold, and
  never lazy-load the hero image.

## Retiring and moving URLs

| Situation | Response |
|---|---|
| A page moved or has a clear successor | 301 (or 308) to the successor, kept for at least a year |
| A page is gone for good with no successor | 410 Gone (404 also works) |
| A temporary move | 302 or 307 |

- Google treats 301 as a strong signal and says permanent redirects do not lose PageRank. It
  treats all 4xx responses (except 429) the same way, so 410 and 404 both remove a page; 410 states
  the intent plainly to every crawler and tool.
- Never redirect a retired page to the homepage just to keep its links. An unrelated target is
  treated much like a 404 and confuses visitors.
- Put the whole redirect map in one place (server config or CDN), in place before any page moves.
- In the same release: update internal links to point at the final URL (no internal link should
  hit a redirect), canonicals, the sitemap and `llms.txt`, so crawlers never see two versions.

## Search Console and Bing Webmaster Tools

When retiring or moving URLs:

1. Export the indexed and "not found" pages from Google Search Console and Bing Webmaster Tools,
   and merge them with the sitemap and the list of old URLs.
2. Classify each URL as keep (200, in the sitemap), 301 or 410.
3. Ship the redirect map.
4. Resubmit the sitemap in both tools and request indexing for the most important changed pages.
5. Use Google's Removals tool only for something urgent; it hides a URL for about six months and
   does not remove it permanently. Redirects and 410s do the permanent work. Bing has its own
   Content Removal tool.
6. Ping IndexNow so Bing and other participating engines (Yandex, Seznam, Naver, Yep) pick up
   changes quickly. Google does not use IndexNow.
7. Check both tools weekly for new errors until the changes settle.

## robots.txt and AI crawlers

Decide per crawler whether you want to appear in AI search, in AI training data, or neither, and
say so in `robots.txt`. Current tokens from each vendor's documentation:

| Vendor | Search and answers | Training | User-triggered fetches |
|---|---|---|---|
| Google | Googlebot (also AI Overviews and AI Mode) | Google-Extended (Gemini apps and training; not Search) | |
| OpenAI | OAI-SearchBot | GPTBot | ChatGPT-User |
| Anthropic | Claude-SearchBot | ClaudeBot | Claude-User |
| Perplexity | PerplexityBot | | Perplexity-User |
| Apple | Applebot | Applebot-Extended (opt-out token only) | |
| Common Crawl | | CCBot | |
| Microsoft | Bingbot (Bing and Copilot answers use the Bing index) | | |

Notes:

- Blocking Googlebot removes you from Google Search and its AI features alike. Google-Extended does
  not affect Search.
- User-triggered fetchers may not follow `robots.txt`, because a person asked for the page.
- A business that wants to be cited in AI answers should allow the search crawlers above.
- Cloudflare's Content Signals Policy adds a line that states how content may be used after it is
  crawled, for example `Content-Signal: search=yes, ai-input=yes, ai-train=no`. It expresses a
  preference; it does not enforce anything.

Example (allow everything, point to the sitemap):

```text
User-agent: *
Allow: /

Sitemap: https://example.com/sitemap.xml
```

## llms.txt

`llms.txt` is a proposal (llmstxt.org, September 2024) for a Markdown file at the site root that
lists the site's key pages for language models. It is not a standard, and Google says you do not
need special AI text files to appear in its AI features. It is cheap to publish and some agents and
tools read it, so a short, accurate one does no harm: the one-line description of the business,
then links to the main pages with a sentence each. Keep it in sync with the sitemap.

## Forms people and agents can use

AI agents in browsers fill in forms the way people using assistive technology do: they read the
labels. So:

- Every input has a visible `<label for>`, a correct `type` (`email`, `url`, `tel`) and an
  `autocomplete` value where one applies.
- Buttons are `<button>` elements with text that says what happens ("Request a quote").
- Errors are text next to the field, not colour alone.
- Do not hide the form behind a script-only widget or a CAPTCHA on first view.
- WebMCP is a draft from the W3C Web Machine Learning Community Group that lets a page declare
  tools for browser agents. Chrome documents declarative form attributes (`toolname`,
  `tooldescription`, and `toolparamdescription` on fields) and an imperative
  `document.modelContext.registerTool()`. It is experimental, so check its current status before
  relying on it. Agents without WebMCP still depend on the labels.

```html
<form action="/quote" method="post"
      toolname="request_quote"
      tooldescription="Request a wholesale bread quote for a restaurant">
  <label for="email">Work email</label>
  <input id="email" name="email" type="email" autocomplete="email" required
         toolparamdescription="Email address to send the quote to">
  <label for="covers">Covers per day</label>
  <input id="covers" name="covers" type="number" min="1"
         toolparamdescription="Average number of diners served per day">
  <button type="submit">Request a quote</button>
</form>
```
