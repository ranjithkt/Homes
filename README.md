# Homes — Monroe Home-Price-Divergence Investigation

This repo holds the **investigation prompt** and **media manifest** for explaining why Redfin and Zillow price two same-builder (MainVue) Monroe WA 98272 homes ~$50K apart — separating the cross-home delta from the common-mode 2026 macro/rates/policy/market-state backdrop that sets the ~$1M price level — and mapping the ~$1M buyer-demand ecosystem (with H1B-visa Indian professional families as the worked anchor) onto each home to find the marginal buyer.

- **The two homes:**
  - HOME A — 13506 196th Ave SE, Monroe WA 98272 (MLS #2528441, Zillow zpid 246561249)
  - HOME B — 13668 198th Ave SE, Monroe WA 98272 (Zillow zpid 240117187)

## Contents
- `prompts/monroe-home-price-divergence.prompt.md` — the standalone investigation prompt (mission, ensemble execution model, embedded media manifest, tool precedence, lenses, personas, evidence/attribution, deliverables).
- `prompts/media-manifest.md` — canonical media manifest (exact absolute paths + per-file ingestion modality + the offline-data asymmetry/gap notes).
- `reports/` — where the executor lands its final deliverables (the only repo location for investigation output).

## How to run
Open `prompts/monroe-home-price-divergence.prompt.md` and run it with a Cursor agent rooted at this repo (`C:\Repos\Homes`). All scratch/working state stays outside the repo; only final reports land in `reports/`.
