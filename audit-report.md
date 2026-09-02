Complete Conversion Funnel & CTA Architecture Audit
Subject: B2B UX design agency site, 377 pages (Framer) Crawl date: 16 August 2026 Method: Full sitemap crawl (377 URLs, all fetched and parsed) + rendered-DOM verification in Chrome on 12 template types + live click-testing of every primary CTA.

Revision note (v1.1). Two changes from the first issue of this document: (a) All client-identifying names and the domain have been replaced with placeholders. (b) Four factual corrections, from a follow-up pass that measured every CTA's rendered position in Chrome and click-tested each one. The first issue described the pricing page as lacking per-tier CTAs; it has three, and they are broken. The same pass found dead CTAs on the industry template, the resources page and blog posts that the static crawl could not detect. Corrected sections: 2.2 Pricing · 2.2 Resources · Funnel 18 · Phase 4 (F18) · Phase 5 (pricing, industry, resources rows) · Phase 6 quick win #4 · Phase 7 pricing branch.
EXECUTIVE SUMMARY
Metric
Result
Pages crawled
377 (100% HTTP 200, zero redirects on sitemap URLs)
Distinct page templates
23
CTAs / clickable elements mapped
24,538 unique (page × text × destination)
Conversion endpoints on the entire site
3 — /contact (form), cal.com/[handle]/30min, cal.com/[handle]/quick-chat + mailto/tel
Broken internal links (404)
14
Orphan pages (zero internal inbound links)
45
Portfolio-filter pages returning zero projects
13
Pages where the persistent "Book a call" button does nothing
~147 (every non-blog template)
Other dead CTA types confirmed by click test
5 — pricing tiers ×4, industry consultation, 7 resource magnets, blog lead-magnet, local-LP service cards

The single biggest finding: the site's most persistent CTA — the yellow "Book a call" pill fixed to the bottom-right of every page — has no href and no click handler on the Homepage, Service pages, Industry pages, Case studies, About, Pricing and Local landing pages. It is only wired up on blog posts. Clicking it produces no navigation, no scroll, no modal. Verified by live click on Homepage (×2), a Service page and a Case study. This is the highest-intent CTA on the site and it is dead on the highest-intent pages.

PHASE 1 — SITE CRAWL AND PAGE INVENTORY
1.1 Inventory summary by page type
Full row-level inventory is in the attached page-inventory.csv (377 rows). Summary:
#
URL pattern
Page Type
Page Purpose
Crawl Depth
Count
1
/
Homepage
Brand entry, service overview, route to contact/work
0
1
2
/contact
Contact (conversion)
Brief form + cal.com booking — the only true conversion page
1
1
3
/pricing
Pricing
Qualify budget, present engagement models
1
1
4
/our-story
About
Trust and credibility
1
1
5
/services
Service hub
Route to 7 service pages
1
1
6
/services/{7 pages}
Service page
Sell a specific capability
1
7
7
/industry
Industry hub
Route to 6 industry pages
1
1
8
/industry/{6 pages}
Industry page
Sell vertical expertise
1–2
6
9
/projects
Case study hub
Filterable portfolio proof
1
1
10
/projects/{13 pages}
Case study
Deep client proof
1–2
13
11
/blog
Blog hub
SEO content index
1
1
12
/blog/{230 posts}
Blog post
Organic acquisition
1–2
230
13
/resources
Resources hub
Lead magnets (Notion / Google Sheets)
1
1
14
/author + /author/{7}
Author pages
E-E-A-T bio + post list
ORPHAN / 2–3
8
15
/web-design/{40 cities}
Local landing (web design)
Local SEO capture
3
40
16
/ui-ux-design/{39 cities}
Local landing (UI/UX)
Local SEO capture
ORPHAN
39
17
/web-design, /saas, /e-commerce, /finance, /ed-tech, /branding, /development, /insurtech, /artificial-intelligence, /market-place, /mobile-app-design, /business-consulting, /ux-design, /ai-design, /brand-design, /saas-design, /health-care, /hr-tech, /web-3
Vertical / portfolio-filter landing
Portfolio category filter — 0 conversion CTAs on all of them
2–3 / ORPHAN
19
18
/thankyou
Thank you
Post-submit confirmation
3
1
19
/terms-of-use, /privacy-policy, /referral-policy
Legal
Compliance
1
3
20
/support
Portfolio filter shell
Mislabelled — renders an empty Projects filter, no support content
3
1
21
/tools-resources
Portfolio filter shell
Intended tools page — renders an empty project filter, orphaned
ORPHAN
1

1.2 Crawl integrity flags
No 404s or redirects among the 377 sitemap URLs. All problems are in internal links pointing off-sitemap:
14 broken internal links (hard 404)
Broken destination
Linked from
Notes
/projects/:EvxErjRB0
5 blog posts (design-system-specialist, interactive-website-examples, principle-of-design-balance, split-complementary-color-scheme, +1)
Unrendered Framer CMS template variable — a raw :slug placeholder shipped to production
/author/:MmG2T32Ts
blog/ai-ux-vs-traditional-ux-what-actually-works-for-saas-products
Same class of bug
/blog/ai-ux-design-tools
blog/ai-prototyping-tools


/blog/ai-UX-design-mistakes
blog/ai-prototyping-tools
Casing error; correct slug is lowercase
/blog/ux-agency-vs-inhouse-designer
blog/interaction-designer
Correct slug is ux-agency-vs-in-house-designer
/blog/ai-product-design-agency-us
blog/ai-design-agency-vs-traditional-agency
Correct slug is best-ai-product-design-agencies-us
/blog/what-is-heuristic-evaluation
blog/what-is-design-thinking
Correct slug is heuristic-evaluation
/blog/saas-metrics
blog/vertical-saas


/blog/interactive-websites
blog/how-to-promote-your-website
Correct slug is interactive-website-examples
/blog/how-to-choose-the-right-web-design-agency
blog/best-design-subscription-agency
Truncated slug
/blog/what-p
blog/what-is-a-ux-design-brief
Truncated URL — link text bled into href
/blog/design-systems-for-s
blog/what-is-a-ux-design-brief
Truncated URL
/blog/...-foundershow
blog/how-to-do-a-ux-audit-steps-and-tools-to-use
Trailing text concatenated into slug
/blog/...-guidewhat, /blog/...-retentionhow
blog/user-journey-vs-user-flow
Same concatenation bug (2 links)

