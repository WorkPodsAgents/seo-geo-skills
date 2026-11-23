# Structured data (JSON-LD)

Which schema.org types to add on each page type, and the rules that keep markup honest. Google
recommends JSON-LD where the site allows it. Microsoft has said publicly (SMX Munich, March 2025)
that schema markup helps its language models understand content for Bing and Copilot.

## Contents

- Rules
- Types by page
- Examples
- What markup does not do

## Rules

1. Mark up only what the page visibly shows. Google's policy is that markup must be a true
   representation of the page and must not describe content readers cannot see.
2. `FAQPage` only beside a visible FAQ, with the same questions and answers, word for word.
3. One shared `Organization` entity (with a stable `@id`) referenced from every page, so engines
   tie all pages to one business.
4. Real people only for `author` and `reviewedBy`, each with `url` and `sameAs` links to their
   public profiles.
5. Dates in the markup match the dates on the page.
6. Validate every template (see verification.md).

## Types by page

| Page | Types |
|---|---|
| Every page | `Organization` (or a specific `LocalBusiness` subtype for a local business), `WebSite`, `WebPage` |
| Every page below home | `BreadcrumbList` |
| Homepage | `Organization` with `description`, `logo`, `sameAs`, `founder` where public; `Service` for the main offer; `FAQPage` if the FAQ is visible |
| Service page | `Service` (`serviceType`, `provider` = the Organization, `areaServed`), `FAQPage` if visible |
| Guide or article | `Article` with `headline`, `author` (Person), `datePublished`, `dateModified`, `image`; `reviewedBy` on the `WebPage` where a reviewer is shown |
| Comparison page | `Article`; `ItemList` if it ranks options |
| Tool page | `SoftwareApplication` or `WebApplication` with `applicationCategory` and `offers` |
| Team or author page | `ProfilePage` with a `Person` (`name`, `jobTitle`, `sameAs`, `worksFor`) |

Notes:

- schema.org marks the general `ProfessionalService` type as deprecated because it was confused
  with `Service`. Use `Organization`, or the most specific `LocalBusiness` subtype that fits
  (`Bakery`, `LegalService`, `AccountingService`), for the business itself.
- A local business adds `address`, `geo`, `openingHoursSpecification` and `telephone` when they
  are known, and the same values appear on the page.
- Optional properties (`logo`, `founder`, `sameAs`, ratings, awards) go in only when the facts
  exist. Omit a property rather than fill it with a placeholder.
- Since 2023 Google shows FAQ rich results only for well-known government and health sites, and it
  no longer shows HowTo rich results. Visible FAQs with matching `FAQPage` markup still help
  readers and machines read the page; just do not expect the rich result.

## Examples

Homepage of a fictional bakery (Larkspur Oven does not exist):

```html
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Bakery",
      "@id": "https://example.com/#org",
      "name": "Larkspur Oven",
      "url": "https://example.com/",
      "logo": "https://example.com/logo.png",
      "description": "Larkspur Oven is a family bakery in Austin that supplies restaurants.",
      "address": {
        "@type": "PostalAddress",
        "addressLocality": "Austin",
        "addressRegion": "TX",
        "addressCountry": "US"
      },
      "sameAs": ["https://www.instagram.com/example"]
    },
    {
      "@type": "WebSite",
      "@id": "https://example.com/#website",
      "url": "https://example.com/",
      "name": "Larkspur Oven",
      "publisher": { "@id": "https://example.com/#org" }
    },
    {
      "@type": "WebPage",
      "@id": "https://example.com/#webpage",
      "url": "https://example.com/",
      "name": "Bakery in Austin | Larkspur Oven",
      "isPartOf": { "@id": "https://example.com/#website" },
      "about": { "@id": "https://example.com/#org" },
      "dateModified": "2026-11-01"
    },
    {
      "@type": "FAQPage",
      "mainEntity": [
        {
          "@type": "Question",
          "name": "Do you deliver on Sundays?",
          "acceptedAnswer": {
            "@type": "Answer",
            "text": "The exact answer text shown on the page goes here."
          }
        }
      ]
    }
  ]
}
</script>
```

Guide with author and reviewer:

```json
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "Article",
      "headline": "How to make a sourdough starter",
      "author": {
        "@type": "Person",
        "name": "Author Name",
        "url": "https://example.com/team/author-name",
        "sameAs": ["https://www.linkedin.com/in/example"]
      },
      "datePublished": "2026-10-01",
      "dateModified": "2026-11-01",
      "image": "https://example.com/guides/sourdough-starter/cover.png",
      "publisher": { "@id": "https://example.com/#org" }
    },
    {
      "@type": "WebPage",
      "url": "https://example.com/guides/sourdough-starter",
      "reviewedBy": {
        "@type": "Person",
        "name": "Reviewer Name",
        "url": "https://example.com/team/reviewer-name"
      }
    },
    {
      "@type": "BreadcrumbList",
      "itemListElement": [
        { "@type": "ListItem", "position": 1, "name": "Home", "item": "https://example.com/" },
        { "@type": "ListItem", "position": 2, "name": "Guides", "item": "https://example.com/guides" },
        { "@type": "ListItem", "position": 3, "name": "How to make a sourdough starter" }
      ]
    }
  ]
}
```

`reviewedBy` belongs to `WebPage` in schema.org, so the reviewer goes on the page node and the
author on the `Article`.

## What markup does not do

- It does not make a weak page rank. It helps engines read what is already there.
- Google says no special markup is needed to appear in AI Overviews or AI Mode; the same SEO basics
  apply. Markup is still worth adding for clarity and for other engines.
