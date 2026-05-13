# Verified 100 W Solar Panel Public-Spec Benchmark

## Report class

This is a **public-spec engineering dossier** for compact 100 W photovoltaic products. It demonstrates how to convert public product pages into a source-locked procurement screen.

This report does **not** certify any product. It does **not** prove field reliability. It does **not** replace IEC, UL, RETC, PVEL, NREL, TÜV, or equivalent accredited testing.

## Executive verdict

The public 100 W compact-panel market contains physically plausible products, but public efficiency language is often ambiguous. In the reviewed examples, headline claims such as `23.4 percent`, `25 percent`, or `22 percent conversion efficiency` are not always equivalent to gross framed-module efficiency calculated from rated power and physical area.

The strongest current rows for this demo are:

| Product | Confidence | Reason |
|---|---:|---|
| CALLSUNSOLAR 100 W N-Type | High for public-spec audit | Detailed electrical, mechanical, and thermal coefficient values were available from a public product page. |
| TP-Link VIGI 100 W | High for manufacturer-page audit | Manufacturer page provides rated power, dimensions, weight, conversion-efficiency language, weatherproofing, and operating range. |
| BLUETTI SP100L | Medium-high | Public product page gives core electrical/mechanical values, but it is a foldable portable panel and should not be directly compared to rigid framed modules without class adjustment. |
| ZOUPW 100 W | Provisional | Public data exists, but the exact model row must be locked to a specific source before use. |
| VXB 100 W | Provisional | Partial public data exists, but the row should remain provisional until a stable source is captured. |

## Central engineering question

Many listings advertise high cell efficiency. A due-diligence report must separate:

```text
cell efficiency
module efficiency
aperture efficiency
gross framed-area efficiency
real hot-field output
```

The core public-spec check is:

```text
module_efficiency_gross = rated_power_W / (1000 W/m2 * gross_area_m2)
```

This is a geometry/nameplate sanity check, not a certified STC measurement.

## Source register

| Source ID | Product | Source type | URL | Evidence grade | Notes |
|---|---|---|---|---:|---|
| SRC-CALLSUN-100W-N | CALLSUNSOLAR 100 W N-Type | Public product page | https://callsunsolar.com/products/100watt-solar-panel-n-type-16bb | EML-1/2 | Detailed values available; manufacturer datasheet/certificates still preferred. |
| SRC-TPLINK-VIGI-100W | TP-Link VIGI 100 W | Manufacturer product page | https://www.vigi.com/us/business-networking/vigi-solar-power-system/vigi-solar-panel-100w/ | EML-2 | Manufacturer-level product page. |
| SRC-BLUETTI-SP100L | BLUETTI SP100L | Public product page | https://www.bluettipower.com/products/foldable-solar-panel-sp100l | EML-1/2 | Portable/foldable class; compare separately from rigid framed modules. |
| SRC-ZOUPW-100W | ZOUPW 100 W | Public product page | https://zoupw.com/ja/products/100w-lightweight-solar-panel-portable | provisional | Exact model/spec row should be source-locked before final benchmark use. |
| SRC-VXB-100W | VXB 100 W | Public listing/product data | pending stable source capture | provisional | Keep out of final ranking until source is captured. |

## Evidence Maturity Level

| Level | Meaning |
|---:|---|
| EML-0 | marketing claim only |
| EML-1 | public retailer/product listing with partial specifications |
| EML-2 | manufacturer datasheet or manufacturer product page |
| EML-3 | datasheet plus warranty plus installation manual |
| EML-4 | datasheet plus certificates tied to exact model |
| EML-5 | public third-party reliability signal tied to exact model/BOM |
| EML-6 | customer-supplied sample test data |
| EML-7 | accredited lab report plus field data |

## Product-class segmentation

A stronger report should not compare all 100 W products as identical. Mechanical class matters.

| Product | Class | Interpretation consequence |
|---|---|---|
| CALLSUNSOLAR 100 W N-Type | rigid compact module | best suited for public-spec electrical sanity checks and module-efficiency comparison. |
| TP-Link VIGI 100 W | system/security solar panel | useful as a manufacturer-documented 100 W product, but optimized for a security-camera power ecosystem. |
| BLUETTI SP100L | portable foldable panel | lower gross deployed-area efficiency may be acceptable because portability is the design objective. |
| ZOUPW 100 W | lightweight/foldable or compact panel depending exact source | source-lock before direct ranking. |
| VXB 100 W | compact panel, provisional | source-lock before direct ranking. |