11 protocol-downgrade internal links (unnecessary redirect hop)
blog/company-rebranding (8 links), blog/ux-design-agency-seattle (2), blog/best-enterprise-ux-design-agencies, blog/heuristic-evaluation, blog/design-strategy all link to http://example-agency.com/... instead of https://example-agency.com/.... Each costs a 301 hop.
1 soft redirect
blog/best-fintech-ux-design-agencies → /blog/how-to-design-ai-dashboards → redirects to /blog/ai-dashboard-design.
4 pages linking to /contact with a stale GA _gl tracking string
blog/best-ux-design-tools, blog/homepage-design-principles, blog/how-to-create-a-product-roadmap, blog/what-is-responsive-website-design — a hard-coded cross-domain linker param from June 2025. Works, but pollutes analytics.
13 portfolio-filter pages that return zero projects
/ux-design, /ai-design, /saas-design, /brand-design, /tools-resources, /finance, /health-care, /hr-tech, /market-place, /web-3, /branding, /development, /support. Each renders exactly 477 words — header + footer + an empty project grid — with no unique content and no conversion CTA. A visitor arriving from search sees a category filter with nothing in it and a dead "Book a call" pill. (A further 8 filter pages are thin: /e-commerce 555 words, /insurtech 561, /business-consulting 564, /ed-tech 771, /mobile-app-design 915, /artificial-intelligence 1,044, /saas 1,359, /web-design 1,383 — all with 0 conversion CTAs.)
Crawl note: an initial concurrent pass returned truncated HTML for 13 URLs; all were re-fetched individually and confirmed to serve full content. The figures above are from the verified re-fetch.
45 orphan pages (no internal inbound link anywhere on the site)
All 39 /ui-ux-design/{city} pages, /author, /ai-design, /brand-design, /saas-design, /tools-resources, /ux-design. The 40 /web-design/{city} pages are linked (depth 3); the 39 /ui-ux-design/{city} twins are not linked from anywhere.

PHASE 2 — CTA AND CLICKABLE ELEMENT MAP
Full row-level map: cta-map.csv, 24,538 rows with columns Page URL | Page Type | CTA Text | CTA Type | Position | Destination URL | Destination Type | Journey Stage | Scope.
Because this is a Framer site, CTAs are template-driven — the same header/footer/sticky elements repeat on every page. The map below is the canonical set; the CSV is the exhaustive per-page expansion.
2.1 Global template CTAs (present on 377/377 pages)
CTA Text
CTA Type
Position
Destination URL
Dest Type
Journey Stage
Site logo
Image link
Header
/
Internal page
Awareness
OUR STORY
Nav item
Header
/our-story
Internal page
Decision
WORK
Nav item
Header
/projects
Internal page
Decision
INDUSTRIES
Nav item
Header
/industry
Internal page
Consideration
Contact
Nav item (button)
Header
/contact
Internal page
Conversion
(91) 8920-527-329
Nav item
Header
tel:8920-527-329
Phone
Conversion
hello@example-agency.com
Nav item
Header
mailto:hello@example-agency.com
Email
Conversion
Home / Our Story / Projects (07) / Services / Industries / Pricing / Blog / Free Resources / Contact
Nav item
Header (overlay menu)
respective internal pages
Internal page
Mixed
Book a call
Button (sticky, fixed bottom-right)
Persistent overlay
null on non-blog pages · ../contact on blog posts
Dead / Internal
Conversion (broken)
Let's talk
Form submit
End of page
Inline form → /thankyou
Form
Conversion
AI-first UX Design / SaaS UX Design / Web Development / Marketing Design / UX Strategy / Brand Identity / Web Design
Footer link
Footer
/services/{slug} (7)
Internal page
Consideration
AI & ML / SaaS / Fintech / Healthcare / E-commerce
Footer link
Footer
/industry/{slug} (5)
Internal page
Consideration
About / Work / Pricing
Footer link
Footer
/our-story, /projects, /pricing
Internal page
Decision
LinkedIn
Footer link
Footer
linkedin.com/company/[agency]
External site
Leak
Dribbble
Footer link
Footer
dribbble.com/[agency]
External site
Leak
Upwork
Footer link
Footer
upwork.com/agencies/[id]/
External site
Leak
Upwork / Dribbble / DesignRush badges (3 image links)
Image link
Footer
Upwork, dribbble.com/ux-ui-design-agency, designrush.com/agency/ui-ux-design
External site
Leak
© Copyright 2026 All Rights Reserved
Text link
Footer
[template-vendor].com
External site
Leak (template vendor)
Terms of service / Privacy policy / Referral policy
Footer link
Footer
/terms-of-use, /privacy-policy, /referral-policy
Internal page
—

Footer leak load: 7 external links on every one of 377 pages (LinkedIn, Dribbble ×2, Upwork ×2, DesignRush, template vendor) = 2,639 off-site exits available site-wide, versus 3 conversion links in the same footer region.
2.2 Page-specific CTAs by template
Homepage (/) — 24 page-specific CTAs
CTA Text
Type
Position
Destination
Dest Type
Stage
Let's talk
Button
Hero
/contact
Internal
Conversion
AI-First UX Design {01} … SaaS UX Design {07}
Text link ×7
Mid page
/services/{slug}
Internal
Consideration
See projects
Button
Mid page
/projects
Internal
Decision
5 featured case-study cards
Image/Text link ×5
Mid page
/projects/{slug}
Internal
Decision
All cases (07)
Button
Mid page
/projects
Internal
Decision
Schedule a consultation
Button
Mid page
/contact
Internal
Conversion
See all reviews on clutch
Text link
Mid page
clutch.co/profile/[agency]#reviews
External
Leak
See how we began
Button
Mid page
/our-story
Internal
Decision
View all industries
Button
Mid page
/industry
Internal
Consideration
Discover more reads
Button
Mid page
/blog
Internal
Awareness
3 blog cards
Text link ×3
Mid page
/blog/{slug}
Internal
Awareness
Ask a question
Button
End of page
/contact
Internal
Conversion
Book a call
Sticky button
Overlay
null — dead
—
Conversion (broken)
Let's talk
Form submit
End of page
Inline form → /thankyou
Form
Conversion

Service page (7 pages) — 1 page-specific CTA
| Ask a question | Button | End of page | /contact | Internal | Conversion |
That is the entire page-specific CTA inventory of a service page. No case-study links, no pricing link, no industry cross-sell, no mid-page CTA. Plus a dead sticky button.
Industry page (6 pages) — 1 page-specific CTA
| Ask a question | Button | Mid page (26%) | /contact | Internal | Conversion |
Pricing (/pricing) — 1 page-specific CTA
| Ask a question | Button | Mid page (31%) | /contact | Internal | Conversion | Three "Choose this plan" buttons do exist — at 8%, 15% and 22% scroll — plus a fourth "Let's talk" on the custom tier at 32%. All four render as <a> with no href, sit outside any form, and do nothing when clicked (verified by click test on a clean load with a 5-second wait). The only working CTA on the page is "Ask a question" at 69%.
About (/our-story) — 1 page-specific CTA
| Let's talk | Button | Mid page (24%) | /contact | Internal | Conversion |
Case study (13 pages) — 7 page-specific CTAs, 0 conversion CTAs
| 3 category tags | Text link | Mid page | /artificial-intelligence, /web-design, /saas | Internal (often empty pages) | Consideration | | Visit website | Button | Mid page | client's own site e.g. the client's own site | External | Leak | | More projects | Button | End of page | /projects | Internal | Decision | | 2 next-project cards | Text link | End of page | /projects/{slug} | Internal | Decision | | Book a call | Sticky | Overlay | null — dead | — | Conversion (broken) | | Let's talk | Form submit | End of page | Inline form → /thankyou | Form | Conversion | | (scroll-triggered modal) "Let's talk" | Form submit | Modal overlay | Inline form → /thankyou | Form | Conversion |
Blog post (230 pages) — CTA set per post
CTA Text
Type
Position
Destination
Stage
Author name
Text link
Above fold (3%)
/author/{slug}
Awareness
Back to blogs
Text link
Above fold (4%)
/blog
Awareness
Get Free Audit (71 posts)
Button
Above fold (4%)
/contact
Conversion
In-content conversion link (see 2.3)
Text link
In-content (5–7%)
/contact or cal.com/[handle]/quick-chat
Conversion
1 featured case-study card
Text link
In-content (7%)
/projects/{slug}
Decision
Book a call (230/230)
Button
End of article (avg 6%)
/contact
Conversion
Ask a question (198/230)
Button
End of page (avg 10%)
/contact
Conversion
Outbound citations / competitor links
Text link
In-content
external
Leak
Hidden full-blog index (234 links)
Text link
Hidden (not visible)
/blog/{slug} × 230
—

