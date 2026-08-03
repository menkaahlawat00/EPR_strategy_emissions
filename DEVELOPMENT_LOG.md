# Development Log

Running log of work on the Canada EPR Packaging Swap Tool. See `PMD.md` for the
current product/project overview.

---

## 2026-08-03

**Context:** Picked up the project again. Repo was previously only tracked on
GitHub (`menkaahlawat00/EPR_strategy_product`) with no local clone; cloned it to
`~/Desktop/EPR_strategy_product` for continued development.

**Changes made to `index.html`:**

1. **Corrected the Alberta regulatory fee.** The tool previously modeled Alberta's
   ARMA oversight fee as `$0` — negligible, "incorporated into Circular Materials
   rates." This was wrong: ARMA (Alberta Recycling Management Authority) is a
   distinct regulator from Circular Materials (a PRO) and charges its own separate
   annual fee. Confirmed against ARMA's *EPR Oversight Fee Guide* (March 2026) and
   the actual 2026 final PPP rates supplied directly: **$180/year flat fee** for
   producers below ARMA's minimum PPP supply threshold, or **$0.0334/kg** variable
   rate above it. Wired the variable rate into `FEES.AB.regFee` (previously `0`)
   and updated all related labels/notes (province note, EPR note, footer, header
   byline, code comments). The flat-fee/threshold branch is not modeled — ARMA's
   PPP threshold weight isn't published, and retail-scale SKU volumes in this tool
   are well above any plausible small-producer cutoff, so the variable rate is the
   applicable case. Flagged as an open item in `PMD.md`.

2. **Added "EPR fee per unit sold" as a new metric.** Business rationale: producers
   recover EPR costs through product pricing, typically via a flat per-unit
   surcharge (e.g. $0.20/unit across a brand) rather than a SKU-specific charge.
   Showing the actual modelled fee per unit (current vs. alternative vs. delta, in
   ¢/unit) lets a team compare that flat surcharge against the real EPR liability
   for a specific SKU. Added a new metric-card row, a `fmtCents()` formatter, and
   wired `feePerUnitA`/`feePerUnitB`/`feePerUnitDelta` (= annual fee ÷ annual
   units) into `calculate()`. Folded the same figures into the plain-language
   summary text.

3. **Fixed a province-scoping bug in the units label.** The "annual units" input
   was labeled "Annual units supplied into **Ontario** market," and the SKU-info
   panel echoed "Assumed **Ontario** units/year" — both implying the sales forecast
   is province-specific. It isn't: it's the same forecasted volume regardless of
   which province tab is selected. Relabeled to "Forecasted annual units sold"
   (input label, SKU-info panel text, and the SKU-data code comment).

4. **Added Golden Design Rules (GDR) alignment per material.** Read the Canada
   Plastics Pact's *Canadian Guidance* to The Consumer Goods Forum's 9 Golden
   Design Rules for plastic packaging (v1, rev. June 2025, plasticspact.ca) —
   voluntary industry commitments covering things like "no EPS/PS," "no PVC/PVDC,"
   "mono-material flexible film only," "no oxo-degradables." Added a second
   badge+note (green/amber/red/gray "not applicable") next to the existing
   recyclability badge for both current and alternative packaging, citing the
   specific rule number. Non-plastic materials (paper, glass, metal) are marked
   "not applicable" since the GDRs only cover plastic packaging. Notably: foam/EPS
   and multi-layer laminate both come back "Not aligned" — GDR 2(c) explicitly
   names EPS/PS for elimination, and GDR 2 & 6 together ban most of what
   multi-layer laminates are made of (PVC/PVDC, aluminium foil, excess additives).
   Added CSS (`.badge-gray`, `.gdr-label`), a `gdr` field on each `MATERIALS`
   entry, and a `getGdrBadgeClass()` helper alongside the existing
   `getBadgeClass()`.

**Verified in-browser** (via a local `python3 -m http.server`, Chrome): confirmed
the per-unit metric renders and matches the underlying annual-fee math, confirmed
the Alberta province note now correctly separates the ARMA fee from Circular
Materials PRO rates, and confirmed the GDR badges render correctly for both the
"not applicable" (paper) and "Not aligned" (foam/EPS, multi-layer) cases.

**Not yet done / carried to next session:**
- Confirm ARMA's PPP minimum supply threshold weight and, if useful, model the
  flat-fee branch for Alberta the same way Ontario's threshold is modeled
- Commit and push these changes (currently only in the local working tree)
