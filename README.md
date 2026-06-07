# FSL — Foundations of Software Languages

This is a fork of [softlang/fsl](https://github.com/softlang/fsl) created as part of the SLE meets AI research lab at the University of Koblenz under Prof. Ralf Lämmel.

## Branch: saref-compatibility

This branch contains my work on investigating whether the SAREF-pypeline CI/CD framework can be applied to FSL. The short answer is: the engineering practices SAREF promotes are genuinely useful for FSL, but the tool itself cannot be directly adopted because it was built for ETSI standards body projects.

## What I added

- `LICENSE` — CC BY 4.0
- `ontology/` — SAREF-compatible copy of the main ontology
- `requirements/` — FSL requirements in SAREF format
- `tests/` — FSL test specifications
- `examples/` — example usage of FSL
- `documentation/` — abstract and description
- `.github/workflows/` — GitHub Actions CI that runs on every push and PR
- `experiment/` — all findings, audit documents, and assessment

## Experiment documents

- `experiment/round1-findings.md` — what happened when we ran the tool on FSL as-is
- `experiment/round2-findings.md` — findings after adapting FSL
- `experiment/clause9-mapping.md` — every SAREF Clause 9 requirement mapped to FSL
- `experiment/assessment.md` — objective assessment of whether SAREF helps FSL
- `experiment/report.md` — full experiment report

## Authors

Aman Karim, Shravan Balasubramanian