Blog posts are the only template where the sticky "Book a call" actually works (href="../contact").
Local landing — /web-design/{city} (40 pages) — 11 page-specific CTAs, 4 conversion
| Let's talk | Button | Hero | /contact | Conversion | | See projects / All cases (07) | Button | Mid page | /projects | Decision | | 5 case-study cards | Text link | Mid page | /projects/{slug} | Decision | | Schedule a consultation | Button | Mid page | /contact | Conversion | | Ask a question | Button | Mid page | /contact | Conversion | | Book your free web design audit | Button | End of page (44%) | /contact | Conversion |
This is the strongest-converting template on the site — 4 distinct conversion CTAs, an offer-led one ("free web design audit"), and portfolio proof in between. It is also the template with the lowest traffic potential.
Local landing — /ui-ux-design/{city} (39 pages) — same 4-CTA sequence
| Let's talk | Button | Hero | /contact | Conversion | | Schedule a consultation | Button | Mid page (22%) | /contact | Conversion | | Ask a question | Button | Mid page (25%) | /contact | Conversion | | Book your free UI/UX audit | Button | End of page (45%) | /contact | Conversion |
Same template and same 4-CTA conversion sequence as the /web-design/{city} twins — but all 39 are orphaned, with zero internal links pointing at them from anywhere on the site. They are reachable only via the sitemap and organic search.
Resources (/resources) — 5 page-specific CTAs, 0 conversion CTAs, 5 off-site
| The 7 Biggest UX Mistakes Killing SaaS Conversions | Text link | Mid page | [workspace].notion.site/... | External | | The Ultimate SaaS & Startup UX/UI Checklist | Text link | Mid page | [workspace].notion.site/... | External | | AI Onboarding Playbook | Text link | Mid page | [workspace].notion.site/... | External | | How UX Debt Evolves Into Tech Debt | Text link | Mid page | [workspace].notion.site/... | External | | Design Debt Audit | Text link | Mid page | docs.google.com/spreadsheets/... | External |
Every lead magnet is an ungated public link that ejects the user to Notion or Google Sheets. Zero email capture, zero return path.
Author page (7 pages) — 32–49 links, 0 conversion CTAs
Nothing but a bio and a list of that author's blog posts. No "work with us", no contact link.
Thank you (/thankyou) — 1 page-specific CTA
| Back to homepage | Button | Mid page | / | Internal | — | No calendar booking, no case study, no resource, no expectation-setting next step.
Contact (/contact) — the conversion destination
Zero navigation, zero footer (only the logo links home) — a deliberately isolated conversion page. Correct pattern.
Tab 1 "Send a Brief" → form: Your Name*, Work Email*, "What's the #1 problem your product has right now?"*, How did you get to know about us? (optional), Location, Opted services (6 checkboxes) → submits to /thankyou.
Tab 2 "Book a Call" → embedded cal.com/[handle]/30min, "30 Min Meeting", Google Meet.
Trust: Clutch 4.9/5.0 badge above the fold.
Legal (3 pages) — 0 CTAs of any kind beyond global chrome.
2.3 Conversion CTA label inventory (the fragmentation problem)
Across 230 blog posts there are 30+ distinct labels for what is functionally the same action:
Label
Occurrences
Avg position
Destination
Book a call
230
6%
/contact
Ask a question
198
10%
/contact
Get Free Audit
71
4%
/contact
Book a discovery call →
10
5%
/contact
Start your project with [Agency]
9
6%
/contact
Let's talk →
8
5%
/contact
book a discovery call with [Agency]
6
5%
cal.com/[handle]/quick-chat
Book a Free UX Audit
5
6%
/contact
Book a 20-minute strategy call
4
6%
cal.com/.../quick-chat
Book a 20-minute call / consultation / discovery call
6
5–6%
cal.com/.../quick-chat
let's talk / Let's talk. / Let's Talk → / Let's Talk
9
5–6%
/contact
Book a discovery call (× 5 casing/punctuation variants)
8
6%
mixed
Talk to [Agency] about your brief →
1
7%
/contact
Work with [Agency] →
1
5%
/contact
Start a conversation with [Agency] →
1
7%
/contact
Let's talk about your product →
1
6%
/contact
our team at [Agency] / our discovery call
2
5–6%
/contact
[EMPTY] (no anchor text)
1
7%
/contact

Conversion destinations from blog: /contact 545 links · cal.com/[handle]/quick-chat 54 links · and 7 mis-targeted CTAs pointing at the wrong domain entirely (see Phase 5).
Only 56 of 230 blog posts (24%) offer the low-friction cal.com booking; the other 174 route only to the form page.
2.4 Journey-stage distribution of all mapped CTAs
Journey Stage
CTAs
Share
Consideration
8,637
35.2%
Awareness
5,947
24.2%
Decision
4,802
19.6%
Leak / Off-site
3,083
12.6%
Conversion
2,069
8.4%

There are 1.5 off-site exits available for every conversion CTA on the site.

PHASE 3 — FUNNEL MAPPING
Conversion endpoints, for reference:
C1 — /contact "Send a Brief" form → /thankyou
C2 — /contact "Book a Call" tab → cal.com/[handle]/30min
C3 — inline page form ("Let's bring your vision to life" → "Let's talk") → /thankyou
C4 — scroll-triggered modal form ("Ready to discuss your project with us?") → /thankyou
C5 — cal.com/[handle]/quick-chat (direct from 56 blog posts)
C6 — mailto:hello@example-agency.com / tel:8920-527-329 (header, every page)

