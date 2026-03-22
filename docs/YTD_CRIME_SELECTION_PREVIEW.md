# Preview: Crime type (left) → YTD panel (right) + district map opacity

## Behavior

### Left sidebar — **Crime Type** (existing radios)
Maps to **`ytd-breakdown.json`** categories:

| Radio value        | YTD category `id`   | Notes |
|--------------------|---------------------|--------|
| All Major Categories | *(all)*         | Citywide sum + existing **By YTD / By District** toggle; map opacity = **sum of all 7 categories** per district |
| Homicide           | `homicide`          | |
| Sex Offenses       | `sex-offenses`      | |
| Robbery            | `robbery`           | |
| Aggravated Assault | `assault`           | Excel **Assault** block (total assault category) |
| Burglary           | `burglary`          | |
| Theft              | `theft`             | |
| Motor Vehicle Theft | `stolen-vehicles` | |

### Right column — when **one** crime type is selected
1. **2026 YTD (citywide)** — single headline count + **% vs 2025** (from JSON).
2. **By district** — North / East / South / West with **2026 YTD** each (same row order as map legend).
3. Short note: data source file name from `ytd-breakdown.json` meta.

The **By YTD / By District** toggle is **only** for **All Major Categories** (unchanged).

### Map — **Police districts** fill (`districts-fill`)
- **Lower** district count for the current selection → **more transparent** fill (same district hue, lower `fill-opacity`).
- **Higher** count → **more opaque**.
- Opacity is **linear** between **min** and **max** of the **four** district values for the **current** selection (recalculated when you change crime type or when JSON reloads).
- If min = max → all districts use a **mid** opacity so polygons stay visible.
- Opacity applies in **By District** map mode (police districts visible). Switching to **By Ward** hides district fills as today.

---

## Example (Assault selected)
- Citywide YTD: **349**
- North 62 · East 61 · South 134 · West 92  
- South polygon most opaque; East/North relatively lighter (depends on min/max spread).

## Example (All categories)
- District totals = sum of all category district cells (e.g. South highest overall → most opaque).

---

*Implementation: `dashboard.html` — `applyDistrictCrimeOpacityToMap()`, `renderProfessionalRightCards()` branch on `majorCrimeType`.*

## Follow-ups
- **Time period** dropdown still drives other CompStat panels; the right YTD block always reflects **`ytd-breakdown.json`** (Excel Crime Breakdown) until that export is extended for WTD/28-day.
