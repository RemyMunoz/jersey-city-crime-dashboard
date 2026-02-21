# JC Crime Dashboard — Codex Project Brief
*Handoff document for continuing development in ChatGPT Codex*

---

## 🧠 Who You're Building For

**Geremy** — Jersey City Police Officer, North District, Badge #3458, JC FOP Lodge #4 member.  
He built this dashboard as a portfolio piece to pitch to other police organizations and real estate professionals. The goal is a B2B SaaS product for property managers, real estate agents, and municipal stakeholders who need crime/safety data visualized at the neighborhood level.

---

## 📁 Project Overview

**Name:** Jersey City Crime Dashboard 2024  
**Type:** Single-file HTML/CSS/JS web app (no build tools, no framework, no backend)  
**Status:** Working prototype — core features complete, ready for enhancement

---

## 🛠 Tech Stack

| Layer | Technology |
|---|---|
| Map | Mapbox GL JS v3.1.2 |
| Fonts | Google Fonts — Space Mono, DM Sans |
| Data | GeoJSON (baked directly into the HTML file) |
| Hosting | None yet — single `.html` file, opens in browser |
| Mapbox Token | `YOUR_MAPBOX_PUBLIC_TOKEN` |

---

## ✅ What's Already Built

### Map
- Dark basemap (Mapbox dark-v11)
- **Ward boundary polygons** — all 6 Jersey City wards (A–F) using official GeoJSON from `data.jerseycitynj.gov`
- **Police district boundary polygons** — all 4 JCPD districts (North, South, East, West) using official GeoJSON from `data.jerseycitynj.gov`
- **Precinct station markers** — custom SVG shield icons at exact geocoded coordinates, color-coded by district
- Interactive popups on hover for both wards and precincts
- Click-to-fly behavior from sidebar to map location

### Sidebar
- City-wide stats cards (total incidents, clearance rate, response time, YoY change)
- Ward list — clickable, flies map to ward boundary
- Precinct list — clickable, flies map to station
- Layer toggle controls (3 switches: Ward Boundaries, Police Districts, Precinct Stations)
- Legend (ward density + police district colors)

### Data
- **2024 JC Crime Stats** (manually sourced, FBI/NJSP data):
  - Ward A (Greenville/West Side): 312 incidents — High — top crime: Assault
  - Ward B (Bergen-Lafayette): 245 incidents — Medium-High — top crime: Robbery
  - Ward C (Heights/North): 198 incidents — Medium-High — top crime: Larceny
  - Ward D (Journal Square/West Bergen): 176 incidents — Medium — top crime: Burglary
  - Ward E (Downtown/Newport): 142 incidents — Lower-Medium — top crime: Theft
  - Ward F (Greenville/South): 118 incidents — Lower — top crime: Vandalism
  - **Total: 1,191 incidents | Clearance rate: 34% | Avg response: 6.2 min**

- **2025 Council Members** (updated after November 2025 elections):
  - Ward A: Denise Ridley (re-elected)
  - Ward B: Joel A. Brooks (NEW — replaced Mira Prinz-Arey)
  - Ward C: Richard Boggiano (re-elected)
  - Ward D: Jake Ephros (NEW — replaced Yousef Saleh)
  - Ward E: Eleana Little (NEW — replaced James Solomon, who became Mayor)
  - Ward F: Frank E. Gilmore (re-elected)
  - *Note: James Solomon won the December 2025 mayoral runoff, defeating Jim McGreevey*

- **JCPD Precinct Stations:**
  | District | Address | Phone | Coords | Color |
  |---|---|---|---|---|
  | North | 282 Central Ave, JC 07307 | (201) 547-5350 | 40.7421, -74.0515 | #4CC9F0 (cyan) |
  | South | 191 Bergen Ave, JC 07305 | (201) 547-5456 | 40.6960, -74.0736 | #F72585 (pink) |
  | East | 207 7th Street, JC 07302 | (201) 547-5408 | 40.7217, -74.0476 | #7B61FF (purple) |
  | West | 576 Communipaw Ave, JC 07304 | (201) 547-5450 | 40.7129, -74.0737 | #FF9F1C (orange) |

---

## 🎨 Design System

```css
--bg: #0a0c10
--panel: #111318
--border: #1e2229
--accent: #e63946 (red)
--blue: #457b9d
--text: #e8eaed
--muted: #6b7280

/* District colors */
North: #4CC9F0
South: #F72585
East: #7B61FF
West: #FF9F1C

/* Ward density colors (high → low) */
High: #e63946
Med-High: #e9c46a
Medium: #f4a261
Lower-Med: #52b788
Lower: #1a472a (dot: #74c69d)
```

Fonts: `Space Mono` (monospace/labels/stats), `DM Sans` (body text)

---

## 📐 Layout

```
┌─────────────────────────────────────────────────────┐
│  SIDEBAR (300px fixed)  │  MAP (flex: 1, full height)│
│  ─ Header               │                             │
│  ─ City Stats           │   Mapbox dark map           │
│  ─ Ward List            │   + ward polygons           │
│  ─ Precinct List        │   + district polygons       │
│  ─ Layer Toggles        │   + precinct markers        │
│  ─ Legend               │   + popups on hover         │
└─────────────────────────────────────────────────────┘
```

---

## 🗂 GeoJSON Data Sources

Both datasets are from Jersey City's official open data portal:

- **Ward boundaries:** `https://data.jerseycitynj.gov/explore/dataset/wards/`
- **Police districts:** `https://data.jerseycitynj.gov/explore/dataset/police-districts/`

Both GeoJSON files are **baked directly into the HTML file** as JS variables:
- `wardsGeoJSON` — ward boundaries
- `districtGeoJSON` — police district boundaries (official polygons from city data)

---

## 🚧 Known Issues / Things to Fix

1. **District polygon replacement was mid-save** — the official district GeoJSON from the city portal was being inserted when the project was handed off. Verify that all 4 district polygons (East, West, North, South) are using the official coordinates, not the old hand-drawn approximations. The official raw GeoJSON is available at: `https://data.jerseycitynj.gov/api/explore/v2.1/catalog/datasets/police-districts/exports/geojson`

2. **No mobile responsiveness** — sidebar collapses on small screens, needs a hamburger menu or bottom sheet

3. **Crime data is static/hardcoded** — no live API connection yet

---

## 🔜 Planned Features (Next Steps)

- [ ] Real crime data feed (JCPD CompStat or NJ state data)
- [ ] Time filter (view crime by month/quarter)
- [ ] Crime type filter (assault, burglary, theft, etc.)
- [ ] Street-level incident dots on map
- [ ] Export to PDF / shareable link
- [ ] Mobile responsive layout
- [ ] Authentication layer (for paid B2B version)
- [ ] Multi-city support (pitch to other NJ departments)

---

## 💼 Business Context

- **Target buyers:** Real estate agents, property managers, municipal stakeholders, other police departments, FOP lodges
- **Revenue model:** B2B SaaS — ~$75/month per client, custom builds for orgs
- **Portfolio piece:** Built to pitch the JC FOP Lodge #4 website redesign at $1,000 + $75/month maintenance
- **Anonymity:** Planning to sell through an LLC with privacy-registered domain

---

## 💡 How to Start a Codex Session

Paste this into your first Codex message:

> "I'm continuing work on a Jersey City crime dashboard. Here is the full project brief: [paste this document]. Here is the current index.html file: [paste file contents]. I want to [describe next task]."

The entire project lives in one `index.html` file — just paste its contents alongside this brief and Codex will have full context.

---

*Brief generated: February 2026 | Project started: Late 2025*