FUNNEL 1: Homepage Hero Direct Funnel
Entry: / · Entry source: Direct / Brand search / Referral
Step 1: / → CTA clicked: "Let's talk" (hero) → lands on: /contact
Step 2: /contact → CTA: "Send a Brief" submit → lands on: /thankyou Conversion: C1 form submission · Funnel depth: 2 pages · Type: Form
FUNNEL 2: Homepage Hero → Calendar Funnel
Entry: / · Source: Direct / Brand
Step 1: / → "Let's talk" → /contact
Step 2: /contact → tab "Book a Call" → cal.com/[handle]/30min (in-page embed) Conversion: C2 calendar booking · Depth: 2 · Type: Calendly-equivalent
FUNNEL 3: Homepage Mid-Page Consultation Funnel
Entry: / · Source: Direct / Organic
Step 1: / → "Schedule a consultation" (after case-study strip) → /contact
Step 2: /contact → form or calendar → /thankyou or cal.com Conversion: C1/C2 · Depth: 2 · Type: Form / Calendly
FUNNEL 4: Homepage Inline Form Funnel (zero-click-out)
Entry: / · Source: Any
Step 1: / → scroll to "Let's bring your vision to life" → fill Name / E-mail / Message → "Let's talk" Conversion: C3 → /thankyou · Depth: 1 · Type: Form Shortest funnel on the site.
FUNNEL 5: Homepage → Services → Contact Funnel
Entry: / · Source: Direct / Organic
Step 1: / → "SaaS UX Design {07}" → /services/saas-ux-design-...
Step 2: /services/saas-ux-design-... → "Ask a question" (only CTA on page) → /contact
Step 3: /contact → form/calendar → /thankyou Conversion: C1/C2 · Depth: 3 · Type: Form / Calendly
FUNNEL 6: Homepage → Work → Case Study → DEAD END
Entry: / · Source: Direct / Organic
Step 1: / → "See projects" → /projects
Step 2: /projects → case-study card → /projects/{case-study-slug}
Step 3: /projects/{case-study-slug} → no conversion CTA exists on the page. Options are "Visit website" (exits to the client’s own site), "More projects" (loop), or a next-project card (loop). Conversion: Exit or Loop — unless the user scrolls into the inline form (C3) or the scroll modal fires (C4) Depth: 3 → loop/exit · Type: Exit / Loop
FUNNEL 7: Case Study Modal-Rescue Funnel
Entry: /projects/{slug} · Source: Internal navigation / Organic
Step 1: user scrolls to ~70% of a case study
Step 2: scroll-triggered modal fires — "Ready to discuss your project with us?" (Clutch/Dribbble/Upwork badges) → Name / E-mail / Tell us about your project → "Let's talk" Conversion: C4 → /thankyou · Depth: 1 · Type: Form (interruptive) This modal is currently the only conversion mechanism on case study pages that is actually surfaced to the user.
FUNNEL 8: Homepage → Industries → Industry Page → Contact
Entry: / · Source: Direct / Organic
Step 1: / → "View all industries" → /industry
Step 2: /industry → "Explore more" → /industry/fintech-ux-design-...
Step 3: /industry/fintech-... → "Ask a question" → /contact
Step 4: /contact → form/calendar → /thankyou Conversion: C1/C2 · Depth: 4 · Type: Form / Calendly
FUNNEL 9: Navigation-Led Direct Funnel
Entry: any page · Source: Any
Step 1: any page → header "Contact" button → /contact
Step 2: /contact → form/calendar → /thankyou Conversion: C1/C2 · Depth: 2 · Type: Form / Calendly Available on 377/377 pages.
FUNNEL 10: Header Phone / Email Funnel
Entry: any page · Source: Any
Step 1: any page → header "(91) 8920-527-329" or "hello@example-agency.com" → dialler / mail client Conversion: C6 · Depth: 1 · Type: Phone / Email
FUNNEL 11: Blog → Contact Funnel (the volume funnel)
Entry: /blog/{slug} · Source: Organic search (230 posts, primary acquisition channel)
Step 1: /blog/ai-prototyping-tools → "Get Free Audit" (above fold) OR "Book a call" (end of article) OR "Ask a question" (page end) → /contact
Step 2: /contact → form/calendar → /thankyou Conversion: C1/C2 · Depth: 2 · Type: Form / Calendly
FUNNEL 12: Blog → Direct Calendar Funnel (best funnel on the site)
Entry: /blog/{one of 56 posts} · Source: Organic search
Step 1: /blog/what-is-ux-research → in-content "book a call with us" → cal.com/[handle]/quick-chat Conversion: C5 calendar booking · Depth: 1 · Type: Calendar booking One click from article to booked call. Available on only 24% of posts.
FUNNEL 13: Blog → Case Study → Loop Funnel
Entry: /blog/{slug} · Source: Organic
Step 1: blog post → featured case-study card → /projects/{slug}
Step 2: /projects/{slug} → no conversion CTA → "More projects" → /projects
Step 3: /projects → another case study → loop Conversion: Loop / Exit · Depth: 3+ · Type: Exit
FUNNEL 14: Blog → Author → Blog Loop Funnel
Entry: /blog/{slug} · Source: Organic
Step 1: blog post → author byline → /author/harpreet-singh
Step 2: /author/harpreet-singh → 49 blog links, zero conversion CTAs → /blog/{another} Conversion: Loop · Depth: 2+ · Type: Exit / Loop
FUNNEL 15: Blog → Competitor Leak Funnel
Entry: /blog/top-10-ux-design-agencies-in-los-angeles (and ~15 similar listicles) · Source: Organic, high commercial intent
Step 1: post → in-content links to Clay, WANDR, Ramotion, Interactivism, Isadora, Work & Co, Use All Five, SPINX, Goji Labs → competitor websites Conversion: Exit to a competitor · Depth: 1 · Type: Exit best-landing-page-design-examples carries 30 external links against 3 conversion CTAs.
FUNNEL 16: Local SEO Funnel (web-design cities)
Entry: /web-design/new-york/ · Source: Organic local search
Step 1: LP → "Let's talk" (hero) OR "Schedule a consultation" OR "Ask a question" OR "Book your free web design audit" → /contact
Step 2: /contact → form/calendar → /thankyou Conversion: C1/C2 · Depth: 2 · Type: Form / Calendly Best-designed funnel structurally; 40 pages, reachable at depth 3.
FUNNEL 17: Orphaned Local SEO Funnel (ui-ux-design cities)
Entry: /ui-ux-design/{city} (39 pages) · Source: Organic search only — zero internal inbound links
Step 1: LP → "Let's talk" / "Schedule a consultation" / "Ask a question" / "Book your free audit" → /contact
Step 2: /contact → form/calendar → /thankyou Conversion: C1/C2 · Depth: 2 · Type: Form / Calendly Structurally identical to F16 and equally strong — but starved of internal link equity, so the funnel almost never receives traffic.
FUNNEL 18: Pricing Funnel
Entry: /pricing · Source: Internal nav / Organic "ux design agency pricing"
Step 1: /pricing → "Ask a question" (the only CTA, at 31% depth) → /contact
Step 2: /contact → form/calendar → /thankyou Conversion: C1/C2 · Depth: 2 · Type: Form The three per-tier "Choose this plan" buttons are dead (no href, no handler). The only working CTA sits 47% further down the page.
FUNNEL 19: About Page Funnel
Entry: /our-story · Source: Nav / Organic brand search
Step 1: /our-story → "Let's talk" → /contact → /thankyou Conversion: C1/C2 · Depth: 2 · Type: Form
FUNNEL 20: Resources / Lead-Magnet Funnel → LEAK
Entry: /resources · Source: Nav / Organic
Step 1: /resources → "The Ultimate SaaS & Startup UX/UI Checklist" → [workspace].notion.site (external, ungated) Conversion: Exit with no email captured · Depth: 1 · Type: Exit All 5 lead magnets behave this way.
FUNNEL 21: Sticky Button Funnel → BROKEN
Entry: any non-blog page · Source: Any
Step 1: user clicks the persistent yellow "Book a call" pill → nothing happens (no href, no handler, no scroll, no modal) Conversion: None — dead end in place · Depth: 0 · Type: Broken Verified live on /, /services/saas-ux-design-..., /projects/{case-study-slug}; href=null also confirmed on /our-story, /industry/fintech-..., /pricing, /web-design/new-york/.
FUNNEL 22: Post-Conversion (Thank You) Funnel → DEAD END
Entry: /thankyou (after any form submit)
Step 1: /thankyou → only CTA is "Back to homepage" → / Conversion: Already converted · Depth: 1 → loop to top of funnel No calendar upsell, no case study, no resource, no "what happens next".
FUNNEL 23: Footer Social Leak Funnel
Entry: any page · Source: Any
Step 1: footer → LinkedIn / Dribbble ×2 / Upwork ×2 / DesignRush / template vendor → off-site Conversion: Exit · Depth: 1 · Type: Exit 7 exits available on all 377 pages.
FUNNEL 24: Broken-Link Funnel
Entry: 13 blog posts · Source: Organic
Step 1: post → in-content internal link → 404 (e.g. /projects/:EvxErjRB0, /blog/what-p) Conversion: Exit · Depth: 1 · Type: Exit
FUNNEL 25: Wrong-Domain CTA Funnel
Entry: 7 blog posts · Source: Organic
Step 1: post → "Book a discovery call →" → claude.ai/contact; or "Let's Talk →" → [wrong-domain]/contact; or "hello@[misspelled-domain-1]" → non-existent mailbox Conversion: Lead sent to the wrong company or lost entirely · Depth: 1 · Type: Exit
FUNNEL 26: Empty-Filter-Page Funnel
Entry: 13 portfolio-filter pages returning no projects (/health-care, /hr-tech, /web-3, /tools-resources, /finance, /branding, /development, /ux-design, /ai-design, /saas-design, /brand-design, /market-place, /support) · Source: Organic / case-study category tags
Step 1: user lands → empty project grid, no unique content, no conversion CTA, dead sticky button Conversion: Exit · Depth: 0 · Type: Exit
FUNNEL 27: Case Study Category Funnel → part dead end
Entry: /projects/{slug} · Source: Internal
Step 1: case study → category tag "SaaS" / "Web Design" / "Artificial Intelligence" → /saas, /web-design, /artificial-intelligence
Step 2: these are portfolio-filter pages with no conversion CTA; three of the family (/health-care, /hr-tech, /web-3) are blank Conversion: Loop or Exit · Depth: 2–3

