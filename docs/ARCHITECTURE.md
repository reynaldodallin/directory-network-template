# Technical Architecture — Directory Network Template

## Overview

Each directory site in the network is a **fully static website** hosted on Cloudflare Pages at zero infrastructure cost, with dynamic data sourced from Google Places API and stored as JavaScript modules.

---

## Hosting: Cloudflare Pages

- **Cost**: Free tier (unlimited bandwidth, unlimited requests)
- **Build**: No build step — pure static HTML/CSS/JS
- **Deploy**: `wrangler pages deploy` or GitHub integration (auto-deploy on push)
- **CDN**: Global edge network, automatic HTTPS

```
GitHub repo → Cloudflare Pages → Live URL
```

---

## DNS Structure

### Per-city subdomain
```
{city}.{root-domain}
# e.g.: dubai.fond.coffee
```

### Per-listing sub-subdomain
```
{business-slug}.{city-code}.{root-domain}
# e.g.: nodgcafe.dxb.fond.coffee
```

### Cloudflare DNS Configuration
```
Type    Name                    Target
CNAME   dubai.fond.coffee       dubai-fond-coffee.pages.dev
CNAME   *.dxb.fond.coffee       dubai-listings-worker.workers.dev
```

The wildcard subdomain points to a **Cloudflare Worker** that dynamically serves individual listing pages by reading the business slug from the hostname.

---

## Data Layer: Static JSON Database

Each city directory uses a JavaScript data module as its "database":

```js
// assets/js/cafes-data.js
const CAFES_DATA = [
  {
    id: "nomadfuel-dxb",
    slug: "nomadfuel",
    name: "Nomad Fuel Café",
    neighborhood: "DIFC",
    rating: 4.7,
    reviews: 312,
    address: "Gate Village 3, DIFC, Dubai",
    phone: "+971 4 XXX XXXX",
    website: "https://nomadfuel.com",
    instagram: "@nomadfueldxb",
    hours: { mon: "7:00-22:00", /* ... */ },
    photos: ["photo1.jpg", "photo2.jpg"],
    tags: ["specialty coffee", "coworking", "wifi"],
    isPremium: false,
    isSponsored: false,
    googlePlaceId: "ChIJ..."
  }
  // ...
];
```

This eliminates the need for a backend database entirely.

---

## Google Places API Integration

Used to **bootstrap and refresh** listing data:

1. **Search**: `Places API → Text Search` to find businesses in city
2. **Details**: `Places API → Place Details` for ratings, photos, hours, phone
3. **Photos**: `Places API → Photo Reference` for business images

The N8N workflow handles this automatically on a scheduled basis.

---

## N8N Automation Pipeline

### Workflow: `google-places-scrape`
```
Trigger (manual/cron)
  → Google Places Search (city + niche keywords)
  → For each result: Places Details API
  → OpenAI: Generate SEO description
  → Format as JS data object
  → Append to cafes-data.js
  → Git commit + push → Cloudflare auto-deploy
```

### Workflow: `premium-listing-onboard`
```
Stripe webhook (payment_intent.succeeded)
  → Update business record isPremium = true
  → Send confirmation email
  → Trigger deploy
```

### Workflow: `blog-content-generator`
```
Trigger (weekly)
  → SeoContent.ai API: generate article
  → Save to /blog/{slug}.html
  → Git commit + push
  → IndexNow ping
```

---

## Payment: Stripe

- **Premium Listing**: Stripe Payment Link (monthly subscription)
- **Sponsored Card**: Stripe Payment Link (monthly)
- **Ebook**: Stripe Payment Link (one-time)
- **Chatbot Agent**: Stripe subscription with metadata `{businessId}`

Webhooks are processed by an N8N workflow that updates the static data file and redeploys.

---

## SEO & Indexing

| Tool | Purpose |
|---|---|
| Google Search Console | Sitemap submission, index monitoring |
| IndexNow | Instant ping on new/updated pages |
| SeoContent.ai | Automated blog article generation |
| Schema.org JSON-LD | LocalBusiness structured data on each listing |
| sitemap.xml | Auto-generated, includes all listing URLs |

---

## City Configuration: `config.js`

```js
const CONFIG = {
  city: "Dubai",
  cityCode: "dxb",
  country: "UAE",
  domain: "dubai.fond.coffee",
  listingSubdomain: "{slug}.dxb.fond.coffee",
  googlePlacesApiKey: process.env.GOOGLE_PLACES_KEY,
  stripePublicKey: process.env.STRIPE_PUBLIC_KEY,
  niche: "coffee",
  currency: "AED",
  language: "en",
  neighborhoods: ["DIFC", "Downtown", "JBR", "Marina", "Al Quoz"],
  premiumPrice: 49,        // USD/month
  sponsoredPrice: 199,     // USD/month
  ebookPrice: 9,           // USD one-time
  chatbotPrice: 99         // USD/month
};
```

---

## Stack Summary

```
Static HTML/CSS/JS
    ↓
Cloudflare Pages (hosting + CDN)
    ↓
Cloudflare Workers (wildcard subdomain routing)
    ↓
cafes-data.js (static JSON DB)
    ↑
N8N (automation: scrape + content + deploy)
    ↑
Google Places API + OpenAI + SeoContent.ai
    ↑
Stripe (payment webhooks → N8N → data update)
```
