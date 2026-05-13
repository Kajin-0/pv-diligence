# PV Diligence

`pv-diligence` is a local, evidence-controlled report generator for photovoltaic module due-diligence analysis.

The tool ingests module specification tables and an evidence ledger, performs deterministic PV physics checks, generates red flags, scores technical risk, and produces Markdown/HTML reports with reproducible calculations.

## What it does

- Calculates module area, W/m², module efficiency, fill factor, datasheet power mismatch, price/W, W/kg, and hot-temperature derating.
- Flags common claim problems such as cell-efficiency vs module-efficiency ambiguity.
- Scores modules using claim, electrical, thermal, warranty, and documentation-risk components.
- Generates a ranked technical scorecard.
- Generates Markdown and HTML reports.
- Produces plots for score, module efficiency, power density, and 65 °C derated power.
- Supports an evidence ledger so every value can be traced to a source.
- Includes prompt templates for optional AI agents: source discovery, extraction, conflict detection, and red-team review.

## What it does not do

- It does not certify PV modules.
- It does not replace IEC 60904, IEC 61215, IEC 61730, UL, PVEL, RETC, TÜV, NREL, or accredited-lab testing.
- It does not guarantee that public claims are true.
- It does not infer hidden BOM-specific reliability.

## Install

```bash
python -m venv .venv
source .venv/bin/activate
pip install -e .
```

On Windows PowerShell:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
pip install -e .
```

## Run demo analysis

```bash
pvdiligence analyze \
  --modules data/modules.demo.csv \
  --sources data/sources.demo.csv \
  --evidence data/evidence_ledger.demo.csv \
  --out outputs
```

Outputs:

```text
outputs/scorecard.csv
outputs/report.md
outputs/report.html
outputs/plots/*.png
outputs/prompts/*.txt
```

## Input data

Use `data/modules.template.csv` for real projects.

Minimum required columns:

```text
manufacturer,model,category,price_usd,rated_power_W,length_mm,width_mm,weight_kg,Voc_V,Isc_A,Vmp_V,Imp_A,temp_coeff_P_pct_C,warranty_product_yr,warranty_performance_yr,claimed_efficiency_pct,listed_module_efficiency_pct,source_id
```

The demo dataset is synthetic but physically plausible. Replace it with public datasheet/listing values before publishing any external benchmark.

## Key calculations

Module area:

```text
A = length_m * width_m
```

Module efficiency:

```text
eta_module = P_rated / (1000 * A)
```

Power density:

```text
W_per_m2 = P_rated / A
```

Fill factor:

```text
FF = P_rated / (Voc * Isc)
```

Datasheet consistency:

```text
P_calc = Vmp * Imp
Delta_P_pct = 100 * (P_calc - P_rated) / P_rated
```

Thermal derating:

```text
P(T) = P_rated * (1 + gamma_P_pct_C / 100 * (T_cell_C - 25))
```

## Evidence Maturity Level

| Level | Meaning |
|---:|---|
| EML-0 | Marketing claim only or synthetic demo data |
| EML-1 | Retailer listing with partial specifications |
| EML-2 | Manufacturer datasheet available |
| EML-3 | Datasheet + warranty + installation manual |
| EML-4 | Datasheet + certificates |
| EML-5 | Public third-party reliability signal |
| EML-6 | Customer-supplied sample test data |
| EML-7 | Accredited lab report + field data |

## Score components

The v1 technical score is:

```text
S_total = 0.25*S_claim + 0.20*S_electrical + 0.20*S_thermal + 0.15*S_warranty + 0.20*S_data
```

| Component | Meaning |
|---|---|
| S_claim | physical plausibility of public claims |
| S_electrical | datasheet internal consistency |
| S_thermal | hot-condition output retention |
| S_warranty | product and performance warranty strength |
| S_data | completeness of public documentation |

## Verdict bands

| Score | Verdict |
|---:|---|
| 85-100 | strong candidate |
| 70-84 | acceptable with verification |
| 55-69 | caution |
| 40-54 | high risk |
| <40 | reject or insufficient evidence |

## Agent workflow

Optional AI agents should operate around the deterministic core:

1. Source Discovery Agent
2. Datasheet Extraction Agent
3. Evidence Conflict Agent
4. Red-Team Review Agent
5. Report Drafting Agent

The calculations in `pvdiligence/calculations.py` are deterministic and should remain non-generative.

## License

Proprietary starter code by default. Add an open-source license only if you intend to publish it publicly.
