# Finding: Content Contradictions & Service-Area Template Bugs

**Severity:** High (trust/E-E-A-T + local SEO)  
**Category:** Content / Local

## 1. Two phone numbers sitewide
| Number | Where seen |
|--------|------------|
| **858-244-2691** | Homepage CTAs, most pages, llms.txt, service-area footers |
| **619-353-5653** | `/service-areas` hub nav (jina render), some FAQ snippets in search |

NAP inconsistency hurts local pack trust and citation consistency.

## 2. Meta description template bug — wrong city
- URL: `/service-areas/san-diego-ca`
- Live meta description: *"BigBox offers portable storage and moving in **Campo, CA**…"*
- Title/H1 correctly say San Diego.

## 3. Delivery-time contradiction
| Claim | Source |
|-------|--------|
| "24–48 hours" | Carlsbad FAQ, homepage messaging |
| "book at least a week in advance" | Lincoln Acres FAQ, Palomar Mountain FAQ |

## 4. Service-model contradiction (self-load vs full-service moving)
Core FAQ: *"Big Box Storage does not actually participate in the loading process"* — self-load model.

But multiple service-area pages advertise:
- "Residential Moving — Full-service moving"
- "White-Glove Handling"
- "Packing & Unpacking Support"
- "Furniture & Appliance Delivery … set up large items"
- "Our crews are trained for terrain challenges"

Seen on: `/service-areas/lincoln-acres-ca`, `/service-areas/pala-ca`, `/service-areas/palomar-mountain-ca` (and likely more of 47 pages).

This misrepresents the offer, confuses AI/LLM extraction, and can create false-advertising risk.

## 5. Award-year math error
- News post (Nov 15 2024): "seven years in a row from **2020 to 2024**" → that's five years.
- Rates page: "7-Time Winner … **2020 to 2026**" (as of audit date, 2026 is consistent with 7 years).

## 6. Access-hours inconsistency
- Most pages / contact: access **10 AM – 4 PM**
- How-it-works step 5: "10:00 a.m. and **3:00 p.m.**"
- Questions FAQ: access 10am–4pm, 2-hour notice

## 7. Unit capacity phrasing
- llms.txt / homepage: ~**1 room**
- How-it-works FAQ: "up to **1.5 rooms**"
- Rates: sizes 40/80/120/160 sq ft all share exterior 8'×5'×7' (interior tiers differ — OK but easy to misread)

## 8. Stale NAP in search index
- Google snippet for contact historically showed ZIP **92191** vs live **92121** — recrawl/submit after fixes.

## Fix
1. Standardize on **one** phone (recommend 858-244-2691 as primary in llms.txt/structured data); update or forward 619 number; align all `tel:` links.
2. Fix san-diego-ca (and audit all 47 descriptions for wrong-city tokens).
3. Pick one delivery SLA and apply everywhere (24–48h vs 1 week — clarify standard vs rural).
4. Rewrite service-area "moving company" blocks to match actual offer (self-load + partner movers via Gorilla Movers if applicable).
5. Fix award-year sentence; unify access hours to 10–4.