## Area-derived module efficiency

| Product | Rated power | Dimensions used | Gross area | Area-derived gross efficiency | Public efficiency language | Classification |
|---|---:|---:|---:|---:|---|---|
| CALLSUNSOLAR 100 W N-Type | 100 W | 790 x 578 mm | 0.457 m2 | 21.90 percent | 25 percent efficiency language | strong row |
| TP-Link VIGI 100 W | 100 W | 1070 x 535 mm | 0.572 m2 | 17.47 percent | 22 percent conversion-efficiency language | strong row |
| BLUETTI SP100L | 100 W | 1132 x 595 mm | 0.674 m2 | 14.85 percent | up to 23.4 percent cell-efficiency language | strong but foldable-class row |
| ZOUPW 100 W | 100 W | source-dependent | source-dependent | source-dependent | source-dependent | provisional |
| VXB 100 W | 100 W | source-dependent | source-dependent | source-dependent | source-dependent | provisional |

## Interpretation: cell efficiency vs gross module efficiency

A product can be physically plausible and still use efficiency language that requires interpretation.

Example using CALLSUNSOLAR-style dimensions:

```text
Area = 0.790 m * 0.578 m = 0.45662 m2
Gross module efficiency = 100 W / (1000 W/m2 * 0.45662 m2)
                        = 21.90 percent
```

If the product page also uses `25 percent` efficiency language, the safest engineering interpretation is:

```text
25 percent = likely cell-level or technology-level efficiency language
21.90 percent = gross framed-area nameplate efficiency
```

This is not automatically a false claim. It is a specification-interpretation risk.

## Electrical consistency audit

For products with available `Vmp` and `Imp`:

```text
Pcalc = Vmp * Imp
mismatch_percent = 100 * (Pcalc - Pmax) / Pmax
```

| Product | Vmp | Imp | Pcalc | Rated Pmax | Mismatch | Interpretation |
|---|---:|---:|---:|---:|---:|---|
| CALLSUNSOLAR 100 W N-Type | 22.68 V | 4.41 A | 100.02 W | 100 W | 0.02 percent | internally consistent |
| BLUETTI SP100L | unavailable in reviewed summary | unavailable | unavailable | 100 W | unavailable | request datasheet |
| TP-Link VIGI 100 W | listed voltage is not enough for full IV consistency | unavailable | unavailable | 100 W | unavailable | request datasheet |

A strong red flag would be:

```text
abs(Vmp * Imp - Pmax) / Pmax > 0.02
```

or a missing `Vmp/Imp` pair in a procurement context.

## Fill-factor sanity check

For products with available `Voc` and `Isc`:

```text
FF = Pmax / (Voc * Isc)
```

| Product | Voc | Isc | Fill factor | Interpretation |
|---|---:|---:|---:|---|
| CALLSUNSOLAR 100 W N-Type | 26.02 V | 4.63 A | 0.830 | plausible high-quality compact crystalline-silicon module |
| BLUETTI SP100L | 24.62 V | 5.13 A | 0.792 | plausible portable crystalline-silicon panel |
| TP-Link VIGI 100 W | unavailable in reviewed summary | unavailable | unavailable | request datasheet |

Fill-factor bands for public-spec sanity checking:

| Fill factor | Interpretation |
|---:|---|
| below 0.60 | suspicious or poor public-spec profile for modern crystalline silicon |
| 0.60 to 0.70 | weak or high-loss public-spec profile |
| 0.70 to 0.80 | plausible commodity range |
| 0.80 to 0.84 | strong compact-module range |
| above 0.86 | verify carefully; possible model mismatch or unusual assumptions |

## Thermal derating

When `gamma_P` is available:

```text
P(T) = Pstc * (1 + gamma_P / 100 * (Tcell - 25 C))
```

CALLSUNSOLAR public data included approximately:

```text
gamma_P = -0.3 percent/K
```

For a 100 W panel at 65 C cell temperature:

```text
P(65 C) = 100 * (1 + (-0.3 / 100) * (65 - 25))
        = 88 W
```

This is a nameplate-to-field-output correction. It does not include:

