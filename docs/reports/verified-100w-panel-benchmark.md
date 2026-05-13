# Verified 100 W Solar Panel Public-Spec Benchmark

## Report purpose

This report demonstrates the `pv-diligence` method using publicly visible 100 W solar panel products with available specification data.

The goal is not to certify any module. The goal is to show how public product specifications can be converted into deterministic engineering checks:

- area-derived module efficiency
- claimed-efficiency interpretation
- electrical consistency from `Vmp * Imp`
- fill-factor sanity check from `Pmax / (Voc * Isc)`
- thermal derating when temperature coefficient is available
- evidence maturity classification

## Scope

This benchmark focuses on compact 100 W modules and portable/off-grid panels. The products are selected because public data was available during source review.

| Product | Product class | Evidence basis |
|---|---|---|
| ZOUPW TC100W | 100 W N-type compact module | public product page/specification data |
| CALLSUNSOLAR 100 W N-Type | 100 W N-type compact module | public product page/specification data |
| VXB 100 W N-Type | 100 W compact module | public product page/specification data |
| TP-Link VIGI 100 W | 100 W camera/security solar panel | manufacturer product page |
| BLUETTI SP100L | 100 W portable folding solar panel | public product page/specification data |

## Central engineering question

Many public listings advertise high cell efficiency, often around 23 to 25 percent. That number should not automatically be interpreted as full framed-module efficiency.

The core check is:

```text
module_efficiency = rated_power_W / (1000 * module_area_m2)
```

where `1000 W/m2` is the standard irradiance used for STC-style nameplate comparison.

## Area-derived module efficiency

| Product | Rated power | Dimensions | Area | Area-derived module efficiency | Public efficiency language |
|---|---:|---:|---:|---:|---|
| ZOUPW TC100W | 100 W | 853 x 578 mm | 0.493 m2 | 20.28 percent | 25 percent cell efficiency claim |
| CALLSUNSOLAR 100 W N-Type | 100 W | 790 x 578 mm | 0.457 m2 | 21.90 percent | 25 percent efficiency language |
| VXB 100 W N-Type | 100 W | 790 x 576 mm | 0.455 m2 | 21.98 percent | 25 percent efficiency language |
| TP-Link VIGI 100 W | 100 W | 1070 x 535 mm | 0.572 m2 | 17.47 percent | 22 percent conversion-efficiency language |
| BLUETTI SP100L | 100 W | 1132 x 595 mm | 0.674 m2 | 14.85 percent | up to 23.4 percent cell-efficiency language |

## Interpretation

A 100 W product can be physically plausible while still using ambiguous efficiency language.

Example:

```text
100 W / (1000 W/m2 * 0.493 m2) = 20.28 percent module efficiency
```

If the same product advertises 25 percent efficiency, the evidence-supported interpretation is usually:

```text
25 percent = cell efficiency or marketing shorthand
20.28 percent = area-derived framed-module efficiency
```

This is not necessarily a false claim. It is a claim-interpretation issue.

## Electrical consistency check

For products with available `Vmp` and `Imp`, calculate:

```text
Pcalc = Vmp * Imp
```

| Product | Vmp | Imp | Pcalc | Rated Pmax | Mismatch |
|---|---:|---:|---:|---:|---:|
| ZOUPW TC100W | 23.1 V | 4.33 A | 100.02 W | 100 W | 0.02 percent |
| CALLSUNSOLAR 100 W N-Type | 22.68 V | 4.41 A | 100.02 W | 100 W | 0.02 percent |

## Interpretation

The two products with complete max-power electrical values show internally consistent power ratings. A very small mismatch is expected from rounding.

A red flag would be:

```text
abs(Vmp * Imp - Pmax) / Pmax > 2 percent
```

That would suggest either specification error, marketing inconsistency, model mismatch, or transcription error.

## Fill-factor sanity check

For products with available `Voc` and `Isc`, calculate:

```text
FF = Pmax / (Voc * Isc)
```

