# PV Diligence

PV Diligence is an MVP for AI-assisted, evidence-controlled photovoltaic module procurement due diligence.

It is designed to produce a traceable technical report from public module data, deterministic PV calculations, and structured risk scoring.

## What this is

This is a public-data PV module due-diligence workflow for:

- procurement screening
- solar panel claim audits
- datasheet consistency checks
- module efficiency sanity checks
- thermal derating analysis
- documentation and evidence maturity scoring
- pre-certification risk review

## What this is not

This is not an IEC, UL, RETC, PVEL, or NREL certification report. It does not replace accredited testing.

It is an engineering due-diligence layer intended to identify claim ambiguity, weak documentation, physically inconsistent specs, thermal risk, missing data, and procurement red flags before a buyer spends money on samples, certification, inventory, or private-label product launch.

## Core thesis

Anyone can ask an LLM to compare solar panels.

This tool makes the process harder to fake by combining:

1. source-tracked evidence
2. deterministic PV calculations
3. evidence maturity scoring
4. red-flag logic
5. reproducible report generation
6. agent prompts for source discovery, extraction, conflict review, and red-team critique

## Install

```bash
python -m venv .venv
source .venv/bin/activate
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
outputs/report.md
outputs/report.html
outputs/scorecard.csv
outputs/plots/
outputs/prompts/
```

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
| EML-0 | Marketing claim only |
| EML-1 | Retailer listing with partial specifications |
| EML-2 | Manufacturer datasheet available |
| EML-3 | Datasheet + warranty + installation manual |
| EML-4 | Datasheet + certificates |
| EML-5 | Public third-party reliability signal |
| EML-6 | Customer-supplied sample test data |
| EML-7 | Accredited lab report + field data |

## Score components

The v1 procurement score is:

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

## Suggested commercial offer

### $1,500 Public Supplier Screen

- 3 candidate modules
- public evidence only
- datasheet audit
- thermal derating
- warranty/documentation review
- procurement recommendation

### $3,500-$5,000 Procurement Risk Report

- 5-8 modules
- evidence ledger
- conflict detection
- red-team review
- energy-yield modeling extension
- recommended verification test matrix

### $7,500+ Private-Label Launch Risk Review

- product claim audit
- supplier comparison
- warranty risk review
- datasheet cleanup
- marketing-claim correction
- test plan before inventory/certification spend

## Demo data warning

The included demo data is synthetic and for workflow demonstration only. Replace it with real public module datasheets before publishing a public benchmark.
