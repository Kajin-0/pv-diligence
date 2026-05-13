# Demo Reports

This folder contains public-demo report formats for PV product intelligence and module due-diligence analysis.

The demo workflow is intentionally source-controlled:

1. Capture public evidence.
2. Record each extracted value in an evidence register.
3. Run deterministic physics checks.
4. Mark unresolved fields as pending.
5. Publish only claims that are traceable to a captured source.

## Verification rule

No product specification should be treated as verified unless it has:

- a source URL or archived source path,
- a source type,
- a date accessed,
- the extracted value,
- a confidence score,
- and a verification status.

## Demo subject

Initial demo subject:

```text
Infrienergy / Amazon-style 100 W solar panel product listing
User-provided URL: https://www.amazon.com/Solar-Panel/dp/B0GY7SZGJS
```

The current demo report is a structured public-evidence report shell. It does not assert unverified product specifications.

## Files

- `infrienergy-public-evidence-report.md` - GitHub-renderable demo report.
- `source-capture-checklist.md` - source capture protocol.
- `../../data/demo/infrienergy_evidence_register.csv` - evidence register template.
- `../../data/demo/infrienergy_specs_pending.csv` - specification table with pending fields.
