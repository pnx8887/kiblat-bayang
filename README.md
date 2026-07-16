# 🕋 Arah Kiblat Melalui Bayang

**Live app:** https://pnx8887.github.io/kiblat-bayang/

A free, installable web app that finds the Qibla direction using the classic shadow-stick (gnomon) method — combined with real solar-position astronomy, so it works accurately at any time of day, from any location, without needing a compass.

Interface is in Bahasa Malaysia.

---

## What it does

- Calculates the exact great-circle bearing to the Kaaba from your location, and the sun's live position, to work out which way a vertical pole's shadow should fall
- Shows a live compass dial plus a plain-language "turn X° left/right from your shadow" instruction
- **AR camera mode** — overlays two fixed arrows (shadow vs. Qibla) at the correct relative angle over your live camera feed, so you visually align the on-screen arrow with your real shadow. No magnetometer/compass sensor used, so no drift or calibration issues
- **Rasdul Kiblat detection** — automatically calculates (not hardcoded) the two days each year the sun sits directly over the Kaaba, and tells you to simply face the sun during that window
- Location via GPS, manual lat/long entry, IP-based fallback, or pin-drop on an OpenStreetMap picker
- Installable as a home-screen PWA — works full-screen like a native app, with an offline app shell

## How the math works

- **Qibla bearing** — standard great-circle initial bearing formula, from the observer's coordinates to the Kaaba (21.4225° N, 39.8262° E)
- **Sun position** — NOAA-style solar position algorithm (solar declination, equation of time, hour angle → elevation & azimuth)
- **Shadow direction** — sun azimuth + 180° (a vertical object's shadow always falls opposite the sun)
- **Rasdul Kiblat** — the two yearly moments the sun's calculated elevation at the Kaaba's own coordinates reaches ~90° (zenith), found by numerical search rather than a fixed calendar date, so it stays correct every year

## Tech stack

Single-file vanilla HTML/CSS/JS — no build step, no framework, no backend/server. Everything runs client-side in the browser.

- Camera access via `getUserMedia`
- Location via the Geolocation API, with IP-geolocation and map-pin fallbacks
- Map picker: [Leaflet.js](https://leafletjs.com/) + [OpenStreetMap](https://www.openstreetmap.org/copyright) tiles
- Fonts: [Spectral, IBM Plex Sans, IBM Plex Mono](https://fonts.google.com/) (Google Fonts)
- Installable via a Web App Manifest + Service Worker (PWA)

## Running locally / self-hosting

No build step needed — it's static files.

1. Clone or download this repo
2. Serve the folder with any static file server (camera/location APIs require a secure context, so `https://` or `localhost` — opening the file directly as `file://` will **not** work for those features)
   ```
   npx serve .
   ```
   or push it to GitHub Pages / Netlify / Vercel / any static host
3. Open in a browser and allow camera/location permissions when prompted

## Files

| File | Purpose |
|---|---|
| `index.html` | The entire app — UI, styling, and logic |
| `manifest.json` | PWA manifest (name, icons, colors) |
| `sw.js` | Service worker for offline app-shell caching |
| `icon-*.png` | App icons |

## Disclaimer

This tool is provided free, "as-is," with no accuracy guarantee. It is not an official JAKIM product. Direction accuracy depends on your device's GPS precision, clock, and timezone. For anything requiring absolute precision (e.g. building a new mosque/surau), please verify with JAKIM or your local religious authority.

No personal data is collected, stored, or transmitted anywhere — location and camera feed are processed entirely on-device, in your own browser.

## License

Free to use, modify, and share.
