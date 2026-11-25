# Finding: Structured Data (Schema) Sparse and Inconsistent

**Severity:** High  
**Category:** Schema / AI Search  
**Weight impact:** Schema 10% category scored **35/100**

## Confirmed live JSON-LD
| Page | Type | Notes |
|------|------|-------|
| `/residential-solutions` | `Service` | serviceType Residential Portable Storage; provider LocalBusiness `@id` → homepage; areaServed San Diego; OfferCatalog (6 use-cases) |

## Confirmed **null** via `script[type="application/ld+json"]` selector (microlink)
- `/` (homepage)
- `/questions`
- `/service-areas` (and `/service-areas/`)
- `/service-areas/la-jolla-ca`
- `/service-areas/san-diego-ca`
- `/portable-storage`
- `/blog/what-is-a-portable-storage-unit-and-how-does-it-work`

## Index-snippet only (not confirmed in live HTML)
- Google `site:bigbox.com` snippet for `/service-areas` contains LocalBusiness JSON-LD text (address, phone, geo, openingHours). Live probe still returned `ld: null` — may be stale index or JS-injected schema not visible to the selector. **Re-verify in production HTML.**

## Missing recommended types
| Type | Where needed |
|------|----------------|
| `Organization` / `LocalBusiness` | Homepage (NAP, geo, sameAs, aggregateRating) |
| `WebSite` + `SearchAction` | Homepage |
| `FAQPage` | `/questions`, FAQ blocks on how-it-works, service-areas |
| `Article` / `BlogPosting` | 152 blog + 25 news posts (have `<time>` but no author, no JSON-LD) |
| `BreadcrumbList` | All interior pages |
| `AggregateRating` / `Review` | Homepage + service pages (SoTellUs 4.9/1496, Google 684 reviews available) |
| `Product`/`Offer` (optional) | Rates page pricing tiers |

## Related gaps
- Blog posts: `author: null` in meta; no byline markup found.
- Canonical: `link[rel=canonical]` → **null** on all pages probed (homepage, how-it-works, blog, service-areas). Viewport & robots meta also null via attr selectors — may be extraction limitation, but **must confirm in raw HTML**; Framer usually emits canonical automatically.
- `llms.txt` present and rich; `llms-full.txt` → **404**.

## Fix (priority order)
1. Add sitewide `LocalBusiness` (or `Organization` + `LocalBusiness`) with verified NAP, geo, openingHours, priceRange, sameAs (Google profile cid=7027956076036550772), and `@id` matching residential-solutions provider reference.
2. Add `FAQPage` to `/questions` and key FAQ sections.
3. Add `BlogPosting` (headline, datePublished, dateModified, author, image, publisher) to all posts.
4. Add `BreadcrumbList`.
5. Wire `AggregateRating` from SoTellUs/Google counts (only if policy-compliant with Google guidelines — self-serving reviews on own site must follow restrictions).
6. Fix `llms-full.txt` (404) or remove references if any.
7. Verify canonical + viewport in View-Source on homepage; if truly absent, add via Framer SEO settings.
