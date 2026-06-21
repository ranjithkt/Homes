# Investigation: Why Do Redfin & Zillow Price Two Same-Builder Monroe Homes ~$50K Apart — and Who Wants Each?

You are a highly capable reasoning agent rooted at `C:\Repos\Homes`. Run this end-to-end at your **highest reasoning effort**. This is **guidance, not a script** — it names the angles and the evidence bar; you invent the rest. No hand-holding, no hedging, no narrating the obvious, no click-by-click padding. Every claim earns its place with a cited source or a code-derived calculation. A number with no source is a guess — delete it or source it. **Macro, market, policy, and demand facts move week-to-week in 2026 — every such figure carries a live retrieval timestamp and an explicit as-of date, or it is cut.**

---

## 1. Mission

Two homes by the **same builder (MainVue Homes)**, in the **same Monroe WA 98272 tract (Eaglemont), ~1-2 blocks apart**, carry online valuation **estimates that diverge by ~$50,000** — and *both* Redfin and Zillow roughly reproduce that cross-home gap. Explain it, exhaustively, with evidence. There are **three coupled puzzles**:

- **Cross-home gap (headline / DIFFERENTIAL):** why does HOME A's estimate differ from HOME B's by ~$50K on each site? Decompose it into ranked, dollar-weighted factors. This is a *differential* question between two near-identical, near-adjacent homes.
- **Cross-site gap (per home):** for *each* home, does the **Redfin Estimate** disagree with the **Zestimate**? By how much, and why? Two algorithms disagreeing on the *same* house is itself a clue to what each weights.
- **Price LEVEL & estimate-vs-realized gap (CONTEXT / COMMON-MODE):** what sets the ~$1M **price LEVEL** both homes sit at, and the gap between an *algorithmic estimate* and *what a real buyer pays NOW* — i.e. macro rates/financing, the 2026 policy regime, the Snohomish/Monroe market state, tech-sector wealth, and the depth of local buyer demand? These forces are *largely common to both homes* (see the governing rule).

Second mission, **weighted equally**: **map the buyer-demand ecosystem onto value.** Do NOT start from a fixed persona list. **Enumerate the realistic $1M-tier buyer ecosystem for THIS location, SIZE each segment's share and willingness-to-pay, and identify the MARGINAL buyer that sets the clearing price for EACH home** (it can differ per home by features). The large **H1B-visa Indian professional** family community in the Seattle eastside/Monroe orbit is the **worked anchor example**, not the only segment. AVMs are blind to micro-persona demand; real market value is not — so the marginal-buyer pool explains the gap between an *algorithmic estimate* and *what a real $1M buyer will pay*, and a shift in that pool moves value.

