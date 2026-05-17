# Launch Checklist — New Directory

Use this checklist every time you launch a new city directory. Duplicate this file and fill in the city-specific details.

---

## Pre-Launch Setup

### Domain & Branding
- [ ] Choose premium domain from [docs/DOMAINS.md](DOMAINS.md)
- [ ] Register/confirm domain is pointing to Cloudflare nameservers
- [ ] Define city code (e.g., `dxb` for Dubai, `cwb` for Curitiba, `nyc` for New York)
- [ ] Design city-specific color palette and hero image
- [ ] Write city tagline: "The best [niche] in [city], curated for you"

---

## Repository & Codebase

- [ ] Clone template-master-directory from GitHub:
  ```bash
  git clone https://github.com/reynaldodallin/directory-network-template.git {city}-directory
  cd {city}-directory
  git remote set-url origin https://github.com/reynaldodallin/{city}-directory.git
  git push -u origin main
  ```
- [ ] Adapt `assets/js/config.js` with city-specific data:
  - City name, city code, country
  - Root domain and listing subdomain pattern
  - Google Places API key
  - Stripe public key
  - Neighborhoods/districts list
  - Niche (coffee, restaurants, coworking, etc.)
  - Currency and language
  - Pricing: premium, sponsored, ebook, chatbot
- [ ] Update `index.html` meta tags (title, description, og:image)
- [ ] Update `sitemap.xml` base URL

---

## Data Population

- [ ] Run N8N workflow: `google-places-scrape`
  - Input: city name + niche keywords
  - Output: populated `cafes-data.js` (target: 30–100 listings minimum)
- [ ] Review scraped data for quality issues
- [ ] Run N8N workflow: `generate-listing-descriptions` (OpenAI)
- [ ] Add 3–5 manually curated "Editor's Pick" listings
- [ ] Verify all neighborhood tags are correct

---

## Cloudflare Configuration

- [ ] Create new Cloudflare Pages project:
  ```bash
  wrangler pages project create {city}-{domain-slug}
  ```
- [ ] Deploy initial version:
  ```bash
  wrangler pages deploy . --project-name={city}-{domain-slug}
  ```
- [ ] Add custom domain in Cloudflare Pages settings:
  - Primary: `{city}.{domain}`
  - Verify DNS propagation
- [ ] Configure DNS in Cloudflare dashboard:
  - CNAME: `{city}.{domain}` → `{project}.pages.dev`
  - Wildcard CNAME: `*.{citycode}.{domain}` → Cloudflare Worker
- [ ] Enable HTTPS (automatic via Cloudflare)
- [ ] Set up Cloudflare Worker for wildcard subdomain routing (per-listing pages)
- [ ] Test 3–5 individual listing subdomains

---

## SEO & Indexing

- [ ] Submit `sitemap.xml` to Google Search Console:
  - Add property: `https://{city}.{domain}`
  - Submit sitemap URL
- [ ] Verify Search Console ownership (HTML tag or DNS)
- [ ] Fire IndexNow:
  ```bash
  curl -X POST "https://api.indexnow.org/indexnow"     -H "Content-Type: application/json"     -d '{"host":"{city}.{domain}","key":"YOUR_INDEXNOW_KEY","urlList":["https://{city}.{domain}/","https://{city}.{domain}/sitemap.xml"]}'
  ```
- [ ] Install Schema.org `LocalBusiness` JSON-LD on listing pages
- [ ] Confirm robots.txt allows all crawlers

---

## Monetization Setup

- [ ] Create Stripe products (Premium, Sponsored, Ebook, Chatbot)
- [ ] Create Stripe Payment Links for each package
- [ ] Update `config.js` with payment link URLs
- [ ] Configure N8N webhook: Stripe → `premium-listing-onboard` workflow
- [ ] Test end-to-end: payment → webhook → data update → redeploy
- [ ] Create Gumroad product for city ebook (if ready)

---

## Content

- [ ] Generate first 3 blog articles via SeoContent.ai:
  - "Best [niche] in [city] [year]"
  - "Top [niche] in [neighborhood 1]"
  - "Hidden gems: [niche] in [city]"
- [ ] Publish blog articles, commit to repo
- [ ] Create city ebook (AI-generated PDF, 30–50 pages)
- [ ] Write About page with city context and directory mission

---

## Launch & Outreach

- [ ] Final QA: test all filters, search, mobile, page speed
- [ ] Run Lighthouse audit (target: >90 performance, >90 SEO)
- [ ] Announce on social media (Twitter/X, Instagram, LinkedIn)
- [ ] Submit to local Facebook groups / Reddit communities
- [ ] Configure TechProspect outreach campaign:
  - Import business contact list from `cafes-data.js`
  - Activate cold email sequence for premium conversion
  - Set follow-up schedule: Day 0, Day 3, Day 7, Day 14
- [ ] Track conversions in Stripe dashboard

---

## Post-Launch (Week 2+)

- [ ] Monitor Google Search Console for indexing progress
- [ ] Review Cloudflare Analytics (traffic, top pages)
- [ ] First premium conversion follow-up calls
- [ ] Add 10–20 new listings based on user feedback
- [ ] Generate and publish 2 new blog articles
- [ ] A/B test premium listing CTA copy