- angle-of-incidence loss
- soiling
- cable loss
- controller loss
- battery voltage mismatch
- partial shading
- cell mismatch
- aging/degradation

## Documentation-risk matrix

| Required document | Why it matters | Current benchmark status |
|---|---|---|
| manufacturer datasheet PDF | model-specific electrical and mechanical values | not consistently captured |
| warranty document | commercial obligation and degradation terms | not consistently captured |
| installation manual | safety, wiring, mounting, environment limits | not consistently captured |
| certificate file | exact model and standard traceability | not consistently captured |
| product label image | confirms exact SKU/model values | not consistently captured |
| temperature coefficient | hot-field output estimate | available for CALLSUNSOLAR row; not all rows |
| bypass diode count/layout | partial-shading behavior | not consistently captured |

## Standards mapping

| Public-spec check | Related formal concept | Limitation |
|---|---|---|
| `Vmp * Imp` consistency | IV-curve maximum power point | not a measured IEC 60904-1 IV curve |
| `Pmax / (Voc * Isc)` fill factor | diode/electrical quality indicator | depends on public values and STC assumptions |
| area-derived efficiency | nameplate vs geometry plausibility | gross area may differ from aperture area |
| thermal derating | temperature-coefficient performance | not a controlled temperature-coefficient test |
| warranty/documentation screen | procurement risk | not legal enforceability review |
| certification claim review | standards traceability | only valid if certificate number matches exact SKU/BOM |

## Reliability context

Public-spec plausibility is not reliability proof. A product can have coherent public electrical values and still fail under:

- thermal cycling
- damp heat
- UV exposure
- hail/mechanical loading
- hot-spot stress
- bypass-diode stress
- junction-box overheating
- delamination
- cell cracking
- solder/interconnect fatigue

For procurement-grade use, every candidate product should move from public-spec screening to sample-level testing.

## Recommended verification package

| Verification item | Purpose |
|---|---|
| controlled IV curve | validate `Pmax`, `Vmp`, `Imp`, `Voc`, `Isc`, and fill factor under measured irradiance/temperature |
| electroluminescence image | detect cracks, inactive cell regions, broken fingers, and solder/interconnect issues |
| IR thermography under load | identify hot spots, bypass diode heating, resistive joints, and cell mismatch |
| partial-shading test | evaluate bypass diode behavior and substring protection |
| insulation resistance screen | identify basic safety risk before deployment |
| wet leakage screen | outdoor sealing/safety risk indicator |
| temperature-coefficient measurement | validate hot-condition output estimate |
| documentation review | verify warranty, certifications, manuals, and exact SKU traceability |

## Red-team review

| Objection | Risk | Mitigation |
|---|---|---|
| Product pages can change. | source drift | archive screenshots or PDFs with access date. |
| Cell efficiency may be confused with module efficiency. | misleading interpretation | always compute gross area-derived efficiency. |
| Folded, unfolded, package, and module dimensions can be mixed. | wrong area calculation | record dimension type explicitly. |
| Retailer listing may differ from manufacturer datasheet. | model mismatch | prefer manufacturer datasheet and product label. |
| Same product name may have multiple revisions. | stale calculation | require model number and revision. |
| Certifications may not apply to exact SKU/BOM. | false compliance confidence | require certificate number and model list. |
| Public specs do not prove reliability. | overclaiming | require sample IV/EL/IR/environmental testing. |
| Rigid and foldable panels have different design objectives. | unfair ranking | classify products before comparison. |

## Final product-intelligence conclusion

The strongest public-spec claim for this benchmark is not which product is best. The strongest claim is methodological:

```text
A compact 100 W solar panel can be electrically plausible while its public efficiency language remains ambiguous.
```

For a serious buyer, the correct decision rule is:

```text
Use public specs to screen.
Use source-locked evidence to rank.
Use sample testing to qualify.
Use certificates and warranty files to approve procurement.
```

## Next report upgrade

The next version should add:

1. archived source captures for every row;
2. product label images where available;
3. stable manufacturer datasheet PDFs;
4. warranty files;
5. certificate traceability;
6. generated plots;
7. sample-test placeholders for IV, EL, and IR results.

## Non-certification disclaimer

This benchmark is a public-spec engineering screen. It does not certify any module, verify field reliability, or replace accredited testing under IEC, UL, RETC, PVEL, NREL, TÜV, or equivalent procedures.