PHASE 4 — FUNNEL QUALITY ANALYSIS
Funnel Name
Depth
Friction Points
Missing CTAs
CTA Clarity
Conv. Probability
Top Issue
Recommended Fix
Priority
F1 Homepage Hero Direct
2
None material
—
Strong
High
Hero CTA "Let's talk" is vague vs. an offer
A/B test "Book a free 30-min UX audit"
Medium
F2 Homepage Hero → Calendar
2
Calendar hidden behind a tab click
Calendar not offered before /contact
Strong / Moderate
High
Booking is 3 clicks deep
Add "Book a call" (cal.com) as a second hero button
High
F3 Homepage Consultation
2
CTA buried at 36% scroll
—
Strong
High
Placement
Repeat after the Clutch review block
Medium
F4 Homepage Inline Form
1
3 fields, low friction
—
Moderate ("Let's talk" ≠ obvious submit)
High
Submit label doesn't state outcome
Change to "Send my brief"
Low
F5 Homepage → Service → Contact
3
Service page has exactly one CTA, at page end
No hero CTA, no case-study link, no pricing link on service pages
Weak
Low
7 service pages carry 1 CTA each
Add hero CTA + mid-page proof CTA + end CTA to service template
Critical
F6 Homepage → Work → Case Study
3 → loop
Case study terminates with "Visit website" (off-site) and loop links
No "Work with us" CTA on any of 13 case studies
Weak
Low
Highest-intent proof page has zero conversion CTA
Add "Get results like this — book a call" block after Results
Critical
F7 Case Study Modal Rescue
1
Interruptive; fires mid-read
—
Moderate
Medium
Modal is compensating for a missing in-page CTA
Keep, but add the in-page CTA so the modal isn't load-bearing
High
F8 Homepage → Industries → Industry → Contact
4
4 steps; industry page has 1 CTA
No case-study or service cross-link on industry pages
Weak
Low
Too deep + single weak CTA
Add hero CTA to industry pages; link matching case studies
High
F9 Navigation-Led Direct
2
None
—
Strong
High
Header "Contact" is a low-commitment label
Test "Book a call" in the header
Low
F10 Header Phone / Email
1
Indian number shown to a US-targeted site; no country context
—
Moderate
Medium
Phone friction for US buyers
Add "+91" formatting and a US-hours note, or hide phone on US LPs
Low
F11 Blog → Contact
2
3 CTAs but all route to a form page
Only 24% offer a calendar
Moderate (30+ labels)
Medium
Label fragmentation destroys measurement
Standardise to 2 labels sitewide
High
F12 Blog → Direct Calendar
1
None
Missing on 174 posts
Strong
High
Best funnel, worst coverage
Roll cal.com/quick-chat in-content CTA to all 230 posts
Critical
F13 Blog → Case Study → Loop
3+
Case study dead-ends
Case study conversion CTA
Weak
Low
Sends warm traffic into a dead end
Fix case study template (same as F6)
Critical
F14 Blog → Author → Blog Loop
2+
Author page = 49 blog links, no CTA
No CTA at all on 7 author pages
None
Low
Pure circulation, no exit to conversion
Add "Work with {name}'s team → Book a call" to author template
Medium
F15 Blog → Competitor Leak
1
9 competitor links in one post
—
N/A
Negative
High-intent listicle traffic handed to competitors
rel="nofollow" + open in new tab + sticky in-article CTA
High
F16 Local SEO (web-design)
2
None material
—
Strong (4 CTAs incl. an offer)
High
Best template, weakest distribution
Use as the master template for service/industry pages
High
F17 Local SEO (ui-ux) orphaned
2
39 pages with zero internal inbound links
—
Strong (same 4-CTA sequence as F16)
High if reached
A well-built funnel that nothing links to
Add a city index page; link from /services, footer and the /web-design/{city} twins
High
F18 Pricing
2
All 3 tier CTAs are dead; only working CTA at 69%
— (they exist, they are broken)
Broken
Zero at the tier
Decision-stage intent is captured by three buttons that do nothing
Bind href on "Choose this plan" ×3 + the custom-tier "Let's talk"
Critical
F19 About
2
One CTA at 24%
No end-of-page CTA
Moderate
Medium
Trust page doesn't close
Add team-photo CTA block at page end
Medium
F20 Resources / Lead Magnets
1
All 5 magnets exit to Notion/Sheets ungated
No email gate, no return path
Weak
Negative
Giving away assets and capturing nothing
Gate behind email; deliver by mail; redirect to /thankyou
Critical
F21 Sticky "Book a call"
0
Button does nothing on ~147 pages
—
Broken
Zero
The most persistent CTA on the site is dead
Set href="/contact" (or cal.com popup) on the global component
Critical
F22 Thank You
1
Only "Back to homepage"
No booking upsell, no next step
Weak
N/A
Wasting the highest-intent moment on the site
Embed cal.com + "what happens next" + 2 case studies
High
F23 Footer Social Leak
1
7 off-site links on every page
—
N/A
Negative
2,639 site-wide exits vs 3 conversion links in footer
Move badges above footer as trust proof; target="_blank" + nofollow
Medium
F24 Broken Links
1
14 hard 404s incl. 2 raw CMS placeholders
—
Broken
Zero
404s inside high-traffic blog posts
Fix the 14 slugs; add a 404 page with a CTA
High
F25 Wrong-Domain CTAs
1
Leads sent to claude.ai, agency.co, [misspelled-domain]
—
Broken
Zero
Live CTAs sending leads to other companies
Correct 7 links immediately
Critical
F26 Empty Filter Pages
0
13 filter pages return no projects, no unique content, no CTA
Conversion CTA + content on all 13
None
Zero
21 portfolio-filter pages, none with a CTA; 13 of them are empty
Add the standard conversion block to the filter template; 410/redirect the 13 empty ones
High
F27 Case Study Category
2–3
Category pages have no CTA; 3 are blank
Conversion CTA
None
Low
Sub-funnel of the case-study dead end
Add the standard conversion block to filter pages
Medium


