# Monetization Model — Directory Network

## Revenue Tiers

### 1. Free Listing (Default)
- Basic card in the directory
- Business name, address, rating, Google Maps link
- Photo from Google Places
- No cost, no action required from business owner

**Goal**: Build directory density quickly. Free listings create value for users and legitimacy for the directory.

---

### 2. Premium Listing — $29–49/month

**What the business gets:**
- Featured hero photo (custom upload)
- Call-to-action button (Book, Order, Reserve, Visit)
- Premium badge displayed on card
- Priority position: appears at the top of neighborhood/category results
- Extended business description (500+ words, SEO-optimized)
- Direct link to business website
- Instagram / WhatsApp / social links
- Monthly analytics report (views, clicks)

**Stripe Configuration:**
```
Product: Premium Listing - [City] Directory
Price: $49/month (or local equivalent)
Interval: monthly
Metadata: { businessId: "slug", city: "dubai", directory: "fond.coffee" }
```

Payment Link URL format:
```
https://buy.stripe.com/{link-id}?prefilled_promo_code=UPGRADE49
```

---

### 3. Sponsored Card — Custom Pricing ($149–299/month)

- Business card appears **pinned at the top** of all search results
- Labeled "Sponsored" (FTC compliant)
- Appears on homepage, category pages, and neighborhood pages
- Custom card design with logo + brand color accent
- Ideal for chains, franchises, new openings

---

### 4. Chatbot Agent — +$99/month add-on

- AI agent trained on everything about the business:
  - Menu, prices, hours, location, specialties
  - FAQs (parking, reservations, dietary restrictions)
  - Promotions and loyalty programs
- Embedded as a chat widget on the listing page
- Available 24/7, reduces calls to the business
- Monthly training update included

**Tech**: OpenAI Assistants API with custom knowledge base per business.

---

### 5. City Ebook — $9–19 (one-time)

- "The Ultimate [City] Coffee Guide [Year]"
- AI-generated PDF: 30–50 pages
- Includes: top 20 cafés, neighborhood map, insider tips, photographic guide
- Delivered via Stripe + email automation
- Also sold on: Gumroad, Amazon KDP (passive income)

**Generation**: Automated with SeoContent.ai + custom PDF template.

---

### 6. Affiliate Revenue

| Partner | Niche | Commission |
|---|---|---|
| Booking.com | Hotels near cafés | 25–40% |
| OpenTable / Resy | Restaurant reservations | Per booking |
| Viator / GetYourGuide | City tours | 8% |
| Amazon | Coffee gear, books | 3–8% |
| Local delivery apps | Food/coffee delivery | Per order |

Affiliate links are embedded naturally in:
- Individual listing pages ("Book a table")
- Blog articles ("Best coffee near [landmark]")
- City ebook ("Where to stay near the coffee scene")

---

## Stripe Setup Guide

### Step 1: Create Products
```bash
# Premium Listing
stripe products create   --name="Premium Listing - Dubai Coffee Guide"   --description="Featured placement + CTA + premium badge"

# Create price
stripe prices create   --product=prod_XXXX   --unit-amount=4900   --currency=usd   --recurring[interval]=month
```

### Step 2: Create Payment Links
- Go to Stripe Dashboard → Payment Links
- Select the product/price
- Add custom fields: Business Name, Slug
- Set success URL: `https://dubai.fond.coffee/premium-success?session_id={CHECKOUT_SESSION_ID}`

### Step 3: Configure N8N Webhook
```
Stripe Webhook → N8N Trigger
Event: payment_intent.succeeded
Action: Update cafes-data.js → isPremium: true → Deploy
```

---

## Revenue Projections per Directory

| Source | Low | Mid | High |
|---|---|---|---|
| Premium Listings (10 × $49) | $490/mo | - | - |
| Premium Listings (30 × $49) | - | $1,470/mo | - |
| Premium Listings (50 × $49) | - | - | $2,450/mo |
| Sponsored Cards (2 × $199) | $398/mo | $398/mo | $597/mo |
| Chatbot Agents (5 × $99) | $495/mo | $495/mo | $990/mo |
| Ebooks | $90/mo | $270/mo | $900/mo |
| Affiliates | $50/mo | $200/mo | $500/mo |
| **Total** | **~$1,523/mo** | **~$2,833/mo** | **~$5,437/mo** |

Multiply across 5–10 active directories for network-level revenue.

---

## Outreach & Conversion

Automated via **TechProspect** (N8N workflow):

1. Scrape business contact info (website, Instagram, Google)
2. Personalized cold email: "Your business is already listed on [Directory] — upgrade to premium"
3. Follow-up sequence: Day 3, Day 7, Day 14
4. WhatsApp message (where appropriate)

Conversion target: 5–10% of total listings → premium.
