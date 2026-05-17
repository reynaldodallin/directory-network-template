# Domain Inventory — Directory Network

Complete inventory of domains owned and their planned use across the directory network.

---

## Coffee & Café Directories

### `fond.coffee`
- **Purpose**: Global café directory hub
- **Structure**: city-based subdomains
- **Active**:
  - `dubai.fond.coffee` — Dubai Coffee Guide ✅ Live
  - `global.fond.coffee` — Global hub (planned)
- **Planned**:
  - `newyork.fond.coffee` — New York
  - `london.fond.coffee` — London
  - `tokyo.fond.coffee` — Tokyo
  - `paris.fond.coffee` — Paris
  - `sydney.fond.coffee` — Sydney
- **Per-listing**: `{slug}.dxb.fond.coffee` (Dubai), `{slug}.nyc.fond.coffee` (NYC)

### `ama.cafe`
- **Purpose**: Brazilian café directories (Portugal: "ama" = loves)
- **Structure**: city-based subdomains
- **Planned**:
  - `curitiba.ama.cafe` — Curitiba Coffee Guide
  - `saopaulo.ama.cafe` — São Paulo
  - `riodejaneiro.ama.cafe` — Rio de Janeiro
  - `florianopolis.ama.cafe` — Florianópolis

---

## Multi-Niche City Directories

### `cwb.site`
- **Purpose**: Curitiba multi-niche directory hub
- **Structure**: niche-based subdomains
- **Planned**:
  - `curitiba.cwb.site` — Main Curitiba directory
  - `cafes.cwb.site` — Curitiba cafés
  - `cowork.cwb.site` — Curitiba coworking spaces
  - `food.cwb.site` — Curitiba restaurants
  - `events.cwb.site` — Curitiba events

---

## SaaS & Tech Directories

### `saas.tips`
- **Purpose**: SaaS tools directory and reviews
- **Structure**: category-based subdomains
- **Planned**:
  - `ai.saas.tips` — AI tools directory
  - `marketing.saas.tips` — Marketing SaaS
  - `productivity.saas.tips` — Productivity tools

### `waas.host`
- **Purpose**: Website-as-a-Service platform directories
- **Platforms hosted**:
  - PixelForge (web build system)
  - SeoContent.ai (SEO automation)
  - TechSites.ai (directory network)
  - TechProspect (outreach automation)

---

## B2B & Expert Directories

### `hq.tips`
- **Purpose**: B2B headquarters / company directory
- **Structure**: industry-based subdomains
- **Planned**:
  - `tech.hq.tips` — Tech companies
  - `agency.hq.tips` — Digital agencies
  - `startup.hq.tips` — Startup directory

### `hho.expert`
- **Purpose**: Professional expert / freelancer directory
- **Niches**:
  - Medical professionals
  - Legal experts
  - Marketing consultants
  - Tech freelancers

---

## Review Sites

### `llc.reviews`
- **Purpose**: Company and LLC review directory
- **Structure**: US state-based and industry-based
- **Planned**:
  - `florida.llc.reviews`
  - `texas.llc.reviews`
  - `saas.llc.reviews`

---

## Yellow Pages Style

### `fond.directory`
- **Purpose**: Classic yellow pages style business directory
- **Structure**: city + category subdomains
- **Global scope**: English-speaking markets first
- **Planned**:
  - `dubai.fond.directory`
  - `miami.fond.directory`
  - `london.fond.directory`

---

## Domain Priority Matrix

| Domain | Category | Priority | Est. Launch |
|---|---|---|---|
| dubai.fond.coffee | Café directory | ✅ Live | Launched |
| curitiba.cwb.site | City multi-niche | High | Sprint 3 |
| curitiba.ama.cafe | Café directory | High | Sprint 3 |
| global.fond.coffee | Global hub | Medium | Sprint 2 |
| newyork.fond.coffee | Café directory | Medium | Sprint 4 |
| ai.saas.tips | SaaS directory | Low | TBD |
| fond.directory | Yellow pages | Low | TBD |

---

## DNS Management

All domains are managed through **Cloudflare DNS** for:
- Zero-TTL propagation on record changes
- Wildcard CNAME support for per-listing subdomains
- DDoS protection at the edge
- Free SSL for all subdomains
- Cloudflare Workers for dynamic routing

---

## Subdomain Routing Architecture

```
User visits: nomadfuel.dxb.fond.coffee
    ↓
Cloudflare DNS: *.dxb.fond.coffee → Worker
    ↓
Worker: extract slug "nomadfuel" from hostname
    ↓
Fetch listing data from cafes-data.js KV store
    ↓
Render listing page template
    ↓
Return HTML response
```
