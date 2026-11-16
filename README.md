# Haze

Single-page monitor for Singapore haze and ASEAN weather. Plain static HTML: no build step, no dependencies.

- **Haze (PSI, PM2.5, PM10):** National Environment Agency via data.gov.sg, Singapore only
  (`https://api-open.data.gov.sg/v2/real-time/api/psi`).
- **Weather (all cities):** [Open-Meteo](https://open-meteo.com).

The page fetches both feeds in the browser on load and every 10 minutes. If a request fails
(offline, rate-limited), it falls back to a saved copy embedded in `index.html` and says so in the
status chip and footnote.

## Files

| File | Purpose |
| --- | --- |
| `index.html` | The whole app |
| `favicon.svg` | Tab icon |
| `vercel.json` | Clean URLs and basic security headers (optional) |

## Deploy to Vercel

1. Push these files to the root of a GitHub repository.
2. In Vercel: **Add New → Project**, import the repository.
3. Framework Preset: **Other**. Leave Build Command and Output Directory empty. Deploy.

Or from the terminal: `npx vercel --prod`.

## Run locally

Open `index.html` in a browser, or serve the folder: `npx serve .`

## Notes

- data.gov.sg may rate-limit anonymous requests. If you see the "Saved copy" chip on the deployed site,
  that is the likely cause. data.gov.sg offers free API keys; because this site is client-side, a key
  would be visible to visitors, so if you need one, call the API from a small Vercel serverless
  function instead and have the page fetch that.
- Saved-copy data in `index.html` is a reading from 16 Nov 2026, 10:00 SGT. Update `SNAP_PSI` and
  `SNAP_WX` if you want a fresher fallback.
- Area boundaries on the map are approximate and the example neighbourhoods are illustrative.