**Governing rule — COMMON-MODE vs DIFFERENTIAL (this governs the entire investigation).** Two homes 1-2 blocks apart share almost all macro/market/policy/wealth conditions, so those forces are **common-mode**: by default they do **NOT** explain the cross-home ~$50K delta. They explain (i) the price **LEVEL**, (ii) the **estimate-vs-realized** gap (market state/timing), (iii) **risk & timing**, and (iv) **which buyer pool is marginal** and how robust that demand is. **Keep the cross-home $50K attribution (differential/micro) SEPARATE from the macro/level/timing analysis (common-mode); never double-count a common-mode force into the $50K bucket.** The one exception — hunt it deliberately — is an **asymmetric interaction**, where a macro force lands unevenly on the two homes (e.g. a jumbo-threshold crossing, an H1B-demand shift hitting the home whose marginal buyer is H1B-Indian, an RTO-revived school/commute salience, a cultural premium attaching to one home's orientation/number/lot). Only when evidenced as asymmetric does that increment move into the $50K delta — with a source; otherwise it stays in the common-mode level/timing analysis.

**Stance — adversarial curiosity.** The gap is a puzzle to be *proven out with evidence*, never asserted. Treat every candidate factor as guilty-of-irrelevance until evidenced, and **if a factor seems not to matter, prove it doesn't** (show the two homes are equivalent on that axis). Quantify or bound-scope every factor. End with a ranked **differential** attribution that *sums toward* ~$50K with an explicit **residual** row — **if the residual is large, you have not finished** — plus a separate common-mode narrative for level/timing/risk.

---

## 2. Execution model — this is what makes the investigation exhaustive (non-negotiable)

Run as an **ENSEMBLE ORCHESTRATOR**, not a lone analyst. Decompose into work-units, fan each unit across multiple models, point-level-consolidate. Three disciplines govern you; follow each exactly.

### 2a. Ensemble orchestration (`agent-orchestration-cursor-cli-ensemble` + `agent-orchestration-cursor-cli`)

- **Decompose into K work-units** with non-overlapping scopes. Suggested cut (you OWN the final decomposition and may refine it — keep scopes non-overlapping and respect feeder sequencing):
  - **U1 — HOME-A source extraction:** Redfin HTML/PDF + Zillow HTML + MLS `.md` + map PNG.
  - **U2 — HOME-B source extraction:** Redfin HTML/PDF + the two owner-dashboard PNGs + map PNG (B's offline estimate numbers live ONLY in those PNGs).
  - **U3 — live gap-fill + the 4-cell discrepancy matrix** (fill what's missing per home; capture current estimates/ranges/comps live).
  - **U4 — valuation-algorithm reverse-engineering** (Zestimate vs Redfin Estimate weighting, list-price anchoring, comp mix, listing richness).
  - **U5 — physical / condition / location factor analysis** from photos + maps + facts.
  - **U6 — comp-selection reconstruction** + neighborhood / same-builder / same-model sales.
  - **U7 — demand-ecosystem research** (enumerate + size the realistic $1M-tier buyer segments; identify the MARGINAL buyer per home; H1B-Indian as the worked anchor; cultural/demographic segments from §7/lens E).
  - **U8 — macro / market-state / policy / wealth research** (rates incl. jumbo threshold, Fed, immigration/H1B, tariffs, tax, Snohomish/Monroe market state, tech RSU/layoffs/RTO). **CURRENT-EVENTS heavy → Tavily-primary, every figure timestamped + 2026 as-of.** Output feeds price-LEVEL, the estimate-vs-realized gap, risk/timing, and the asymmetric-interaction hunt — NOT the $50K differential by default.
  - **U9 — synthesis:** ranked **differential** $50K attribution (common-mode-excluded) + asymmetric-macro-interaction sub-table + separate common-mode level/timing/risk narrative + marginal-buyer→value mapping + deliverables.
  - **U1/U2 feed everything; sequence accordingly** (they are upstream of U3-U9, not pure parallel). U7/U8 are research-heavy and can run parallel to U4-U6 once U1/U2 land; U9 consumes all.
- **Fan each unit across M model slugs** (default **M=3**: `claude-opus-4-8-thinking-xhigh`, `gpt-5.5-extra-high`, `gemini-3.1-pro`). Never run a unit on a single model.
- **Model-slug validation gate (run BEFORE any worktree is created).** Validate **EVERY** slug (defaults or override) for **EXACT** string presence in `cursor-agent --list-models`. **NEVER silently substitute a slug.** If a slug is absent from the live list: do NOT swap in an unvalidated equivalent — **record the failed slug AND the closest-available live slugs in the `ensemble-registry`**, and because you run **headless** and cannot pause to ask, **prefer fanning that unit across only the validated slugs as a logged, degraded slug set** (still honoring the ≥2-finisher consolidation floor) rather than substituting. Proceeding on the closest validated slug is permissible **ONLY as an explicitly-recorded last resort**, never as a silent swap, and never below the ≥2 floor.
- **Launch via the committed script**, one non-blocking call **per tool call**, **≥30s apart via SEPARATE calls** (never `Start-Sleep` inside a launch call — burst dispatch collides on auth/MCP cold-boot):
  ```
  python "C:\Users\ranji\.agents\skills\agent-orchestration-cursor-cli\scripts\launch_child.py" --model "<slug>" --dir "<worktree>" --context-folder "<cand-folder>" --manifest "<shared children-manifest.json>"
  ```
  Pass **ONLY** `--model` + `--dir` + `--context-folder` (+ the shared `--manifest`); the headless/yolo posture (`-p --force --trust --approve-mcps --sandbox disabled --output-format stream-json`) is baked into the script — never pass it. Each candidate gets its OWN `git worktree` (`git worktree add -b ens/<unit>/<slug> <wt> HEAD`) off a worktrees root **OUTSIDE** `C:\Repos\Homes`.
- **Track two layers, kept separate:** (1) the **script-written `children-manifest.json`** (process state — poll with `poll_children.py`, kill stuck children with `kill_child.py` PID-only/triple-guarded, recover/reconcile with `recover.py`; **NEVER** `Stop-Process -Name node` / `taskkill /IM node.exe` — host agent + MCP servers are all `node.exe`); (2) your own **`ensemble-registry.md` / `.json`** (units, slugs, worktrees, consolidation verdicts, lifecycle). Reconcile `git worktree list` against the ledger at every checkpoint so nothing is orphaned.
- **Stuck-candidate policy:** a candidate is stuck only when `poll_children.py` reports `STUCK` (no log growth for the stuck window while alive, or a hard blocker like `not logged in` / `is not a valid model`). Retry the SAME slug once into a fresh worktree; if still stuck after siblings finish, drop ONLY that candidate for that unit. **Slug membership is IMMUTABLE for the run** — the next unit uses the full M again. **Floor: consolidate a unit only from ≥2 finished candidates;** if <2 usable, re-dispatch the whole unit (full M, fresh) up to the circuit-breaker, else surface the failure in the registry.
- **Per-unit consolidation is DELEGATED** to a consolidator child (also via `launch_child.py`, default `claude-opus-4-8-thinking-xhigh`), merging the M outputs **POINT-LEVEL**: complementary valid points → keep both; competing/duplicate points → keep the single best (dedupe); wrong/hallucinated → drop. **No blind union, no lossy single-winner.** The consolidated unit must read as if one analyst produced it and must list which candidates it consumed.
- **Cleanup is LAST**, gated on landed + reviewed. Never remove a worktree before its unit is consolidated and reviewed.

### 2b. Stateful working memory (`stateful-work`)

All scratch state — orchestrator `context.md` / `todos.md` / `insights.md`, the `ensemble-registry`, `children-manifest.json`, every candidate/consolidator folder, all worktrees, and all scratch evidence ledgers / OCR dumps / downloaded pages / intermediate JSON — lives **OUTSIDE** the repo (under a dated working folder in `C:\Users\ranji\OneDrive\Ranjith\Stuff\Books\AI\LLM Context\main\` and a sibling worktrees root). **ONLY the final deliverable documents land in `C:\Repos\Homes\reports\`.** Do not pollute the repo with scratch. Do NOT git commit / push / merge / run destructive git. Do NOT ask the user questions — make the best evidence-backed judgment, record the assumption, and continue.

### 2c. Delegate to code (`delegate-to-code`)

Never eyeball-extract. **HTML → parse embedded `<script>`/JSON blobs with code** (Zestimate / Redfin Estimate, ranges, comps, and sale history live in JSON, not visible text). **PDF → `perform_pdf_ocr`** (`user-mcp-ocr`; OCR targeted pages for large files). **PNG dashboards & maps → `perform_ocr` / `perform_batch_ocr`** (`user-mcp-ocr`). **Photos → vision** for condition/finish/layout **plus `perform_batch_ocr`** for text overlays. **Every $ figure, sqft, ratio, %-of-gap, distance/commute delta, monthly-payment / affordability calc, and the attribution sum → computed in Python**, not generated token-by-token. Build the discrepancy/attribution/comp tables and the rate→payment→affordability math programmatically from extracted fields. **Sanity-check code output against source snippets; if code and visible text conflict, investigate — do not average them away.**

---

## 3. Grounding (verified — sanity-check extraction against this; do NOT invent facts for B)

| | HOME A | HOME B |
|---|---|---|
| Address | 13506 196th Ave SE, Monroe WA 98272 | 13668 198th Ave SE, Monroe WA 98272 |
| IDs | MLS #2528441 · Zillow zpid 246561249 | Zillow zpid 240117187 |
| Listing photos | 40 | 24 |
| Known facts | 4bd/2.5ba; **3,267 sqft finished, no basement**; 2-story; built 2017; lot 5,663 sqft (0.1294 ac); HOA $115/mo; tax $7,575 (2025); condition "Very Good"; Has View; 2 gas fireplaces; central air; tankless WH; **MLS Active, 51 cumulative DOM, on-market 2026-05-22**; APN 01154400001200; schools Chain Lake Elem / Park Place Middle / Monroe High (Monroe district); community CCRs, park, playground, trails; site: deck, fully fenced, outdoor fireplace, patio, garden | **Extract live/offline — do NOT assume.** Beds/baths, finished/total sqft, lot, year, HOA, tax, condition, view, status, list/sale price, DOM, estimate numbers & ranges are all UNKNOWN here and must be pulled from B's Redfin HTML/PDF, the two owner-dashboard PNGs, and the live Zillow/Redfin pages. |

Both are MainVue. The **MainVue floorplan/model name** of each is a load-bearing unknown — same-model vs different-model reshapes the entire comp picture; **resolve it**.

---

## 4. Media manifest — exact absolute paths + per-file ingestion modality (the offline evidence base)

Base folder: `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media`
(A standalone copy of this manifest also lives at `C:\Repos\Homes\prompts\media-manifest.md` — keep any usage consistent with it.)

### HOME A
| Absolute path | Type | Ingestion modality |
|---|---|---|
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 _ MLS# 2528441 _ Redfin.html` | saved Redfin page | Parse embedded JSON/`<script>` (facts, Redfin Estimate, range, price/sale history, listing status, comps) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 _ MLS# 2528441 _ Redfin_files\` | page assets | Usually noise; mine only if it holds structured data/images needed for evidence |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 _ MLS# 2528441 _ Redfin.pdf` | Redfin PDF | `perform_pdf_ocr(input_data="<path>")` (or text layer if present; OCR targeted pages if large) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 - Property Details From MLS.md` | MLS facts | Read directly — authoritative public-fact anchor for HOME A |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 Google Map View.png` | map screenshot | `perform_ocr(input_data="<path>")` + vision (street position, lot, **orientation/facing**, adjacency) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Avenue SE, Monroe, WA 98272 _ MLS #2528441 _ Zillow.html` | saved Zillow page | Parse embedded JSON/`<script>` (Zestimate, range, comps, facts, history) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Avenue SE, Monroe, WA 98272 _ MLS #2528441 _ Zillow_files\` | page assets | Usually noise; mine only if it holds data |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13506 196th Ave SE, Monroe, WA 98272 Photos\` (40 images) | listing photos | Vision for condition/finish/quality/staging/layout/yard; `perform_batch_ocr(inputs=[...])` for text overlays |
| **MISSING for A** | — | **NO Zillow PDF, NO owner-dashboard PNGs** → A's *current* Zestimate/Redfin-Estimate numbers + ranges must be pulled **live** |

### HOME B
| Absolute path | Type | Ingestion modality |
|---|---|---|
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 _ Redfin.html` | saved Redfin page | Parse embedded JSON/`<script>` (facts, Redfin Estimate, range, history, comps) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 _ Redfin_files\` | page assets | Usually noise; mine only if it holds structured data/images |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 _ Redfin.pdf` | Redfin PDF | `perform_pdf_ocr(input_data="<path>")` (text layer if present; OCR targeted pages if large) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 Google Map View.png` | map screenshot | `perform_ocr(input_data="<path>")` + vision (**orientation/facing**, lot, adjacency) |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 Owners View Redfin.png` | Redfin owner dashboard | `perform_ocr(input_data="<path>")` — **Redfin Estimate, range, comps, "what affects your estimate"** |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 Owners View Zillow.png` | Zillow owner dashboard | `perform_ocr(input_data="<path>")` — **Zestimate, range, comps, value factors** |
| `C:\Users\ranji\OneDrive\Ranjith\Stuff\Homes\Monroe\Selling\Media\13668 198th Ave SE, Monroe, WA 98272 Photos\` (24 images) | listing photos | Vision for condition/finish/quality/staging/layout/yard; `perform_batch_ocr(inputs=[...])` for text overlays |
| **MISSING for B** | — | **NO saved Zillow HTML, NO MLS `.md`** → B's full public facts (sqft/beds/baths/lot/year/HOA/tax/status/list price/DOM) must be extracted **live** |

### Asymmetry — call it out and FILL THE GAPS LIVE
- **HOME A has** saved Zillow HTML + authoritative MLS `.md`, but **no Zillow PDF and no owner-dashboard PNGs** → A's *current* estimate numbers + ranges must be pulled **live**.
- **HOME B has** the two owner-dashboard PNGs (the **ONLY** offline source of B's actual Redfin/Zillow **estimate numbers, ranges, and comp tiles**) but **no saved Zillow HTML and no MLS `.md`** → B's full public facts must be extracted **live**.
- OCR the B owner-dashboards **precisely** — they are your only offline window into B's estimates and the comps each site used for B. **Cross-check every offline figure against the live page when reachable; flag any stale/conflicting value** (offline saves may predate the current estimate).

---

## 5. Tool precedence — use the next tool ONLY when the prior is blocked, stale, or incomplete

Redfin and Zillow are **bot-protected**, so WebFetch/Tavily will often be blocked on the property pages → browser-use is the realistic live fallback for those. For comps/market/schools/demand/macro/policy research, Tavily search is primary. **Preserve evidence of every attempt** (record it in the source-attempt ledger, §8).

1. **WebFetch** the URL directly (also use to resolve the Redfin short links).
2. **Tavily MCP `user-tavily`:**
   - Property pages: `tavily_extract(urls=[...], extract_depth="advanced", format="markdown")`
   - Comps / market / schools / commute / community / demand / macro / policy research: `tavily_search(query="<specific query>", search_depth="advanced")`
3. **browser-use (ApplySolo)** — live, logged-in Chrome already launched by the user. Read `C:\Repos\Perplexity-Computer\.cursor\skills\browser-use\SKILL.md` first. Run **from `C:\Repos\Perplexity-Computer`** (NOT `C:\Repos\Homes`), **one command per shell call, no `&&`, no `cd` in the same command**:
   - `$env:BU_CDP_URL="http://localhost:9233"`
   - `$env:BU_SESSION="applysolo"`
   - `python scripts/bu.py open "<url>"` → `python scripts/bu.py state` → `python scripts/bu.py get html` → `python scripts/bu.py screenshot Temp/x.png`
   - then OCR the screenshot by its **absolute path**: `perform_ocr(input_data="C:\\Repos\\Perplexity-Computer\\Temp\\x.png")`.
   - Use browser HTML + screenshot OCR when the visible estimate/range/comp cards do not appear in extracted text. Capture enough page state to PROVE which home/page you read.

**Current-events research (macro / policy / market-state / demographic) — Tavily search is PRIMARY here (not a fallback).** Mortgage rates (30-yr conforming + jumbo), Fed actions/expectations, the FHFA conforming/jumbo limit, H1B/immigration policy, tariffs, tax changes, tech layoffs/RTO mandates, and Snohomish/Monroe market stats are **live 2026 events that move week-to-week and are often litigated** → lead with `tavily_search(query="<specific, 2026-dated query>", search_depth="advanced")` (use `tavily_research` for multi-source synthesis), then WebFetch/browser-use for primary sources (FHFA, USCIS / Federal Register, the Fed, county assessor, MLS/brokerage market reports). **Every macro/policy/market/demographic figure carries (a) its source, (b) a retrieval timestamp, and (c) an explicit "as-of" date** — undated is worthless. Example of the volatility: the Sept-2025 **$100,000 H-1B proclamation fee** was **vacated by a federal court in mid-2026 and is on appeal** — its status as-of your run is unknown until you check it live. Prefer official primary sources; corroborate any single-source macro claim.

**The four URLs to bake in:**
- Zillow A: `https://www.zillow.com/homedetails/13506-196th-Ave-SE-Monroe-WA-98272/246561249_zpid/`
- Zillow B: `https://www.zillow.com/homedetails/13668-198th-Ave-SE-Monroe-WA-98272/240117187_zpid/`
- Redfin (short links — **resolve which maps to which home and cite the resolution evidence**): `https://redf.in/4GtgoF` , `https://redf.in/zNBSpU`

Capture the **current** Zestimate + Redfin Estimate + both ranges + the comp tiles for **both** homes, with **retrieval timestamps** — an Active listing's estimate moves.

---

## 6. Investigation LENSES — run each as a probing question, then **invent more**, then **cross-check**

These are axes, not a checklist. Exercise every one; your real value is the angle you deepen and **the angle nobody listed that you discover**. After running each lens independently, **cross-check them: a factor that surfaces under two lenses is high-confidence; a factor that *should* appear under a second lens but doesn't — investigate why.** Lenses split into two families: **DIFFERENTIAL (cross-home)** lenses that explain the ~$50K delta, and **CONTEXT / COMMON-MODE** lenses that explain the price LEVEL, timing, and the marginal buyer. Keep them separate per the §1 governing rule.

### 6A. Differential (cross-home) lenses — these explain the ~$50K

- **Data-discrepancy lens (start here — often the biggest hidden driver).** Do Redfin and Zillow even *agree* on each home's core inputs — finished vs total sqft, beds, baths, lot size, year built, HOA, tax? Build the 4-cell matrix (2 homes × 2 sites). A site feeding a wrong sqft/lot into its model manufactures a "gap" that is pure data error, not value. Which cells disagree, and does a disagreeing input track the estimate direction?
- **Valuation-algorithm lens.** Where do Zestimate and Redfin Estimate weight differently — comp radius/recency, same-builder/same-model comp inclusion, DOM, price-cut history, prior sale history, tax-assessed value, listing freshness, and **listing richness** (photo count, remark length)? Use the two homes as a natural experiment to infer each algorithm's sensitivities.
- **Listing-status / list-price-anchoring lens (likely high-impact).** An **actively listed** home's estimate is pulled toward its list price; an off-market home's estimate is pure-algorithm. HOME A is **Active (51 DOM, listed 2026-05-22)** — is HOME B active, pending, sold, or off-market on each site? If statuses differ, a large slice of the ~$50K may be *anchoring asymmetry*, not real value. Prove each home's exact status per site and quantify the anchoring pull. Treat active/pending/sold/off-market/stale-dashboard/DOM/price-cut/relist as distinct estimator inputs.
- **Comp-selection lens.** Reverse-engineer which comparable sales each site likely used (from the comp tiles in the HTML JSON and the B owner-dashboards). Reconstruct comp pools by radius, recency, same builder/tract/model, size band, school boundary, view/lot premium, condition. Pull recent neighborhood + same-builder MainVue sales. Show how a different comp mix mechanically produces dollars.
- **Physical-attribute lens.** Finished vs total sqft, lot size & premium, beds/baths count and mix, main-floor bedroom/full bath, garage stalls, stories, year built, view quality, basement/bonus/flex room, outdoor (deck/patio/outdoor fireplace/fence/yard usability), roof/HVAC/water heater. Convert each delta to a $ estimate via local $/sqft and feature comps.
- **Floorplan/model lens.** Are the homes different MainVue plans/variants with different market liquidity? Identify model/floorplan from listing text, photos, county/permit clues, archived listings, or builder plan archives. Tie layout to demand, not just square footage.
- **Condition/quality/photo lens (from photos).** Finish level, kitchen, flooring, appliances, baths, staging, light, view framing, visible upgrades vs wear — A (40 photos) vs B (24). Is the *condition delta* real, or is **photo richness itself** an algorithmic listing-signal (more/better photos → higher estimate) and a merchandising signal to buyers, independent of true condition? Separate the two.
- **Location-microfactor lens.** Corner vs cul-de-sac, lot/view premium, street traffic, backing/side adjacency, greenbelt/open-space/power lines, slope, privacy, sidewalks, kid safety, sun exposure, driveway/garage approach, school walkability, proximity to amenities — what can 1-2 blocks change? Investigate any intra-tract school-boundary or noise nuance despite proximity.
- **Vastu / orientation lens.** For Indian professional buyers, does either home have an **east-facing (or otherwise preferred) entry**, favorable kitchen/stair/master orientation, or a correctable/unfavorable T-junction lot? Derive from the Google Map PNGs, listing photos, compass evidence, and live maps — do not guess. (Cross-listed with the demand-ecosystem and cultural lenses; a factor confirmed under two lenses is high-confidence, and an orientation premium that attaches to only one home is a candidate **asymmetric** increment.)
- **School/community lens.** Are the assigned schools identical? If so, do GreatSchools/Niche/district data, demographics/competitiveness, commute-to-school, or local reputation still differentiate demand? If schools are identical, **prove they do not explain the gap** before moving on.
- **Commute/amenity lens.** Compare both homes for commute to Redmond, Bellevue, Seattle, Bothell, Kirkland, Everett, major tech employers, SR-522/US-2; and proximity to Indian/Asian groceries, temples/gurdwaras/mosques/churches, cricket/community venues, parks, trails, healthcare, retail. At this micro-distance the answer may be "no meaningful difference" — **prove it** with distance/time evidence.
- **Tax/assessment lens.** Do county assessed values, tax history, APN records, permit records, or prior sale records imply a platform input or a real value difference? Separate tax-assessment artifacts from buyer-paid market value.
- **Market-timing / reconciliation / staleness lens (cross-check, easy to miss).** Do the offline saved figures match the live figures for each home? A stale saved estimate masquerading as current would corrupt the whole attribution. Are platform estimates reacting to a moving local market, stale cached owner-dashboard data, or the current Active listing? **Date-stamp every number.**
- **Demand-ecosystem lens (weighted — see §7).**

### 6B. Context / common-mode lenses (A-F) — run these for LEVEL, timing & the marginal buyer, NOT for the ~$50K by default

Per the §1 governing rule, these forces are largely **shared** across two near-adjacent homes, so they explain the price **LEVEL**, the **estimate-vs-realized** gap, **risk/timing**, and **which buyer pool is marginal** — they enter the ~$50K differential **ONLY** as a proven **asymmetric interaction** (and then move to the §8 sub-table with a source). Hold each to the same evidence bar; every figure is **timestamped + 2026 as-of**.

- **A. Macro rates & financing lens.** The 2026 mortgage environment sets purchasing power at the ~$1M tier: current 30-yr **conforming** and **jumbo** rates, the Fed's policy trajectory and market rate expectations, points/buydowns. In code, compute monthly **PITI + HOA + insurance** at each home's price under current rates and a realistic down payment, and how much price a fixed budget buys as rates move — this sets the LEVEL and the estimate-vs-realized gap, and AVMs **lag** rate-driven shifts. **Jumbo threshold (possible ASYMMETRIC hook):** retrieve the current FHFA one-unit limit for **Snohomish County — a high-cost area (2026 high-balance limit ≈ $1,063,750; confirm live)**. Both homes sit near ~$1M; at realistic down payments, check whether either home's **loan** crosses the conforming→jumbo line (jumbo overlays = higher rate / bigger down / stricter DTI). If a ~$50K price difference straddles that threshold for a given down payment, the financing-cost asymmetry feeds the delta — if it doesn't (likely at this price/down-payment), **prove it doesn't** and keep it common-mode. Insurance/climate-cost and property-tax escalation are part of total carrying cost — note any per-home difference.
- **B. Political / policy lens (2026 administration & Congress).** Hunt CURRENT policy and its price transmission, each timestamped:
  - **Immigration / H1B policy** — fees (incl. the 2025 **$100K H-1B proclamation fee** and its 2026 litigation/vacatur status), denial/RFE rates, green-card backlog, visa-insecurity sentiment → directly throttles/shifts the **H1B-Indian demand pool** concentrated in tech suburbs; visa/job risk raises the premium on **resale liquidity** and on safe **school/commute** fundamentals. **Asymmetric hook:** an H1B-demand shift hits harder the home whose marginal buyer is H1B-Indian.
  - **Tariffs / trade policy** → lumber/steel/appliance/material costs → new-construction & **replacement cost** (both homes are 2017 MainVue) → supports the price **floor**.
  - **Tax policy** — SALT cap, mortgage-interest deduction, capital-gains, any 2025-26 changes → high earners' buy/own math.
  - **Fed / monetary policy & political pressure on the Fed** → rate expectations → feeds lens A.
  - **Economic-policy uncertainty / consumer confidence** → big-ticket purchase **timing**.
- **C. Local & regional market-state lens (sets the estimate-vs-realized gap).** Monroe / 98272 / Snohomish County: months of supply / inventory, absorption rate, median-price **YoY trend** (appreciating vs cooling), **sale-to-list ratio**, **DOM trend**, **seasonality** (HOME A listed 2026-05-22 — peak spring/summer). The **new-construction pipeline** (MainVue + competitors) and **builder incentives** (rate buydowns on new homes) cap resale ceilings for 2017 builds; **rate lock-in** (low-rate owners not selling) constrains inventory. Eastside-vs-Monroe price differential and migration. A hot vs cooling market changes AVM behavior and the **estimate-vs-realized gap** — name which regime you're in and how far real clearing prices sit from the algorithmic estimates.
- **D. Tech-sector & wealth-effect lens (moves LEVEL and LOCATION preference).** The $1M Monroe/eastside pool is heavily tech-employed → **RSU/stock-comp wealth** (equity-market level drives down-payment capacity), **AI-era layoffs / restructuring** (job security — and for a visa holder a layoff can force a sale, i.e. both a demand cut and a forced-supply risk), and **return-to-office mandates** (Amazon/Microsoft RTO revives commute salience → reshapes suburb demand, reversing remote-work normalization). **Asymmetric hook:** RTO-revived commute/school-boundary salience can favor whichever home is better positioned for the eastside commute.
- **E. Cultural-demand & demographic-concentration lens (broaden BEYOND Indian/Vastu).** Enumerate the FULL set of cultural/demographic buyer segments realistically active here and their distinct, **evidence-derived** preferences: other South Asian communities; **East-Asian** buyers (feng-shui; lucky/unlucky **house-number & lot superstitions** — e.g. tetraphobia around "4", preference for "8"); **multigenerational-living** cultures (main-floor bed + full bath); **faith-community proximity** (temples, gurdwaras, mosques, churches); **local PNW move-up families**. Demographic **CONCENTRATION** creates a localized premium/discount. Derive every preference from demographics / school-composition / community data via Tavily — **NEVER from stereotype**. Cross-listed with the Vastu/orientation lens; a house-number, entry orientation, or lot geometry that triggers a cultural premium is a candidate **asymmetric** per-home increment.
- **F. Replacement-cost / new-construction substitution lens.** Both homes are 2017 MainVue builds competing against newer construction. Building on lens B (tariff/material/labor costs → **replacement cost** as a price **floor**) and lens C (the new-build pipeline + builder rate-buydown incentives as a resale **ceiling**), test the per-home **substitution quality**: does one home better substitute for a new build through condition, finishes, floorplan modernity, or warranty-like buyer perception? A common-mode floor/ceiling does not move the $50K; a proven per-home substitution advantage is a candidate **asymmetric** increment.

**Invent additional lenses** as evidence suggests (e.g., assessor/tax-roll vs portal mismatch, seller concessions, HOA/CCR differences, solar/ADU, financing/insurability, micro-flood/zoning, insurance-cost/climate-risk, new-build substitution). Name any you add, classify it differential vs common-mode, and hold it to the same evidence bar.

---

## 7. Demand ecosystem — enumerate, size, find the marginal buyer, tie demand to value

AVMs do **not** model micro-persona demand, so this analysis explains the gap between an *algorithmic estimate* and *what a real $1M buyer will pay* — a distinct, central part of the puzzle. **Do NOT start from a fixed persona list.** Instead:

1. **ENUMERATE** the realistic buyer ecosystem for THIS price tier (~$1M) + location (Monroe 98272 / eastside orbit) from evidence — demographics, school composition, local sales, community/faith data (Tavily).
2. **SIZE** each segment: its approximate share of the active $1M buyer pool and its willingness-to-pay (and what it will/won't pay for).
3. **Identify the MARGINAL buyer per home** — the segment that actually sets the clearing price for HOME A and (separately) for HOME B. **Price is set by the marginal buyer pool, which can differ per home by features** (orientation, layout, lot, school sub-boundary, house number). Where the marginal buyer differs between the two homes, that difference is itself a demand-driven contributor to the ~$50K — quantify it (it is one of the few demand factors that can legitimately enter the differential).

Derive every preference from **evidence** (orientation from the map PNGs, finishes from photos, schools/commute from data) — **never from stereotype**; use a preference hypothesis only when anchored to a sourceable local-demand, listing, school/community, or property fact.

**Worked anchor — H1B-visa Indian professional families buying ~$1M in the Seattle eastside/Monroe orbit** (the user's original example; the worked case, not the only segment). Research and weigh: GreatSchools ratings **and** school competitiveness/ethnic composition; commute to Redmond/Bellevue/Seattle/Bothell/Kirkland tech hubs; proximity to Indian groceries, Hindu temples, and community; **Vastu** (east-facing entrance, kitchen/master/stairs orientation, no T-junction lot); multigenerational space (bedroom + full bath on main); new construction & modern finishes; larger sqft / more bedrooms; low-maintenance yard; cul-de-sac safety for children; park/trail access; strong **resale liquidity** (visa/job-risk — sharpened by the current H1B-fee/immigration regime, §6B-B — raises the premium on liquidity + strong school/commute fundamentals). Determine which home this segment prefers and why, and translate that demand into a $ effect (or rank-weighted direction) on value and on the estimate-vs-realized gap.

**Other segments to enumerate, size, and weigh (non-exhaustive — let evidence add more; fold in §6B-E's cultural segments):** other South Asian and **East-Asian** buyers (feng-shui, house-number/lot superstition); **multigenerational** families (main-floor bed+bath); move-up **local PNW families** (schools, yard, neighborhood familiarity, carrying cost); equity-rich **relocators / remote-hybrid tech workers** (newer construction, view, space, finish, WFH rooms, commute tolerance, resale); **investors / value-sensitive** buyers (rental/resale calculus); **downsizers**; plus any segment the evidence surfaces.

For **every** segment output a **verdict**: preferred home, its share/willingness-to-pay, the 2-3 decisive evidenced factors, disqualifiers/sweeteners, and the directional $ effect on value. If a segment is indifferent, **prove indifference**. Where a segment's preferred home is the *lower-estimate* home, that tension is a finding — explain it. **Close with the marginal-buyer verdict for EACH home** and the demand→value mapping that follows from it.

---

## 8. Evidence, ledgers, attribution & deliverables

### Evidence bar
- **Every material assertion cites a source.** Offline → absolute file path + extracted field / OCR text / parsed JSON key / photo index. Live → URL + extracted field + page title/state + timestamp + fetch method. Derived → input-source list + code-generated output. Macro/policy/market → source + **retrieval timestamp + as-of date**. **No source → cut it.**
- **COMMON-MODE vs DIFFERENTIAL (governing — do not violate).** Before assigning any factor a dollar value, label it **DIFFERENTIAL** (it differs across the two near-adjacent homes → eligible for the ~$50K table) or **COMMON-MODE** (macro/market/policy/wealth shared by both → goes to the level/timing/risk narrative, **NEVER** the $50K table). A common-mode force enters the differential ONLY as a **proven asymmetric interaction**, and then only the asymmetric increment, sourced, via the 7a sub-table. **Never double-count a common-mode force into the $50K.**
- **Quantify each DIFFERENTIAL factor's contribution to the ~$50K gap** (in $ or a bounded range) with an explicit **confidence** (high/medium/low + reason) and the **assumptions** behind it.
- **Three-bucket classification for every DIFFERENTIAL factor:** (a) *algorithmic artifact* (list-price anchoring, comp mix, bad input data, photo-count signal, staleness), (b) *real value difference* (physical/location/condition), (c) *buyer-demand difference* (marginal-buyer/persona pull). Use a 4th label `uncertain/mixed` only when forced. The same nominal "gap" can sit in different buckets per site — keep them distinct, and **explicitly separate "why the estimates differ" from "what a rational buyer would actually pay."**
- **Conflict handling:** do NOT average conflicting platform facts. Identify the conflict, privilege the best source for that field, and estimate the $ impact of the wrong input. If offline screenshots disagree with live pages, treat timestamps + page context as evidence, not noise.

### Required evidence ledgers (build with code; keep scratch outside the repo, surface summaries in the report)
- **Source-attempt ledger:** per URL/media file — tool used, success/failure, timestamp, what was extracted.
- **Comp ledger:** address, status (sold/active/pending), sale/list price, date, sqft, lot, beds/baths, distance, builder/model if known, source, why included/excluded.
- **Photo/condition ledger:** per-home summary + notable photo evidence; do not overfit one attractive image.
- **Demand-ecosystem ledger:** per segment — estimated share, willingness-to-pay, source-backed preference evidence, property-specific mapping, and the **marginal-buyer verdict per home**.
- **Macro / market / policy ledger:** each rate / Fed / jumbo-limit / H1B-policy / tariff / tax / market-stat / RSU-RTO figure with source + **retrieval timestamp + as-of date** + which mission element it informs (LEVEL / timing / risk / marginal-buyer / asymmetric-interaction).

### Deliverables — land ONLY these in `C:\Repos\Homes\reports\`
A standalone primary report (e.g. `C:\Repos\Homes\reports\monroe-home-price-divergence-investigation.md`); use supporting files only if they improve readability, but the primary report must stand alone (do not hide required tables in scratch files). It must contain:
1. **Executive answer** — one dense page naming the dominant explanation of the estimate gap, the price-**LEVEL** & timing context, and the **marginal buyer per home** + which segments prefer which home.
2. **Property/source summary** — both homes, all known/extracted facts, the Redfin short-link → address mapping, source timestamps.
3. **The 4-cell data-discrepancy matrix** (Redfin-A, Zillow-A, Redfin-B, Zillow-B) for core facts **plus** each site's current estimate and range per home, with conflicts flagged.
4. **Platform-estimator analysis** — Zestimate vs Redfin Estimate behavior; status/listing/DOM/comp/list-price/photo artifacts.
5. **Physical / condition / location / floorplan comparison.**
6. **Comparable-sales reconstruction** + likely comp-mix explanation.
7. **Ranked DIFFERENTIAL factor-attribution table for the ~$50K cross-home gap — COMMON-MODE-EXCLUDED.** Each factor with $ contribution (or range), bucket (a/b/c), confidence, evidence pointer, assumptions, and an explicit **residual** row (gap not explained). Contributions sum directionally toward ~$50K; if exact summation isn't defensible, give a reconciled range and explain overlap. **No common-mode macro/market/policy force appears in this table.** **If the residual is large, keep digging before finalizing.**
   - **7a. Asymmetric-macro-interaction sub-table.** Any macro/market/policy/wealth/cultural force **proven** to land unevenly on the two homes: the increment ($), the home it favors, the mechanism, and the source. These — and ONLY these — roll into the item-7 reconciliation. If none survive the evidence bar, say so explicitly (that is the expected default).
8. **Macro / market-state / policy / wealth context + price-LEVEL & estimate-vs-realized-gap analysis (COMMON-MODE).** What sets the ~$1M level; the 2026 rate / jumbo-threshold / Fed environment; the policy regime (H1B/immigration, tariffs, tax) and its demand transmission; the Snohomish/Monroe market state (inventory, YoY, sale-to-list, DOM, seasonality); tech wealth / layoffs / RTO; and the resulting estimate-vs-realized gap and risk/timing read. **Every figure timestamped + as-of.** State plainly: these are LEVEL/timing forces, not $50K drivers (except any item-7a increments).
9. **Demand-ecosystem analysis** — enumerated + sized segments, per-segment verdict, the H1B-Indian worked anchor treated as central, and the **marginal-buyer-per-home** mapping with the demand→value translation.
10. **Confidence / assumptions / open-questions** — what could not be verified offline, what was fetched live, what remains uncertain (including the as-of staleness risk on macro/policy facts) and why, and which uncertainties would most change the answer.

---

## 9. Self-check before finishing
- Did you extract both Redfin and Zillow estimate numbers AND ranges for BOTH homes (live where offline is missing)?
- Did you resolve which Redfin short link maps to which address, with cited evidence?
- Did you prove or eliminate data-input discrepancy as a driver (the 4-cell matrix)?
- Did you resolve each MainVue floorplan/model, and each home's exact per-site listing status?
- Did you distinguish algorithmic artifacts from real market value from buyer demand (three buckets) — for **differential** factors only?
- Did you **separate common-mode macro/market/policy context from the cross-home $50K differential, with NO double-counting** (no macro force in the $50K table except proven item-7a asymmetric increments)?
- Did you capture the **2026 macro/policy/market state** — rates (incl. the Snohomish jumbo threshold), Fed, H1B/immigration, tariffs, tax, Snohomish/Monroe market stats, tech RSU/layoffs/RTO — each with a **retrieval timestamp + as-of date**?
- Did you **ENUMERATE and SIZE** the buyer ecosystem and name the **MARGINAL buyer for EACH home** (not only H1B-Indian)?
- Did you test for **asymmetric macro interactions** (jumbo straddle, H1B-demand asymmetry, RTO commute/school salience, cultural number/orientation premium, per-home new-build substitution) and route ONLY proven asymmetric increments into the $50K table?
- Did you treat H1B Indian professional family demand as the worked anchor **within** an enumerated, sized ecosystem, WITHOUT stereotyping (evidence-anchored)?
- Does the ranked **differential** attribution sum toward ~$50K with a small, explained residual, with the common-mode level/timing/risk narrative kept separate?
- Does every important claim cite a source or a code-derived calculation (and every macro/policy figure carry a timestamp + as-of date)?
- Did all scratch state stay OUTSIDE `C:\Repos\Homes`, with only final docs under `C:\Repos\Homes\reports\`?

## 10. Style mandate
Dense, direct imperatives. No praise, no hedging, no restating the obvious, no click-by-click padding. Name angles, provoke maximum reasoning and live research, **invent more lenses, and cross-check lenses** — a factor confirmed under two independent lenses outranks one seen under a single lens. Keep macro/policy/market coverage **decision-relevant, not an economics essay**: name the force, its 2026 as-of figure, and its transmission to LEVEL / timing / marginal-buyer — then stop. The **common-mode-vs-differential separation must be unmistakable** in the output: a reader must never mistake a level/timing force for a $50K driver. A short, rigorously-sourced result that *proves* it looked hard beats a long one that performs thoroughness. Finish only when the **differential** attribution sums toward ~$50K with a small, explained residual, the common-mode level/timing/risk context is laid out separately, and every segment (with the marginal buyer per home) has a verdict.