| Product | Voc | Isc | Fill factor | Interpretation |
|---|---:|---:|---:|---|
| ZOUPW TC100W | 26.94 V | 4.51 A | 0.823 | plausible high-quality compact mono module |
| CALLSUNSOLAR 100 W N-Type | 26.02 V | 4.63 A | 0.830 | plausible high-quality compact mono module |

## Fill-factor interpretation bands

These are not certification limits. They are public-spec sanity bands.

| Fill factor | Interpretation |
|---:|---|
| below 0.60 | suspicious or low-quality for modern crystalline silicon module |
| 0.60 to 0.70 | weak or potentially high-loss design |
| 0.70 to 0.80 | plausible commodity module range |
| 0.80 to 0.84 | strong compact-module range |
| above 0.86 | verify carefully; may indicate specification mismatch or unusual assumptions |

## Thermal derating example

When a power temperature coefficient is available, estimate hot-condition output:

```text
P(T) = Pstc * (1 + gamma_P / 100 * (Tcell - 25))
```

CALLSUNSOLAR lists a Pmax temperature coefficient of approximately `-0.3 percent/K` in the reviewed product data.

For a 100 W panel at 65 C cell temperature:

```text
P(65 C) = 100 * (1 + (-0.3 / 100) * (65 - 25))
        = 88 W
```

This shows why a 100 W STC module may produce materially less than 100 W in hot real-world conditions before additional losses from:

- angle of incidence
- clouds or haze
- soiling
- wiring loss
- charge-controller loss
- battery voltage constraints
- mismatch
- partial shading

## Evidence maturity

| Product | Evidence maturity | Reason |
|---|---:|---|
| ZOUPW TC100W | EML-1 to EML-2 | public product data with detailed specs; primary manufacturer documentation still preferred |
| CALLSUNSOLAR 100 W N-Type | EML-1 to EML-2 | public product data with detailed specs; primary manufacturer documentation still preferred |
| VXB 100 W N-Type | EML-1 | partial public listing/specification data |
| TP-Link VIGI 100 W | EML-2 | manufacturer product page with dimensional and power data |
| BLUETTI SP100L | EML-1 to EML-2 | public product data with core specs; cell-vs-module efficiency distinction needed |

Evidence maturity levels:

| Level | Meaning |
|---:|---|
| EML-0 | marketing claim only |
| EML-1 | public retailer/product listing with partial specifications |
| EML-2 | manufacturer datasheet or manufacturer product page |
| EML-3 | datasheet plus warranty plus installation manual |
| EML-4 | datasheet plus certificates |
| EML-5 | public third-party reliability signal |
| EML-6 | customer-supplied sample test data |
| EML-7 | accredited lab report plus field data |

## Main findings

1. Compact 100 W N-type panels with framed-module efficiencies around 20 to 22 percent are physically plausible.
2. A public claim of 25 percent efficiency usually needs to be interpreted carefully.
3. If dimensions and rated power imply 20 to 22 percent module efficiency, then 25 percent likely refers to cell efficiency rather than full module efficiency.
4. `Vmp * Imp` is a fast internal-consistency check for public datasheets and listings.
5. `Pmax / (Voc * Isc)` is a fast fill-factor sanity check.
6. Hot-condition output can be substantially below STC nameplate rating.
7. Public product pages are useful for initial screening but insufficient for procurement-grade qualification without datasheets, warranty documents, certificates, and sample testing.

## Recommended verification package

For any candidate 100 W panel, request or perform:

| Verification item | Purpose |
|---|---|
| Manufacturer datasheet | verify electrical and mechanical specs |
| Product label photo | confirm model-specific values |
| Warranty document | confirm commercial obligations |
| Certificate file | verify regulatory claims and exact model number |
| IV curve measurement | validate output under known irradiance and temperature |
| Electroluminescence image | detect cracks and inactive cell regions |
| IR thermography under load | detect hot spots, diode heating, and resistive defects |
| Partial-shading test | evaluate bypass diode behavior |
| Temperature-coefficient test | validate hot-condition performance |

## Non-certification disclaimer

This benchmark is a public-spec engineering screen. It does not certify any module, verify field reliability, or replace accredited testing under IEC, UL, RETC, PVEL, NREL, TÜV, or equivalent procedures.
