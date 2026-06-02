# FSL SAREF Audit — Round 2
**Date:** May 2026
**Authors:** Aman Karim, Shravan Balasubramanian
**Tool:** saref-pypeline v0.3.1
**Mode:** develop
**Branch:** saref-compatibility

---

## Summary

After adapting FSL with SAREF-required files and metadata,
saref-pypeline now completes a full run. This document records
all findings from Round 2, 3, and 4 of the pipeline.

---

## Progress Across Rounds

| Round | Errors | Key Change |
|---|---|---|
| Round 1 | Tool crashed | Naming incompatibility |
| Round 2 | 14 errors | First full run after basic fixes |
| Round 3 | 8 errors | Fixed CSV headers, schema prefix, dcterms |
| Round 4 | 8 errors | Fixed gitignore, added examples |

---

## Remaining Errors — Categorized

### Category A — ETSI-Specific (SKIP — not applicable to FSL)

These errors exist because saref-pypeline assumes all projects
are official ETSI/SAREF projects. FSL is an independent research
ontology and these requirements fundamentally do not apply.

| Error | Clause | Reason for Skip |
|---|---|---|
| LICENSE must say "Copyright YYYY ETSI" | 9.2 | FSL uses CC BY 4.0, not ETSI license |
| Must contain saref.etsi.org namespace | 9.4.2 | FSL has its own namespace |
| Ontology IRI must be saref.etsi.org/core/ | 9.4.3.1 | FSL has its own IRI |
| Publisher must be https://www.etsi.org/ | 9.4.3.2 | Publisher is University of Koblenz |
| License must be ETSI license | 9.4.3.2 | FSL uses CC BY 4.0 |
| Example must use saref.etsi.org IRI | 9.6.3 | FSL examples use own namespace |

**Count: 6 permanently unfixable errors**
**Reason: FSL is not an ETSI project**

---

### Category B — OWL2 DL Violations (FSL improvement opportunity)

These violations come from FSL using custom annotation properties
that are not formally declared as owl:AnnotationProperty in the
ontology. This is a legitimate quality improvement for FSL
independent of SAREF.

| Undeclared Property | What it is |
|---|---|
| tbox:commentingPolicy | FSL custom annotation |
| tbox:formattingPolicy | FSL custom annotation |
| tbox:linkingPolicy | FSL custom annotation |
| tbox:metamodelingPolicy | FSL custom annotation |
| dcterms:title | Dublin Core — should be declared |
| dcterms:description | Dublin Core — should be declared |
| dcterms:creator | Dublin Core — should be declared |
| dcterms:license | Dublin Core — should be declared |
| vann:preferredNamespacePrefix | VANN vocabulary |
| schema:Person | Schema.org class |
| schema:Organization | Schema.org class |

**Fix:** Add owl:AnnotationProperty declarations for all
tbox properties in tbox.ttl. Import schema.org and Dublin
Core ontologies properly.

---

### Category C — Warnings (Nice to have)

| Warning | Action |
|---|---|
| dcterms:title should have @en language tag | Small fix |
| vocabularies/ directory should exist | Not relevant for FSL |
| dcterms:abstract missing | Could add later |

---

## What FSL Added for SAREF Compatibility

| Item Added | Clause Addressed |
|---|---|
| LICENSE (CC BY 4.0) | 9.2 |
| ontology/ folder with saref.ttl | 9.4.1 |
| requirements/requirements.csv | 9.3 |
| tests/tests.csv | 9.5 |
| examples/python-example.ttl | 9.6 |
| documentation/abstract.md | 9.7 |
| documentation/description.md | 9.7 |
| owl:versionIRI | 9.4.3.1 |
| owl:versionInfo | 9.4.3.1 |
| dcterms:title | 9.4.3.2 |
| dcterms:description | 9.4.3.2 |
| dcterms:creator | 9.4.3.3 |
| dct:license | 9.4.3.2 |
| vann:preferredNamespacePrefix | 9.4.3.1 |

---

## Key Finding — SAREF Assumes ETSI Membership

The most important finding of this experiment is that
saref-pypeline was designed exclusively for ETSI SAREF projects.
Several core requirements are hardcoded to ETSI-specific values:

- The ontology IRI must be saref.etsi.org
- The publisher must be www.etsi.org
- The license must be the ETSI forge license
- The LICENSE file must credit ETSI

These requirements cannot be met by any non-ETSI ontology
without misrepresenting its ownership and licensing.

---

## Assessment Against Criteria

| Criteria | Score | Notes |
|---|---|---|
| Applicability to FSL | 4/10 | Many requirements are ETSI-specific |
| Effort to comply | Medium | 14 fixes needed, 6 impossible |
| Value of checks found | Medium | OWL2 DL violations are genuinely useful |
| Automation via GitHub Actions | High | Pipeline runs in under 10 seconds |
| Relevance for research ontology | Low-Medium | Designed for industry standards |

---

## Recommendation

SAREF-pypeline provides useful checks for ontology structure,
metadata completeness, and OWL2 DL compliance. However it
cannot be fully adopted for FSL because of hardcoded ETSI
assumptions.

**Recommended approach:**
1. Use the OWL2 DL violation checks as inspiration for FSL
2. Adopt the folder structure requirements (requirements, tests,
   examples, documentation) as FSL best practices
3. Do NOT require ETSI-specific metadata in FSL
4. Consider building a lightweight FSL-specific pipeline
   inspired by SAREF but without the ETSI constraints