PHASE 5 — DEAD END AND LEAK DETECTION
Page URL
Issue Type
Description
Impact
Fix
All 13 /projects/{slug} case studies
CTA Gap
No "work with us" CTA anywhere in the page body. Only exits are "Visit website" (off-site), "More projects" (loop) and 2 next-project cards
Critical — highest-intent proof pages convert nobody directly
Add a post-Results conversion block: headline + "Book a call" (cal.com) + "Get a free audit" (form)
All 7 /services/{slug} pages
Weak CTA
Exactly one CTA ("Ask a question") at end of page. No hero CTA, no proof link, no pricing link
Critical
Clone the /web-design/{city} template: hero CTA, mid-page case studies, offer CTA at end
All 6 /industry/{slug} pages
Broken CTA + Weak CTA
Nothing clickable from 5% to 75%. The first CTA after that dead zone — "Schedule a consultation" at 75% — has no href and is click-tested dead. Only "Ask a question" at 79% works
Critical
Bind "Schedule a consultation"; add a hero CTA and case-study cross-links
/pricing
Broken CTA
"Choose this plan" ×3 (8% / 15% / 22%) and the custom-tier "Let's talk" (32%) all have no href and no handler — click-tested dead. Only "Ask a question" at 69% works
Critical
Bind all four to /contact, pre-filling the "Opted services" checkboxes
All 7 /author/{name} pages
No CTA
32–49 links, all to blog posts. Zero conversion CTAs
Medium
Add "Work with {name}'s team" CTA to the author template
/thankyou
Dead End
Only "Back to homepage". No booking, no expectation-setting, no content
High
Embed cal.com booking + "what happens next" + 2 case studies
/terms-of-use, /privacy-policy, /referral-policy
Dead End
Zero page-specific links
Low
Acceptable; ensure the global footer renders
/resources
Broken CTA + Leak
All 7 lead-magnet buttons are dead — "Get the UX guide" (12%), "Go to the checklist" (21%), "Get the playbook" (29%), "Find my UX leaks" (38%), "Start the audit" (46%), "Go to the checklist" (55%), "Go to the playbook" (64%), plus "Load more" (73%) — no href, click-tested dead. The only working path is 5 small date cards at 67–72% that exit ungated to [workspace].notion.site / docs.google.com
Critical
Bind all 7 buttons to an email gate; deliver by mail; land on /thankyou
/tools-resources
Dead End / No CTA
Renders an empty portfolio filter under a "tools & resources" URL; orphaned
Medium
Build it or remove from sitemap
Every page (footer)
Leak
7 external links (LinkedIn, Dribbble ×2, Upwork ×2, DesignRush, template vendor) × 377 pages
High
Convert badges to non-linked trust proof; target="_blank" rel="nofollow" on the rest
blog/top-10-ux-design-agencies-in-los-angeles
Leak
9 direct competitor links (Clay, WANDR, Ramotion, Work & Co, SPINX, Goji Labs, …)
Critical
rel="nofollow", target="_blank", add sticky in-article CTA
blog/best-landing-page-design-examples
Leak
30 external links vs 3 conversion CTAs
High
Same
blog/ai-tools-for-ui-ux-designers-that-save-hours-of-work
Leak
22 external links vs 2 conversion CTAs
High
Same
blog/interactive-website-examples
Leak
21 external links vs 2 conversion CTAs
High
Same
blog/best-b2b-web-design-agencies-to-hire, paywall-examples, best-website-design-examples-to-inspire, how-to-develop-an-ai-powered-saas-product, ecommerce-website-designs-examples, best-ai-web-design-tools, dc-web-design-agency, black-and-orange-website, infographic-design-services, branding-agencies-for-startups, graphic-design-agency
Leak
9–15 external links each
Medium–High
Same
blog/no-code-website-design-agency
Broken Link
CTA "Book a discovery call →" points to https://claude.ai/contact
Critical
Change to /contact
blog/web-design-agency-pricing-guide
Broken Link
CTA "Let's Talk →" points to https://[wrong-domain]/contact (wrong domain)
Critical
Change to /contact
blog/what-is-a-ux-prototype-..., blog/wireframes-vs-prototypes-in-ux-design
Broken Link
CTA mailto:hello@[misspelled-domain-1] — non-existent mailbox
Critical
Change to hello@example-agency.com
blog/integrating-ai-into-saas-ux-best-practices-and-strategies
Broken Link
CTA mailto:hello@[misspelled-domain-2] — non-existent mailbox
Critical
Change to hello@example-agency.com
5 blog posts
Broken Link
/projects/:EvxErjRB0 — raw Framer CMS placeholder → 404
High
Bind the CMS field or remove
blog/ai-ux-vs-traditional-ux-...
Broken Link
/author/:MmG2T32Ts → 404
Medium
Same
blog/what-is-a-ux-design-brief
Broken Link
/blog/what-p and /blog/design-systems-for-s — truncated hrefs → 404
High
Fix both slugs
blog/user-journey-vs-user-flow
Broken Link
2 links with body text concatenated into the slug → 404
High
Fix
blog/how-to-do-a-ux-audit-...
Broken Link
...-foundershow → 404
High
Fix
blog/ai-prototyping-tools (×2), interaction-designer, ai-design-agency-vs-traditional-agency, what-is-design-thinking, vertical-saas, how-to-promote-your-website, best-design-subscription-agency
Broken Link
8 further 404s from wrong/renamed slugs
High
Fix or 301
blog/company-rebranding (8), ux-design-agency-seattle (2), best-enterprise-ux-design-agencies, heuristic-evaluation, design-strategy
Broken Link
Links use http://example-agency.com — forced redirect hop
Medium
Rewrite to https://example-agency.com
/ux-design, /ai-design, /saas-design, /brand-design, /tools-resources, /finance, /health-care, /hr-tech, /market-place, /web-3, /branding, /development, /support
No CTA / Dead End
Portfolio-filter pages that return zero projects — 477 words of pure header/footer, no unique content, no conversion CTA, indexable and in the sitemap
High
Populate or return 410 / redirect to /projects
All 21 portfolio-filter pages (/web-design, /saas, /e-commerce, /artificial-intelligence, …)
CTA Gap
Not one of the 21 filter pages carries a conversion CTA, yet case-study category tags route users into them
High
Add the standard conversion block to the filter template
All 39 /ui-ux-design/{city}
Dead End (inbound)
Zero internal inbound links from anywhere on the site
High
Link from /services, footer, and a city index page
/author, /ai-design, /brand-design, /saas-design, /ux-design, /tools-resources
Dead End (inbound)
Orphaned
Medium
Link or remove
Every non-blog page (~147)
Broken CTA
Sticky "Book a call" pill has href=null and no click handler — verified dead on /, service, case study, industry, about, pricing, local LP
Critical
Wire the global component to /contact or a cal.com popup
/support
CTA Gap
Renders the Projects category filter under a "support" URL; no support content, no CTA
Medium
Repurpose or remove
blog/best-ux-design-tools, homepage-design-principles, how-to-create-a-product-roadmap, what-is-responsive-website-design
Weak CTA
/contact links carry a hard-coded stale _gl GA linker param
Low
Strip the param


