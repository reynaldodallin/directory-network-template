# Sprint Log — Directory Network

Sprint tracking log following the PixelForge project organization standard.
Each sprint = one shipped directory or major milestone.

---

## Sprint 1 — Dubai Coffee Guide ✅ CONCLUÍDO

**Domain**: [dubai.fond.coffee](https://dubai.fond.coffee)
**Sprint Duration**: ~2 weeks
**Status**: Live & indexed

### Deliverables
- [x] 40+ café listings across 8 Dubai neighborhoods
- [x] 8 neighborhoods covered: DIFC, Downtown, Marina, JBR, Al Quoz, Business Bay, Palm Jumeirah, JLT
- [x] Individual listing pages via subdomain routing (`{slug}.dxb.fond.coffee`)
- [x] Premium listing infrastructure (Stripe integration)
- [x] Blog section with SEO articles
- [x] Mobile navigation v3.5 (final fix — hamburger menu, filters, search)
- [x] Google Places API integration for real ratings and photos
- [x] Schema.org JSON-LD (LocalBusiness) on all listing pages
- [x] sitemap.xml auto-generated
- [x] IndexNow submission
- [x] Google Search Console setup

### Metrics (Launch Week)
- Listings: 40+
- Neighborhoods: 8
- Blog articles: 3
- Google index status: Submitted

### Technical Notes
- Stack: HTML5 + CSS3 + Vanilla JS, Cloudflare Pages
- Data: `cafes-data.js` (static JSON, ~40 entries)
- Nav fix: v3.1 → v3.2 → v3.3 → v3.4 → v3.5 (mobile hamburger + filter overlay)
- DNS: `dubai.fond.coffee` CNAME → Cloudflare Pages, wildcard `*.dxb.fond.coffee` → Worker

---

## Sprint 2 — Global Hub 🔜 PLANEJADO

**Domain**: global.fond.coffee
**Status**: Planned
**Goal**: Central hub linking all city directories in the fond.coffee network

### Planned Deliverables
- [ ] Landing page: "The World's Best Coffee, City by City"
- [ ] Directory of all active city guides (Dubai → more)
- [ ] "Coming soon" previews for planned cities
- [ ] Newsletter signup (Beehiiv or ConvertKit)
- [ ] SEO: "best coffee cities in the world", "coffee travel guide"
- [ ] Link hub for all fond.coffee subdomains
- [ ] Affiliate integration: Booking.com, Viator, travel gear

### Target Metrics
- Cities linked: 5+ (3 live, 2 coming soon)
- Email subscribers: 100+ in first month

---

## Sprint 3 — Curitiba Directories 🔜 PLANEJADO

**Domains**: curitiba.cwb.site + curitiba.ama.cafe
**Status**: Planned
**Goal**: First Brazilian city directory — pilot for Portuguese-language market

### Planned Deliverables
- [ ] curitiba.cwb.site — Multi-niche Curitiba guide (cafés + coworking + events)
- [ ] curitiba.ama.cafe — Dedicated Curitiba coffee guide (Portuguese)
- [ ] 50+ café listings scraped via Google Places API
- [ ] Bairros: Batel, Água Verde, Rebouças, Centro, Bigorrilho, Cabral, Hugo Lange, Seminário
- [ ] Portuguese UI localization
- [ ] BRL currency support for Stripe (premium R$149–249/mês)
- [ ] Local SEO: "café em Curitiba", "melhores cafés de Curitiba"
- [ ] Blog: "Guia de Cafés de Curitiba [Ano]"
- [ ] WhatsApp integration for premium listings (Brazil-specific)

### Target Metrics
- Listings: 50+
- Bairros: 8+
- Premium conversions target: 3 in first month

---

## Sprint 4 — New York Coffee Guide 🔜 PLANEJADO

**Domain**: newyork.fond.coffee
**Status**: Planned
**Goal**: Flagship English-language market — highest competition, highest revenue potential

### Planned Deliverables
- [ ] 100+ café listings
- [ ] Neighborhoods: Manhattan (SoHo, Williamsburg, East Village, Midtown, UWS, UES), Brooklyn (Park Slope, DUMBO, Greenpoint), Queens (Astoria, Long Island City)
- [ ] NYC-specific features: nearest subway station, outdoor seating flag
- [ ] Premium listing at $49/month (higher than Dubai due to market)
- [ ] Sponsored card at $299/month
- [ ] "Best coffee near [landmark]" SEO cluster
- [ ] OpenTable / Resy affiliate integration
- [ ] Print ebook: "The New Yorker's Coffee Guide 2025" — $19

### Target Metrics
- Listings: 100+
- Neighborhoods: 10+
- Premium conversions target: 10 in first 3 months
- Monthly revenue target: $1,000+ by month 3

---

## Backlog

| Sprint | Directory | Domain | Priority |
|---|---|---|---|
| S5 | London Coffee | london.fond.coffee | Medium |
| S6 | São Paulo | saopaulo.ama.cafe | Medium |
| S7 | Tokyo Coffee | tokyo.fond.coffee | Low |
| S8 | Paris Coffee | paris.fond.coffee | Low |
| S9 | Miami | miami.fond.directory | Low |
| S10 | SaaS Tools | ai.saas.tips | Low |

---

## Velocity Reference

| Sprint | Duration | Listings Shipped | Revenue D+30 |
|---|---|---|---|
| S1 (Dubai) | 2 weeks | 40 | TBD |
| S2 (Global Hub) | 1 week | N/A | TBD |
| S3 (Curitiba) | 2 weeks | 50 (target) | TBD |
| S4 (New York) | 3 weeks | 100 (target) | TBD |

---

*Log maintained by [@reynaldodallin](https://github.com/reynaldodallin) — follows [PixelForge](https://github.com/reynaldodallin/pixelforge-cell) sprint conventions*
