# PV Product Intelligence Demo Report

## Subject

Target listing supplied by user:

- Amazon ASIN: B0GY7SZGJS
- User URL: https://www.amazon.com/Solar-Panel/dp/B0GY7SZGJS
- Target brand reference: Infrienergy

## Verification status

This report is source-locked. The target Infrienergy/Amazon listing could not be verified from indexed public search results at the time this demo was prepared. Therefore, no Infrienergy-specific electrical or dimensional values are asserted as verified in this report.

Instead, this demo uses verified public comparable products in the same market class:

- 100 W N-type solar panels
- 25 percent cell-efficiency claims
- RV, marine, rooftop, and off-grid positioning
- compact framed monocrystalline modules

## Why this demo is useful

The public market contains many 100 W solar panels advertising high cell efficiency. The key engineering question is whether the advertised efficiency is cell efficiency or full module efficiency.

The central calculation is:

```text
module_efficiency = rated_power_W / (1000 * module_area_m2)
```

A 100 W module with 0.45 to 0.50 square meters of area has a module efficiency near 20 to 22 percent. A claim of 25 percent is not automatically false, but it often refers to cell efficiency rather than full framed-module efficiency.

## Evidence table

| ID | Product | Source type | Verified fields used | Status |
|---|---|---|---|---|
| E01 | Infrienergy / Amazon B0GY7SZGJS | user-supplied listing URL | ASIN only | pending source capture |
| E02 | ZOUPW TC100W 100 W N-type panel | product page | Pmax, Vmp, Imp, Voc, Isc, dimensions, weight, cell efficiency claim | verified public comparable |
| E03 | CALLSUNSOLAR 100 W N-type panel | product page | Pmax, Vmp, Imp, Voc, Isc, dimensions, weight, temperature coefficient, load rating | verified public comparable |
| E04 | VXB 100 W N-type panel | product page | Pmax, dimensions, weight, cell efficiency claim | verified public comparable |
| E05 | TP-Link VIGI 100 W panel | manufacturer page | Pmax, dimensions, weight, conversion efficiency claim | verified public comparable |
| E06 | BLUETTI SP100L 100 W panel | product page | Pmax, Voc, Isc, dimensions, weight, cell efficiency claim | verified public comparable |

## Deterministic checks

### Area-derived module efficiency

| Product | Rated power | Dimensions | Area | Area-derived module efficiency | Public efficiency claim type |
|---|---:|---:|---:|---:|---|
| ZOUPW TC100W | 100 W | 853 x 578 mm | 0.493 m2 | 20.28 percent | cell efficiency: 25 percent |
| CALLSUNSOLAR 100 W | 100 W | 790 x 578 mm | 0.457 m2 | 21.90 percent | efficiency listed: 25 percent |
| VXB 100 W | 100 W | 790 x 576 mm | 0.455 m2 | 21.98 percent | efficiency listed: 25 percent |
| TP-Link VIGI 100 W | 100 W | 1070 x 535 mm | 0.572 m2 | 17.47 percent | conversion efficiency: 22 percent |
| BLUETTI SP100L | 100 W | 1132 x 595 mm | 0.674 m2 | 14.85 percent | cell efficiency: up to 23.4 percent |

### Electrical consistency checks

For products with Vmp and Imp:

```text
Pcalc = Vmp * Imp
```

| Product | Vmp | Imp | Pcalc | Rated Pmax | Mismatch |
|---|---:|---:|---:|---:|---:|
| ZOUPW TC100W | 23.1 V | 4.33 A | 100.02 W | 100 W | 0.02 percent |
| CALLSUNSOLAR 100 W | 22.68 V | 4.41 A | 100.02 W | 100 W | 0.02 percent |

### Fill factor checks

```text
FF = Pmax / (Voc * Isc)
```

| Product | Voc | Isc | Fill factor | Interpretation |
|---|---:|---:|---:|---|
| ZOUPW TC100W | 26.94 V | 4.51 A | 0.823 | plausible high-quality compact mono module |
| CALLSUNSOLAR 100 W | 26.02 V | 4.63 A | 0.830 | plausible high-quality compact mono module |

## Thermal derating example

CALLSUNSOLAR lists a Pmax temperature coefficient of -0.3 percent per K. For a 100 W module at 65 C cell temperature:

```text
P(65 C) = 100 * (1 + (-0.3 / 100) * (65 - 25)) = 88 W
```

This illustrates the difference between STC rating and hot-field output. A 100 W panel can be technically valid while producing roughly 88 W at elevated cell temperature before angle, soiling, wiring, controller, and battery losses.

## Key finding

The main issue is not that 100 W compact N-type modules are physically impossible. The issue is claim interpretation.

For compact 100 W panels, area-derived module efficiencies around 20 to 22 percent are physically plausible. Public claims of 25 percent usually need to be interpreted carefully because they may refer to cell efficiency rather than full framed-module efficiency.

## Infrienergy target listing status

The supplied Infrienergy/Amazon target is not yet source-verified in this report. To complete the report, capture the following from the actual listing or product label:

- rated power
- dimensions
- weight
- Vmp
- Imp
- Voc
- Isc
- cell type
- claimed efficiency
- temperature coefficient
- warranty language
- certification claims
- junction box rating
- connector type
- bypass diode count if listed

Once those values are captured, the same calculations above can be run against the Infrienergy product directly.

## Recommended final demo structure

A strong public GitHub demo should present:

1. the unverified target listing as pending evidence;
2. verified comparable public examples;
3. deterministic calculations;
4. no unsupported claims;
5. a clear method for converting a public listing into a traceable product intelligence report.

## Non-certification disclaimer

This report is a public-evidence engineering screen. It is not a certification report and does not replace IEC, UL, RETC, PVEL, NREL, TÜV, or other accredited test-lab measurements.
