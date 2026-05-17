# Directory Network Template — Global City Guide System

> Global network of AI-powered city directory guides — built on static HTML, deployed on Cloudflare Pages, automated with N8N.

---

## Overview

This repository is the **master template** for a growing network of city-guide directory websites. Each directory targets a specific city and niche (coffee shops, restaurants, coworking, nightlife, etc.), following the naming convention:

```
{city}.{domain}
```

Examples:
- **Dubai Coffee Guide** → [https://dubai.fond.coffee](https://dubai.fond.coffee) *(live)*
- **Curitiba Coffee** → curitiba.ama.cafe *(planned)*
- **New York Coffee** → newyork.fond.coffee *(planned)*

Each listing (café, business) gets its own sub-subdomain:
```
{slug}.dxb.fond.coffee   (e.g. nodgcafe.dxb.fond.coffee)
```

---

## Stack

| Layer | Technology |
|---|---|
| Frontend | HTML5 + CSS3 + Vanilla JS (static) |
| Hosting | Cloudflare Pages (free tier) |
| DNS | Cloudflare DNS (wildcard subdomains) |
| Data | `cafes-data.js` / `businesses-data.js` (JSON static DB) |
| Places Data | Google Places API (ratings, photos, hours) |
| Automation | N8N (scrape → content gen → deploy pipeline) |
| AI Content | OpenAI GPT-4 / TechSites.ai |
| Payments | Stripe (premium listings) |
| Blog SEO | SeoContent.ai |
| Indexing | IndexNow + Google Search Console |

---

## Project Structure

```
directory-network-template/
├── index.html               # Main directory listing page
├── listing.html             # Individual business page template
├── blog/
│   └── index.html           # Blog listing page
├── assets/
│   ├── css/
│   │   └── style.css
│   ├── js/
│   │   ├── main.js
│   │   ├── cafes-data.js    # Static JSON database
│   │   └── config.js        # City-specific configuration
│   └── images/
├── sitemap.xml
├── robots.txt
├── docs/
│   ├── ARCHITECTURE.md
│   ├── MONETIZATION.md
│   ├── LAUNCH-CHECKLIST.md
│   └── DOMAINS.md
└── SPRINT-LOG.md
```

---

## Naming Convention

```
{cidade}.{dominio}
```

| City | Domain | Status |
|---|---|---|
| Dubai | dubai.fond.coffee | Live |
| Curitiba | curitiba.cwb.site | Planned |
| Curitiba (café) | curitiba.ama.cafe | Planned |
| New York | newyork.fond.coffee | Planned |

Per-listing subdomain pattern:
```
{business-slug}.{city-code}.{root-domain}
# e.g.: nomadfuel.dxb.fond.coffee
```

---

## How to Clone & Adapt for a New City

1. **Clone this template:**
   ```bash
   git clone https://github.com/reynaldodallin/directory-network-template.git my-city-directory
   cd my-city-directory
   ```

2. **Edit `assets/js/config.js`** with city-specific data:
   ```js
   const CONFIG = {
     city: "Curitiba",
     cityCode: "cwb",
     domain: "curitiba.cwb.site",
     googlePlacesApiKey: "YOUR_KEY",
     stripePublicKey: "YOUR_STRIPE_KEY",
     niche: "coffee",
     currency: "BRL",
     language: "pt-BR"
   };
   ```

3. **Run N8N pipeline** to populate listings:
   - Trigger: `google-places-scrape` workflow
   - Output: updates `cafes-data.js` with real business data

4. **Deploy to Cloudflare Pages:**
   ```bash
   wrangler pages deploy . --project-name=curitiba-cwb-site
   ```

5. **Configure DNS** in Cloudflare:
   - Add CNAME: `curitiba.cwb.site` → `curitiba-cwb-site.pages.dev`
   - Add wildcard: `*.cwb.fond.coffee` → wildcard worker

6. **Submit sitemap** to Google Search Console and fire IndexNow.

7. **Create Stripe payment links** for premium listings.

---

## Monetization Model

| Tier | Price | Features |
|---|---|---|
| Free Listing | $0 | Basic card, name, address, rating |
| Premium Listing | $29–49/mo | Featured photo, CTA button, premium badge, top position |
| Sponsored Card | Custom | Pinned to top of all search results |
| Chatbot Agent | +$X/mo | AI agent trained on the business, 24/7 chat |
| City Ebook | $9–19 | AI-generated PDF city guide |
| Affiliates | Revenue share | Booking.com, OpenTable, Viator links |

See [docs/MONETIZATION.md](docs/MONETIZATION.md) for full Stripe configuration.

---

## Live Directories

| Directory | URL | Status |
|---|---|---|
| Dubai Coffee Guide | [https://dubai.fond.coffee](https://dubai.fond.coffee) | ✅ Live |

---

## Roadmap

| Sprint | Directory | Domain | Status |
|---|---|---|---|
| Sprint 1 | Dubai Coffee Guide | dubai.fond.coffee | ✅ Live |
| Sprint 2 | Global Hub | global.fond.coffee | Planned |
| Sprint 3 | Curitiba | cwb.site + ama.cafe | Planned |
| Sprint 4 | New York | newyork.fond.coffee | Planned |

---

## Powered By

- [TechSites.ai](https://techsites.ai) — AI-powered directory network infrastructure
- [SeoContent.ai](https://seocontent.ai) — Automated SEO blog content
- [PixelForge](https://github.com/reynaldodallin/pixelforge-cell) — Web build system

---

*Built by [@reynaldodallin](https://github.com/reynaldodallin)*
