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
- `jc_dashboard_codex_brief.md` — project brief and context
