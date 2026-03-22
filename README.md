# Jersey City Crime Dashboard

Single-file Mapbox dashboard visualizing Jersey City wards, police districts, and precinct stations.

## Local run

1. Set your Mapbox public token in `index.html`:

```js
mapboxgl.accessToken = 'YOUR_MAPBOX_PUBLIC_TOKEN';
```

2. Start a local server:

```bash
python3 -m http.server 4173
```

3. Open [http://127.0.0.1:4173/index.html](http://127.0.0.1:4173/index.html).

## Files

- `index.html` — app UI, data, and map logic
- `dashboard.html` — CompStat / map dashboard
- `data.json` — CompStat bundle for charts and tables
- `ytd-breakdown.json` — **right-hand YTD panel** (7 categories, citywide + district); generated from Excel — see below
- `jc_dashboard_codex_brief.md` — project brief and context

## Refresh YTD panel from Excel

The right column **Total Crime Count (YTD)** and category cards load from **`ytd-breakdown.json`**, exported from the workbook’s **Crime Breakdown** sheet (not hand-edited numbers in HTML).

```bash
python3 scripts/export_ytd_breakdown.py "/path/to/JCIMPACT Weekly Jan Feb 2026.xlsx"
```

Commit the updated `ytd-breakdown.json` and deploy. See **`docs/YTD_PANEL_PREVIEW.md`** for layout and opacity rules.
