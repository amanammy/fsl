# FSL SAREF Experiment — Final Report
**Date:** June 2026
**Authors:** Aman Karim, Shravan Balasubramanian
**Branch:** saref-compatibility
**Tool:** saref-pypeline v0.3.1

---

## 1. Objective

Investigate whether SAREF-pypeline can be applied to the FSL
ontology as a CI/CD quality framework. Assess how helpful
SAREF is for FSL and recommend whether to adopt it long-term.

---

## 2. What We Did

### Phase 1 — Tool Setup
- Installed saref-pypeline via Docker due to Windows/Python 3.14
  incompatibility with plyvel-wheels dependency
- Successfully tested tool on saref-core reference ontology
- saref-core produced only INFO and WARNING messages — zero errors
- Confirmed tool works correctly before applying to FSL

### Phase 2 — FSL Audit Round 1
- Ran saref-pypeline on FSL as-is
- Tool crashed immediately with "Illegal project name"
- Root cause: SAREF only accepts project names following SAREF
  naming conventions (4-letter acronym or "saref"/"core")
- FSL name "fsl" is only 3 letters — hardcoded rejection
- Additional crash: missing projects_metadata.yaml file

### Phase 3 — FSL Adaptation
Added the following to make FSL SAREF-compatible:
- LICENSE file (CC BY 4.0)
- ontology/ folder with saref.ttl (copy of fsl.ttl)
- requirements/requirements.csv with real FSL requirements
- tests/tests.csv with real FSL test descriptions
- examples/python-example.ttl with real usage example
- documentation/abstract.md and description.md
- owl:versionIRI and owl:versionInfo metadata
- dcterms:title, description, creator, license metadata
- vann:preferredNamespacePrefix and Uri

### Phase 4 — Pipeline Runs
Ran saref-pypeline multiple times and fixed issues iteratively:

| Round | Errors | Key Action |
|---|---|---|
| Round 1 | Crashed | Naming incompatibility discovered |
| Round 2 | 14 errors | First full run after basic structure added |
| Round 3 | 8 errors | Fixed CSV headers, schema prefix, dcterms |
| Round 4 | 8 errors | Fixed gitignore, added real examples |

### Phase 5 — GitHub Actions CI
- Created GitHub Actions workflow
- Fixed Python version incompatibility (needed 3.13+)
- Fixed LevelDB dependency by using Docker in CI
- Achieved green CI run — pipeline now runs automatically
  on every push to saref-compatibility and main branches

---

## 3. Key Findings

### Finding 1 — Naming Convention Incompatibility
SAREF hardcodes project naming to SAREF family conventions.
Any non-SAREF ontology will fail before any real checks run.
This is a fundamental barrier for independent ontologies.

### Finding 2 — ETSI-Specific Requirements Cannot Be Met
6 errors cannot be fixed without misrepresenting FSL:
- LICENSE must credit ETSI
- Ontology IRI must be saref.etsi.org
- Publisher must be www.etsi.org
- License must be ETSI forge license

These requirements assume the ontology is an ETSI standard.
FSL is a research ontology — these do not apply.

### Finding 3 — OWL2 DL Violations Are Genuinely Useful
The pipeline identified real FSL quality issues:
- FSL's tbox custom annotation properties are undeclared
- Dublin Core terms used without proper declarations
- These are legitimate improvements FSL should make
  independent of SAREF

### Finding 4 — Folder Structure Requirements Are Valuable
SAREF's requirement for requirements/, tests/, examples/,
and documentation/ folders is good practice for any ontology.
FSL benefited from adding these even outside SAREF context.

### Finding 5 — GitHub Actions Integration Works Well
Once Docker was used to handle the LevelDB dependency,
the CI pipeline runs cleanly in under 10 minutes on GitHub.
This validates the CI/CD approach for ontology engineering.

---

## 4. Assessment Against Criteria

| Criteria | Score | Notes |
|---|---|---|
| Applicability to FSL | 4/10 | 6 requirements permanently inapplicable |
| Effort to comply | Medium | Significant restructuring needed |
| Value of checks | 6/10 | OWL2 DL and structure checks are useful |
| CI automation | 9/10 | Works well via Docker on GitHub Actions |
| Relevance for research | 5/10 | Designed for industry standards body |

---

## 5. Recommendation

SAREF-pypeline cannot be fully adopted for FSL because of
hardcoded ETSI assumptions. However the experiment was
valuable because:

1. The OWL2 DL violation checks revealed real FSL quality
   issues worth fixing
2. The folder structure (requirements, tests, examples,
   documentation) is good practice FSL should keep
3. The GitHub Actions CI workflow works and can be reused
   for other FSL quality checks

**Recommended next steps:**
- Keep the folder structure additions on the saref-compatibility
  branch as permanent FSL improvements
- Fix the OWL2 DL violations in tbox.ttl independently
- Build a lightweight FSL-specific CI pipeline inspired by
  SAREF but without ETSI constraints
- Consider OnToology as a complementary tool that may be
  more suitable for non-ETSI ontologies

---

## 6. Links

- Fork: https://github.com/amanammy/fsl
- Branch: saref-compatibility
- GitHub Actions: https://github.com/amanammy/fsl/actions
- Round 1 Audit: SAREF_AUDIT_ROUND1.md
- Round 2 Audit: SAREF_AUDIT_ROUND2.md

