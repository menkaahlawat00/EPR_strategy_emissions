# Canada EPR Packaging Swap Tool — Product/Project Doc (PMD)

## Purpose
A prototype decision-support tool for Own Brands retail teams evaluating packaging
material swaps. Given a SKU's current packaging (material + weight) and a proposed
alternative, it estimates:
- Annual packaging tonnage and the tonnage delta from a swap
- Annual EPR (Extended Producer Responsibility) regulatory + PRO fee obligation,
  and the fee delta from a swap
- EPR fee per unit sold — the underlying per-unit cost before any consumer-facing
  markup, so it can be compared against a flat per-unit cost-recovery surcharge
- A recyclability rating for each material and whether the swap improves it

Covers two provincial EPR regimes: Ontario (RPRA) and Alberta (ARMA + Circular
Materials).

## Target Users
Own Brands / private-label packaging and procurement teams deciding whether a
material swap is worth pursuing — before requesting a formal PRO quotation.

## Why "fee per unit" matters (business rationale)
Producers ultimately hand off EPR costs to consumers through product pricing, most
commonly as a flat per-unit surcharge (e.g. $0.20/unit across a brand) rather than a
SKU-specific charge. Knowing the actual modelled EPR fee per unit lets a team check
whether a flat cost-recovery surcharge is under- or over-shooting the real EPR
liability for a specific SKU — and whether a material swap changes that math enough
to be worth pursuing.

## Current Features
- Province selector (Ontario / Alberta) — swaps fee schedules and disclosure notes
- SKU search/lookup against a sample Compliments-brand product catalog, or manual
  entry of material + weight + annual units
- Annual tonnage (current vs. alternative vs. delta)
- Annual EPR fee estimate in CAD (current vs. alternative vs. delta)
- EPR fee per unit sold, in ¢/unit (current vs. alternative vs. delta)
- Recyclability rating per material (green/amber/red) with notes
- Golden Design Rules (GDR) alignment per material (green/amber/red/n.a.) — directional
  alignment with the Canada Plastics Pact's Canadian Guidance to The Consumer Goods
  Forum's 9 Golden Design Rules for plastic packaging (voluntary industry commitments,
  not regulatory requirements)
- Plain-language summary combining all of the above

## Data Sources & Assumptions

**Ontario:**
- RPRA compliance fee: $0.0097/kg, confirmed 2026 rate, flat rate for producers
  over 50,000 kg
- PRO collection fees: **indicative estimates only** — Ontario PRO rates are not
  publicly published (private fee-setting process); actual fees require direct
  PRO quotation (Circular Materials, Ryse Solutions, or H2 Compliance)

**Alberta:**
- PRO fees: published Circular Materials Alberta 2025 Fee Schedule (confirm at
  circularmaterials.ca)
- ARMA EPR oversight fee (separate from PRO/Circular Materials fees): 2026 final
  rates per the ARMA *EPR Oversight Fee Guide* (March 2026, albertarecycling.ca),
  PPP (Single-use Products, Packaging and Paper Products) category:
  - Variable rate: $0.0334/kg, for producers above ARMA's minimum PPP supply
    threshold
  - Flat fee: $180/year, for producers under that threshold
  - (HSP — Hazardous and Special Products — category rates: $325/year flat,
    $0.1026/kg variable. Not applicable to this tool, which covers packaging only.)

**Both provinces:** annual units sold is treated as a single, province-agnostic
forecast — the same product volume, not a separately-forecast per-province figure.

**Golden Design Rules:** Canada Plastics Pact, *Canadian Guidance* to The Consumer
Goods Forum's Golden Design Rules for Plastic Packaging (Version 1, revised June
2025, plasticspact.ca). GDRs apply to plastic packaging only — paper, glass, and
metal are marked "not applicable." Alignment status is a directional read on the
material *category* (e.g. all foam/EPS is flagged per GDR 2(c); all multi-layer
laminate is flagged per GDR 2 & 6) — not a certification of any specific SKU's
actual construction.

## Known Limitations
- Ontario PRO rates are estimates, not confirmed figures — do not use for
  compliance reporting or budgeting without direct PRO quotation
- Alberta's ARMA minimum PPP supply threshold (the weight cutoff between the flat
  $180/year fee and the $0.0334/kg variable rate) is not published in the Oversight
  Fee Guide and is not modeled — this tool always applies the variable rate,
  which is the applicable case for retail-scale SKU volumes
- The tool models per-SKU EPR liability; real ARMA/RPRA obligations are assessed
  at the whole-producer level across all SKUs supplied, not SKU-by-SKU
- SKU catalog is a sample/mock dataset for demonstration, not real Compliments
  brand data
- This is a prototype for upstream design decision support only — not compliance
  advice; always confirm final obligations with your PRO / RPRA / ARMA before
  reporting or budgeting

## Open Items
- Confirm Alberta's ARMA PPP minimum supply threshold weight (contact
  epr@albertarecycling.ca) so the flat-fee/variable-rate branch can be modeled
  the same way Ontario's is
- Confirm current Ontario PRO rates directly with a PRO if this moves beyond
  prototype stage
- Consider whether "fee per unit" should also show a suggested/example flat
  cost-recovery surcharge for direct side-by-side comparison

## Repo
- Live: https://menkaahlawat00.github.io/EPR_strategy_product/
- GitHub: https://github.com/menkaahlawat00/EPR_strategy_product
