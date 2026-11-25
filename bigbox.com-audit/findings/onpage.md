# Finding: On-Page Elements (Titles, Descriptions, H1s, OG)

**Severity:** Medium  
**Category:** On-Page SEO

## What works
| Element | Status |
|---------|--------|
| `<title>` | Unique on all sampled pages; length OK |
| Meta description | Present and unique on sampled pages |
| H1 | One per page; topic-matched (microlink `h1` selector) |
| `lang` | `en` |
| Internal nav | Clear IA: Home / Portable Storage / Service Areas / Rates / How It Works / Company |

## Sampled titles
- `/` → Big Box Storage - Affordable Portable Storage Delivered to You
- `/how-portable-storage-works` → How Portable Storage Works - Big Box Storage San Diego
- `/portable-storage` → Portable Storage Units in San Diego - Big Box Storage
- `/questions` → Frequently Asked Questions - Big Box Storage
- `/service-areas` → Big Box Storage - Service Areas | Storage Pods in San Diego
- `/blog/what-is-a-portable-storage-unit…` → What Is a Portable Storage Unit? How It Works by Big Box Storage

## Issues

### 1. Fit-text H1 extraction risk (Framer)
Markdown/jina extracts show either run-together (`HowPortableStorageWorks`) or letter-spaced (`H o w P o r t a b l e…`) text. html2txt and microlink `h1` type=text return proper words — so **rendered text is likely fine for Googlebot**, but:
- Confirm in DevTools that `h1.textContent` has normal spaces.
- If spans lack whitespace, fix (Framer fit-text) — extractors and some AI crawlers may misread.

### 2. Keyword-stuffed H1 on rates
- `/rates-promos` extract: `GettheBest PortableStorageUnitsCostinSanDiego`
- Prefer natural: "Portable Storage Rates & Promotions in San Diego"

### 3. Canonical / viewport / robots meta
- microlink attr selectors returned **null** for `link[rel=canonical]`, `meta[name=viewport]`, `meta[name=robots]` on every page tested.
- Could be selector/attr extraction limits — **verify in raw View-Source**. If truly missing: add canonical (self), confirm viewport (mobile), add `max-image-preview:large` robots meta sitewide.

### 4. Sitewide og:image
- Same `framerusercontent…9ljoHKFmXu14xSTcXqPBpwyRCc.png` (1200×630, 209KB) on every URL.
- Not duplicate-content fatal, but weak for social CTR; generate per-template OG images (hero + city for service areas).

### 5. Blog authorship
- `author: null` on sampled post; `<time>` present (Jul 29, 2026) — good date signal, missing E-E-A-T author.

### 6. Internal links into redirects
- See redirects finding — fix hrefs to final destinations.

### 7. H1 on service-area hub
- Long keyword-ish H1 via jina: "Affordable Storage Pods in San Diego for Easy Portable Storage" — acceptable but could be tightened.

## Fix priority
1. Verify canonical+viewport in raw HTML; fix if absent.
2. Confirm fit-text H1 textContent spacing.
3. Rewrite rates H1.
4. Add author bylines + `BlogPosting` to posts.
5. Per-page OG images for key templates.
