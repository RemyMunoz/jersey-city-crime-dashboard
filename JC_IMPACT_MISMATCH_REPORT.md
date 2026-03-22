# JC IMPACT Compliance Audit (Phase 1)

Source of truth used for this audit:
- `/Users/remyclaw/Desktop/JCIMPACT Tracking Categories.docx`
- `/Users/remyclaw/Desktop/JCIMPACT Weekly Jan Feb 2026.xlsx`

Audit scope:
- `dashboard.html`
- `district.html`
- `ward.html`
- `data.json`

## Mismatch Matrix

| Current website label | Correct JC IMPACT label | Where it appears | Data source | Status |
|---|---|---|---|---|
| `Criminal Mischief` in major category lists/charts | Remove from **7 Major Impact Crime Categories** | `dashboard.html` (major category order, chart options, trend bundles, KPI and mobile summary), `data.json` (`crime.Criminal Mischief`) | Mixed: Excel export + hardcoded trend/mock blocks | **Incorrect** |
| `Burglary — auto (theft from auto)` under burglary grouping | `Theft From Auto` (separate; not burglary) | `dashboard.html` district rows (`burglaryAutoTheftFromAuto`), `district.html` monthly rows | Excel export label mapping + UI hardcoded labels | **Incorrect** |
| `Assault (total)` / `Assault Total` shown as major line | `Aggravated Assault` as tracked major category | `dashboard.html` citywide/district rows and trend mappings, `data.json` (`assaultTotal`) | Excel export + UI mappings | **Incorrect** |
| `Rape / Sex Offenses` or `Sex Offenses` | `Sexual Assault` (forcible rape definition) | `dashboard.html` row labels/charts, `district.html`, `data.json` (`sexOffenses`, `crime["Sex Offenses"]`) | Excel export + UI hardcoded labels | **Incorrect** |
| `Stolen Vehicles` | `Motor Vehicle Theft` | `dashboard.html` chart options/KPIs/mobile summary, `data.json` labels | Excel export + UI hardcoded labels | **Incorrect** |
| `Robbery` (single line without explicit incidents/victims split in major table) | `Robbery Incidents` and `Robbery Victims` separated | `dashboard.html` compstat table has incidents only; no victims row | Excel export has incidents-style totals; victims not wired | **Missing (victims)** |
| `Aggravated Assault` (single line without explicit incidents/victims split) | `Aggravated Assault Incidents` and `Aggravated Assault Victims` separated | `dashboard.html` compstat table has incidents only; no victims row | Excel export has incidents-style totals; victims not wired | **Missing (victims)** |
| Legacy source cards (`FBI`, `NJSP UCR`, `JC Open Data`) used as primary dashboard source framing | Excel workbook as sole operational source for IMPACT framework | `dashboard.html` Data Sources panel | Hardcoded content | **Incorrect** |
| Static 2024/2025 trend bundles and static mobile stats | Excel-driven values only, no invented/fallback counts | `dashboard.html` (`crimeStats2024`, `crimeStats2025`, static mobile crime rows) | Hardcoded | **Incorrect** |

## Required Sections Compliance (1-10)

| JC IMPACT section | Current website state | Where | Data source | Status |
|---|---|---|---|---|
| 1. 7 Major Impact Crime Categories | Present but includes prohibited/legacy naming (`Criminal Mischief`, `Assault Total`, `Sex Offenses`, `Stolen Vehicles`) | `dashboard.html`, `data.json`, `district.html` | Excel export + hardcoded mappings | **Incorrect** |
| 2. Supplemental Crime Stats | Partially present (`Theft From Auto`, `Theft of Auto Parts`, shootings, stabbings, drug arrests, shoplifting, bias) but not organized as JC IMPACT section | `dashboard.html`, `data.json` | Excel export | **Partial / incorrect grouping** |
| 3. Arrests & Gun Offenses Unit | Partially present (`Guns Recovered`, `Total arrests`, firearm arrest rows) but not labeled as GOU framework | `dashboard.html`, `data.json` | Excel export | **Partial / incorrect grouping** |
| 4. Traffic & Vision Zero | No explicit section with `MVA Total`, `Pedestrians Struck` | Not rendered | Not wired | **Missing** |
| 5. Missing Persons | Data keys exist in citywide monthly rows, but no dedicated IMPACT section | `data.json` has `missingPersonsAdult/Juvenile`; UI lacks IMPACT grouping | Excel export | **Partial / missing section** |
| 6. Communications / 911 | No section or metrics rendered | Not rendered | Not wired | **Missing** |
| 7. Internal Affairs | No section or metrics rendered | Not rendered | Not wired | **Missing** |
| 8. Workforce & Wellness | No section or metrics rendered | Not rendered | Not wired | **Missing** |
| 9. External Coordination | No section or metrics rendered | Not rendered | Not wired | **Missing** |
| 10. Community Engagement | No section or metrics rendered | Not rendered | Not wired | **Missing** |

## High-priority flags requested

- `Criminal Mischief` is still used in major category UX and trend views -> **must be removed from major categories**.
- `Burglary into auto` is still represented under burglary labels in district tables -> **must be moved/renamed to Theft From Auto**.
- `Assault Total` appears in data mappings and rows -> **must be replaced in public major taxonomy by Aggravated Assault**.
- `Sex Offenses` appears in public labels -> **must be renamed Sexual Assault (forcible rape definition)**.
- `Stolen Vehicles` appears in public labels -> **must be renamed Motor Vehicle Theft**.
- Incidents vs victims split for `Robbery` and `Aggravated Assault` is incomplete -> **victim lines missing in UI; needs explicit split with Data Pending where unavailable**.
