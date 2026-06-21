# Media Manifest — Monroe Home-Price-Divergence Investigation

Canonical reference for the offline evidence base. Kept **consistent** with the manifest embedded in `monroe-home-price-divergence.prompt.md` (same paths + modalities). Base folder is **verified to exist**.

Base folder: `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media`

Two homes, **same builder (MainVue Homes)**, **same Monroe WA 98272 tract (Eaglemont)**, ~1-2 blocks apart. The offline media set is **asymmetric** per home (see below) — the executor MUST fill gaps via the live-tool precedence (WebFetch → Tavily → browser-use).

## Ingestion rules (apply per file type)
- **HTML saved pages:** high-value data (facts, Zestimate / Redfin Estimate, ranges, history, comps) lives in embedded JSON / `<script>` blobs, not just visible text — **parse it with code** (delegate-to-code), don't eyeball.
- **PDFs:** `perform_pdf_ocr(input_data="<path>")` (`user-mcp-ocr`); use the text layer if present; OCR targeted pages for large files.
- **PNGs (owner dashboards, maps):** `perform_ocr(input_data="<path>")`; batch many with `perform_batch_ocr(inputs=[...])`. The HOME B owner dashboards are the **ONLY** offline source of B's actual estimate numbers / ranges / comp tiles — OCR them carefully.
- **Photos:** vision for condition, finish, kitchen, flooring, staging, upgrades, layout, lot/yard; `perform_batch_ocr` for any text overlays. Note 40 (A) vs 24 (B) and whether photo richness itself is an estimate/merchandising signal.
- **`.md`:** read directly.
- **Cross-check:** validate every offline figure against the live page when reachable; **flag any stale/conflicting value** (offline saves may predate the current estimate).

## HOME A — 13506 196th Ave SE, Monroe WA 98272 (MLS #2528441, Zillow zpid 246561249)

| Absolute path | Type | Ingestion modality |
|---|---|---|
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 _ MLS# 2528441 _ Redfin.html` | saved Redfin page | Parse embedded JSON/`<script>` (facts, Redfin Estimate, range, price/sale history, listing status, comps) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 _ MLS# 2528441 _ Redfin_files\` | page assets | Usually noise; mine only if it holds structured data/images |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 _ MLS# 2528441 _ Redfin.pdf` | Redfin PDF | `perform_pdf_ocr(input_data="<path>")` (text layer if present; OCR targeted pages if large) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 - Property Details From MLS.md` | MLS facts | Read directly — authoritative public-fact anchor for HOME A |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 Google Map View.png` | map screenshot | `perform_ocr(input_data="<path>")` + vision (street position, lot, orientation/facing, adjacency) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Avenue SE, Monroe, WA 98272 _ MLS #2528441 _ Zillow.html` | saved Zillow page | Parse embedded JSON/`<script>` (Zestimate, range, comps, facts, history) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Avenue SE, Monroe, WA 98272 _ MLS #2528441 _ Zillow_files\` | page assets | Usually noise; mine only if it holds data |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 Photos\` (40 images) | listing photos | Vision for condition/finish/quality/staging/layout/yard; `perform_batch_ocr(inputs=[...])` for text overlays |
| **MISSING for A** | — | **NO Zillow PDF, NO owner-dashboard PNGs** → pull A's current Zestimate/Redfin-Estimate numbers + ranges **live** |

### HOME A grounding facts (from the MLS `.md` — use to sanity-check extraction)
4bd / 2.5ba; 3,267 sqft finished (no basement); 2-story; built 2017; lot 5,663 sqft (0.1294 ac); HOA $115/mo; tax $7,575 (2025); condition "Very Good"; Has View; 2 gas fireplaces; central air; tankless WH; MainVue Homes; MLS Active; 51 cumulative DOM; on-market 2026-05-22; APN 01154400001200; schools Chain Lake Elem / Park Place Middle / Monroe High (Monroe district); community CCRs, Park, Playground, Trails; site: deck, fully fenced, outdoor fireplace, patio, garden space.

## HOME B — 13668 198th Ave SE, Monroe WA 98272 (Zillow zpid 240117187)

| Absolute path | Type | Ingestion modality |
|---|---|---|
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 _ Redfin.html` | saved Redfin page | Parse embedded JSON/`<script>` (facts, Redfin Estimate, range, history, comps) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 _ Redfin_files\` | page assets | Usually noise; mine only if it holds structured data/images |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 _ Redfin.pdf` | Redfin PDF | `perform_pdf_ocr(input_data="<path>")` (text layer if present; OCR targeted pages if large) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 Google Map View.png` | map screenshot | `perform_ocr(input_data="<path>")` + vision (orientation/facing, lot, adjacency) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 Owners View Redfin.png` | Redfin owner dashboard | `perform_ocr(input_data="<path>")` — Redfin Estimate, range, comps, "what affects your estimate" |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 Owners View Zillow.png` | Zillow owner dashboard | `perform_ocr(input_data="<path>")` — Zestimate, range, comps, value factors |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 Photos\` (24 images) | listing photos | Vision for condition/finish/quality/staging/layout/yard; `perform_batch_ocr(inputs=[...])` for text overlays |
| **MISSING for B** | — | **NO saved Zillow HTML, NO MLS `.md`** → extract B's full public facts (sqft/beds/baths/lot/year/HOA/tax/status/list price/DOM) **live** |

### HOME B grounding
Deliberately incomplete offline. Do **not** invent B's sqft, beds, baths, lot, year, HOA, taxes, status, estimate numbers, ranges, or listing history — extract them. The MainVue floorplan/model is a load-bearing unknown for both homes; resolve it.

## Asymmetry (central to the investigation)
- **HOME A** has saved Zillow HTML + authoritative MLS `.md`, but **no Zillow PDF and no owner-dashboard PNGs** → A's current estimate numbers + ranges are a **live** gap.
- **HOME B** has the two owner-dashboard PNGs (the **only** offline source of B's actual Redfin/Zillow estimate numbers, ranges, comp tiles) but **no saved Zillow HTML and no MLS `.md`** → B's full public facts are a **live** gap.
- OCR the B owner-dashboards precisely; cross-check every offline number against the live page when reachable and flag stale/conflicting values.

## Live sources to fill the gaps
- Zillow A: `https://www.zillow.com/homedetails/13506-196th-Ave-SE-Monroe-WA-98272/246561249_zpid/`
- Zillow B: `https://www.zillow.com/homedetails/13668-198th-Ave-SE-Monroe-WA-98272/240117187_zpid/`
- Redfin short links (resolve which maps to which home): `https://redf.in/4GtgoF` , `https://redf.in/zNBSpU`

Redfin/Zillow are bot-protected; live capture typically requires browser-use (ApplySolo) against the logged-in Chrome. Timestamp every live figure.