PHASE 6 — PRIORITY FUNNEL RECOMMENDATIONS
TOP 3 HIGHEST-CONVERTING FUNNELS (as currently built)
1. F12 — Blog → Direct Calendar (cal.com/[handle]/quick-chat) Shortest possible path: one click from an in-content link straight into a booking calendar. No intermediate page, no form. Highest intent-to-action ratio on the site. Live on 56 posts.
2. F16 — Local SEO Funnel (/web-design/{city} → /contact) The only template that runs a full CRO sequence: hero CTA → portfolio proof → "Schedule a consultation" → "Ask a question" → offer-led close ("Book your free web design audit"). 4 conversion CTAs, clear stage progression, 2-step depth.
3. F1/F2 — Homepage Hero → /contact Two clicks to either a brief form or a cal.com booking, with a Clutch 4.9 badge above the fold on the contact page and a nav-free layout that eliminates escape routes. Best-built conversion page on the site.
TOP 3 BROKEN FUNNELS (highest priority to fix)
1. F21 — The Sticky "Book a call" Funnel The most persistent, highest-intent CTA on the site is dead on roughly 147 pages including the homepage, all 7 service pages, all 13 case studies and all 6 industry pages. Every click is a lost lead with no feedback to the user. Fix: one attribute on one global Framer component. Highest impact-to-effort ratio in this entire audit.
2. F6/F13 — Case Study Funnel 13 case studies — the strongest proof assets the agency has — contain no conversion CTA at all. Warm traffic arriving from the homepage, blog and portfolio hub either loops back to /projects or exits to the client's website via "Visit website". Currently rescued only by an interruptive scroll modal.
3. F20 — Resources / Lead-Magnet Funnel Five genuine lead magnets are published as ungated public Notion and Google Sheets links. Every download is a lead given away for free with no email captured and no return path to the site.
TOP 5 CRO QUICK WINS (each under 1 hour)
1. Wire the sticky "Book a call" button Page: global Framer component (affects ~147 pages) → Current state: href=null, click does nothing → Recommended change: set link to /contact, or attach a cal.com popup for cal.com/[handle]/30min → Expected impact: recovers 100% of currently-lost sticky-CTA clicks; on an agency site a persistent sticky CTA typically drives 10–20% of all conversions.
2. Fix the 7 wrong-domain CTAs Pages: blog/no-code-website-design-agency (→claude.ai/contact), blog/web-design-agency-pricing-guide (→[wrong-domain]/contact), blog/what-is-a-ux-prototype-... + blog/wireframes-vs-prototypes-in-ux-design (→hello@[misspelled-domain-1]), blog/integrating-ai-into-saas-ux-... (→hello@[misspelled-domain-2]) → Current state: live CTAs sending qualified leads to another company or a non-existent mailbox → Recommended change: repoint all to /contact and hello@example-agency.com → Expected impact: recovers 100% of the leads these 7 CTAs currently destroy.
3. Add a conversion block to the case study template Page: /projects/{slug} template (13 pages) → Current state: page ends with "Visit website" (off-site) and next-project loop cards → Recommended change: insert after the Results section — "Want results like this? Book a 30-min call" → cal.com/[handle]/30min, plus a secondary "Get a free UX audit" → /contact → Expected impact: converts the site's highest-intent page type, currently at effectively 0% direct conversion.
4. Bind the four dead CTAs on /pricing Page: /pricing → Current state: "Choose this plan" on all three tiers, plus the custom-tier "Let's talk", have no href and no click handler — every click does nothing → Recommended change: bind all four to /contact, pre-filling the matching "Opted services" checkbox → Expected impact: recovers 100% of clicks on the page's only decision-stage CTAs.
5. Roll the in-content cal.com CTA to all 230 blog posts Pages: the 174 blog posts without a calendar link → Current state: only 56 posts (24%) offer one-click booking; the rest route to a form page → Recommended change: standardise one in-content CTA block — "Book a 30-min UX audit call" → cal.com/[handle]/quick-chat — after the first H2 of every post, and collapse the 30+ CTA label variants to two ("Book a call" and "Get a free audit") → Expected impact: extends the site's best-performing funnel across 4× more traffic and makes CTA performance measurable for the first time.

PHASE 7 — FULL FUNNEL VISUALISATION
GLOBAL CHROME (present on all 377 pages)
├── Header: "Contact" ────────────────────────────→ [/contact] ──→ CONVERSION (form or cal.com)
├── Header: "(91) 8920-527-329" ──────────────────→ tel: ────────→ CONVERSION (phone)
├── Header: "hello@example-agency.com" ────────────────→ mailto: ─────→ CONVERSION (email)
├── Header nav: Our Story / Work / Industries / Services / Pricing / Blog / Free Resources
├── STICKY: "Book a call" ────────────────────────→ ✖ DEAD (href=null) on ~147 non-blog pages
│                                                  └─→ [/contact] only on blog posts
├── Inline form "Let's bring your vision to life" → "Let's talk" → [/thankyou] → CONVERSION
├── Scroll modal "Ready to discuss your project?" → "Let's talk" → [/thankyou] → CONVERSION
└── Footer: 7 external links ─────────────────────→ ✖ LEAK (LinkedIn, Dribbble ×2, Upwork ×2,
                                                             DesignRush, template vendor)

