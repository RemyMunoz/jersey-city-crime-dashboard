# YTD right-panel preview (Excel → `ytd-breakdown.json`)

## Data flow

1. Source: **Crime Breakdown** sheet in `JCIMPACT Weekly Jan Feb 2026.xlsx` (7 Impact categories × City-Wide + N/E/S/W districts).
2. Export: `python3 scripts/export_ytd_breakdown.py "/path/to/workbook.xlsx"`
3. Output: **`ytd-breakdown.json`** at repo root (committed for the live site).
4. Dashboard loads it with `fetch('ytd-breakdown.json')` alongside `data.json`.

## By YTD (citywide)

- One card per category from Excel **City-Wide** column **2026 YTD**.
- **Total Crime Count (YTD)** = sum of those citywide 2026 YTD values (7 categories).
- **% vs 2025** = \((2026 - 2025) / 2025 × 100\) per category (same as spreadsheet logic).

## By District

- Rows = categories (same 7 as Excel sections).
- Columns = **North · East · South · West** (fixed order).
- **Cell fill**: `rgba(201, 168, 76, α)` where **α** is **0.12–1.0** from:

  \[
  \alpha = 0.12 + \frac{v - v_{\min}}{v_{\max} - v_{\min}} \times 0.88
  \]

  - \(v\) = district **2026 YTD** count for that cell  
  - \(v_{\min}, v_{\max}\) = **min / max over all 28 district cells** (7×4) in the loaded file — **recomputed whenever JSON changes**, no fixed thresholds.

- If \(v_{\max} = v_{\min}\), all cells use α = **0.55** (mid) so the grid is still readable.

## Sample numbers (current export)

| Category        | Citywide 2026 YTD |
|----------------|------------------:|
| Assault        | 349 |
| Stolen Vehicles| 104 |
| Burglary       | 122 |
| Homicide       | 0 |
| Theft          | 407 |
| Sex Offenses   | 31 |
| Robbery        | 44 |
| **Sum (header)** | **1,057** |

District min/max for opacity (from same export): **0** (homicide rows) → **134** (e.g. South assault), so low counts appear pale; high counts saturated.

---

*This file is documentation only; the live UI is in `dashboard.html` → `#rightStatsCards`.*