[HOMEPAGE /]
├── CTA: "Let's talk" (hero) ─────────────────────→ [/contact] ──→ CONVERSION
├── CTA: "Schedule a consultation" ───────────────→ [/contact] ──→ CONVERSION
├── CTA: "Ask a question" (end) ──────────────────→ [/contact] ──→ CONVERSION
├── CTA: "See all reviews on clutch" ─────────────→ clutch.co ───→ ✖ LEAK
├── CTA: "AI-First UX Design {01}" … "{07}" ──────→ [SERVICE PAGE ×7]
│   └── CTA: "Ask a question" (only CTA) ─────────→ [/contact] ──→ CONVERSION
│       └── ✖ CTA GAP: no hero CTA, no proof link, no pricing link
├── CTA: "See projects" / "All cases (07)" ───────→ [/projects]
│   ├── filter: Web Design / Mobile App / SaaS / Ecommerce → [VERTICAL LP] → ✖ NO CTA (3 blank)
│   └── 13 case-study cards ──────────────────────→ [CASE STUDY]
│       ├── CTA: "Visit website" ─────────────────→ client site ─→ ✖ LEAK
│       ├── CTA: "More projects" ─────────────────→ [/projects] ─→ ↺ LOOP
│       ├── 2 next-project cards ─────────────────→ [CASE STUDY] ─→ ↺ LOOP
│       ├── category tags ────────────────────────→ [VERTICAL LP] → ✖ NO CTA
│       └── ✖ CTA GAP: no conversion CTA — rescued only by scroll modal
├── CTA: "View all industries" ───────────────────→ [/industry]
│   ├── CTA: "Let's talk" ────────────────────────→ [/contact] ──→ CONVERSION
│   └── CTA: "Explore more" ×6 ───────────────────→ [INDUSTRY PAGE]
│       └── CTA: "Ask a question" (only CTA) ─────→ [/contact] ──→ CONVERSION
├── CTA: "See how we began" ──────────────────────→ [/our-story]
│   └── CTA: "Let's talk" ────────────────────────→ [/contact] ──→ CONVERSION
├── CTA: "Discover more reads" / 3 blog cards ────→ [BLOG POST]
└── Footer: "Pricing" ────────────────────────────→ [/pricing]
    └── CTA: "Ask a question" (only CTA) ─────────→ [/contact] ──→ CONVERSION
        └── ✖ 3 tier CTAs + custom-tier CTA are DEAD (no href)

[BLOG POST] × 230  (primary organic entry)
├── CTA: "Get Free Audit" (above fold, 71 posts) ─→ [/contact] ──→ CONVERSION
├── In-content CTA (5–7%) ────────────────────────→ [/contact] (174 posts)  ──→ CONVERSION
│                                                  └→ cal.com/quick-chat (56) ──→ CONVERSION ★ best
├── CTA: "Book a call" (end of article, 230/230) ─→ [/contact] ──→ CONVERSION
├── CTA: "Ask a question" (page end, 198/230) ────→ [/contact] ──→ CONVERSION
├── STICKY "Book a call" ─────────────────────────→ [/contact] ──→ CONVERSION (works here only)
├── Author byline ────────────────────────────────→ [AUTHOR PAGE]
│   └── 32–49 blog links, ✖ ZERO CTAs ────────────→ [BLOG POST] ─→ ↺ LOOP
├── 1 featured case-study card ───────────────────→ [CASE STUDY] ─→ ↺ LOOP / dead end
├── "Back to blogs" ──────────────────────────────→ [/blog] ─────→ ↺ LOOP
├── Outbound citations & competitor links ────────→ external ────→ ✖ LEAK
│   └── worst: top-10-ux-design-agencies-in-los-angeles (9 competitors),
│              best-landing-page-design-examples (30 links)
├── ✖ 14 in-content links → 404
└── ✖ 7 CTAs → claude.ai / agency.co / agency.studio / agency.com

[/resources]
├── "The 7 Biggest UX Mistakes…" ─────────────────→ notion.site ─→ ✖ LEAK (ungated)
├── "The Ultimate SaaS & Startup UX/UI Checklist" ─→ notion.site ─→ ✖ LEAK (ungated)
├── "AI Onboarding Playbook" ─────────────────────→ notion.site ─→ ✖ LEAK (ungated)
├── "How UX Debt Evolves Into Tech Debt" ─────────→ notion.site ─→ ✖ LEAK (ungated)
└── "Design Debt Audit" ──────────────────────────→ google sheets → ✖ LEAK (ungated)

[LOCAL LP /web-design/{city}] × 40   ★ strongest template
├── CTA: "Let's talk" (hero) ─────────────────────→ [/contact] ──→ CONVERSION
├── CTA: "See projects" / 5 case cards ───────────→ [/projects] / [CASE STUDY]
├── CTA: "Schedule a consultation" ───────────────→ [/contact] ──→ CONVERSION
├── CTA: "Ask a question" ────────────────────────→ [/contact] ──→ CONVERSION
├── CTA: "Book your free web design audit" ───────→ [/contact] ──→ CONVERSION
└── ✓ all 40 carry the full 4-CTA conversion sequence

[LOCAL LP /ui-ux-design/{city}] × 39   ✖ ALL ORPHANED (zero internal inbound links)
├── CTA: "Let's talk" (hero) ─────────────────────→ [/contact] ──→ CONVERSION
├── CTA: "Schedule a consultation" ───────────────→ [/contact] ──→ CONVERSION
├── CTA: "Ask a question" ────────────────────────→ [/contact] ──→ CONVERSION
├── CTA: "Book your free UI/UX audit" ─────→ [/contact] ──→ CONVERSION
└── ✖ 39/39 receive zero internal links — organic-only funnel

[/contact]   ← the single conversion destination (no nav, no footer)
├── Tab "Send a Brief" → Name / Work Email / #1 problem / source / location /
│                        6 service checkboxes → submit ──────────→ [/thankyou]
└── Tab "Book a Call" → cal.com/[handle]/30min (Google Meet) ─→ BOOKED CALL

[/thankyou]   ✖ DEAD END
└── CTA: "Back to homepage" ──────────────────────→ [HOMEPAGE] ─→ ↺ LOOP
    └── ✖ no booking upsell, no case study, no "what happens next"

[PORTFOLIO FILTER PAGES] × 21   ✖ NO CONVERSION CTA ON ANY
├── 13 return ZERO projects → /ux-design · /ai-design · /saas-design · /brand-design
│   /tools-resources · /finance · /health-care · /hr-tech · /market-place · /web-3
│   /branding · /development · /support        → empty grid, no CTA, dead sticky → EXIT
└── 8 thin (555–1,383 words) → /e-commerce · /insurtech · /business-consulting
    /ed-tech · /mobile-app-design · /artificial-intelligence · /saas · /web-design
    └── show projects but carry NO conversion CTA → ↺ LOOP into case-study dead end

