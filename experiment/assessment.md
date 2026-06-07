# SAREF for FSL — Systematic Assessment
**Date:** June 2026
**Authors:** Aman Karim, Shravan Balasubramanian
**Purpose:** Objectively assess how helpful SAREF is for FSL
at its current stage, as requested by Prof. Lämmel.

---

## Assessment Approach

Before running experiments we identified 5 assessment criteria
that would objectively determine whether SAREF is helpful for FSL.
Each criterion has a clear question, a measurement method, and
a scoring scale. Evidence is drawn from our pipeline experiments.

---

## Criterion 1 — Structural Applicability
**Question:** How many of SAREF Clause 9 structural requirements
genuinely apply to FSL as a research ontology?

**Why this matters:** If most requirements do not apply, adopting
SAREF creates unnecessary overhead without quality benefit.

**Measurement:** Count applicable vs non-applicable requirements
from the Clause 9 mapping (see SAREF_CLAUSE9_MAPPING.md).

**Evidence from experiments:**
- Total Clause 9 requirements checked: 45
- Already compliant: 9 (20%)
- Applicable with small fix: 28 (62%)
- Significant work needed: 5 (11%)
- Permanently not applicable (ETSI-specific): 10 (22%)

**Score: 35/45 = 78% of requirements applicable to FSL**

**Verdict:** HIGH applicability. Most structural and metadata
requirements make sense for FSL independently of SAREF.

---

## Criterion 2 — Genuine Quality Improvement
**Question:** Does running SAREF-pypeline reveal real quality
issues in FSL that are worth fixing regardless of SAREF compliance?

**Why this matters:** If SAREF only finds ETSI-specific issues,
it adds no value to FSL. If it finds real ontology quality problems,
it is valuable even if full compliance is impossible.

**Measurement:** Count errors that are genuine FSL quality issues
vs errors that are purely ETSI-specific and irrelevant to FSL.

**Evidence from experiments:**

| Issue Found | Genuine FSL Problem? |
|---|---|
| tbox annotation properties undeclared in OWL2 DL | ✅ Yes |
| Dublin Core terms used but not declared | ✅ Yes |
| schema.org terms used but not declared | ✅ Yes |
| Version metadata missing from all 8 ontologies | ✅ Yes |
| No requirements document | ✅ Yes |
| No examples folder | ✅ Yes |
| No documentation folder | ✅ Yes |
| LICENSE must say "Copyright ETSI" | ❌ ETSI-only |
| Publisher must be www.etsi.org | ❌ ETSI-only |
| IRI must be saref.etsi.org | ❌ ETSI-only |

**Score: 7 genuine FSL quality improvements identified**

**Verdict:** HIGH value. SAREF-pypeline found real problems in FSL
that are worth fixing independently of SAREF compliance.

---

## Criterion 3 — CI/CD Integration Feasibility
**Question:** Can SAREF-pypeline be integrated into FSL's GitHub
Actions CI/CD pipeline in a practical and sustainable way?

**Why this matters:** A tool that is too difficult to integrate
or maintain will not be adopted long-term regardless of its quality.

**Measurement:** Track number of workarounds needed, time to green
CI, and sustainability of the solution.

**Evidence from experiments:**

| Challenge | Workaround | Sustainable? |
|---|---|---|
| plyvel C++ dependency on Windows | Use Docker | ✅ Yes |
| Python 3.13+ requirement | Specify in workflow | ✅ Yes |
| Missing metadata file | Create in CI step | ✅ Yes |
| Project naming convention | Mount as /saref | ✅ Yes |
| LevelDB in GitHub Actions | Docker in CI | ✅ Yes |

- Iterations to green CI: 3
- Final CI run duration: under 10 minutes
- Maintenance burden: Low — Docker image self-contained

**Score: Achievable — 3 workarounds, all sustainable**

**Verdict:** MEDIUM-HIGH feasibility. Integration required effort
but the result is stable and maintainable.

---

## Criterion 4 — ETSI Barrier Severity
**Question:** What proportion of SAREF requirements are permanently
impossible for FSL to meet because of hardcoded ETSI assumptions?

**Why this matters:** If too many requirements cannot be met,
SAREF compliance becomes misleading and the tool loses credibility
as a quality framework for non-ETSI ontologies.

**Measurement:** Count permanently non-applicable requirements and
assess whether remaining errors after fixes are ETSI-specific.

**Evidence from experiments:**

| Mode | Total errors after fixes | ETSI-specific | Fixable for FSL |
|---|---|---|---|
| Develop | 8 | 8 (100%) | 0 |
| Release | 11 | 11 (100%) | 0 |

Permanently non-applicable requirements: 10 out of 45 (22%)
All remaining pipeline errors: 100% ETSI-specific

**Score: Significant barrier — 22% permanently blocked**

**Verdict:** SIGNIFICANT concern. Once ETSI-specific requirements
are excluded, no fixable errors remain — meaning the tool has
reached its useful limit for FSL.

---

## Criterion 5 — Long-term Adoption Value
**Question:** Should FSL adopt SAREF-pypeline as its primary
CI/CD quality tool on a permanent basis?

**Why this matters:** Adoption decisions should be based on
sustained value, not just initial findings.

**Measurement:** Weigh benefits against costs based on criteria 1-4.

**Benefits identified:**
- Inspired better folder structure for FSL ✅
- Identified 7 genuine quality improvements ✅
- Provided working GitHub Actions CI template ✅
- Introduced versioning and Dublin Core practices ✅
- Runs in under 10 minutes automatically ✅

**Costs identified:**
- Cannot achieve full compliance without misrepresenting FSL ❌
- 10 requirements permanently inapplicable ❌
- Requires Docker workaround for sustainability ❌
- Naming convention rejection needs permanent workaround ❌

**Score: Partial adoption recommended**

**Verdict:** Do not adopt as primary tool. Adopt the practices
it inspired. Build FSL-specific pipeline without ETSI constraints.

---

## Overall Assessment Summary

| Criterion | Score | Verdict |
|---|---|---|
| 1. Structural applicability | 78% applicable | ✅ High |
| 2. Genuine quality improvement | 7 real issues found | ✅ High value |
| 3. CI/CD integration feasibility | Achievable | ✅ Medium-High |
| 4. ETSI barrier severity | 22% permanently blocked | ⚠️ Significant |
| 5. Long-term adoption value | Partial only | ⚠️ Limited |

---

## Final Answer to the Research Question

**"How helpful is SAREF for FSL at its current stage?"**

SAREF is **genuinely helpful as an inspiration and diagnostic tool**
but **not suitable as FSL's primary CI/CD framework.**

The experiment reveals a fundamental tension: SAREF's engineering
practices (versioning, structured folders, metadata standards,
automated validation) are exactly what FSL needs. But the tool
implementing those practices is so tightly coupled to ETSI
membership that it cannot be honestly applied to an independent
research ontology.

**The practices are right. The tool assumptions are wrong.**

Concretely, this experiment has already improved FSL by:
- Adding version metadata to all 8 ontology files
- Establishing a requirements, tests, examples, and documentation
  structure that FSL previously lacked
- Identifying OWL2 DL violations in tbox.ttl worth fixing
- Providing a working GitHub Actions CI/CD pipeline

These improvements are permanent and valuable regardless of
whether SAREF is adopted long-term.

---

## Recommended Next Steps

1. Fix OWL2 DL violations — declare tbox properties properly
2. Add dcterms:modified, dcterms:issued, dcterms:abstract
3. Build FSL-specific validation pipeline without ETSI constraints
4. Evaluate OnToology as a complementary tool for non-ETSI ontologies
5. Use this Clause 9 mapping as a template for the FSL-specific
   quality checklist


---

## Addendum — Compliance Progress (from custom run_checks.py)

A custom Python compliance checker (run_checks.py) was written to
implement all applicable Clause 9 checks without ETSI constraints.
This gives granular per-clause PASS/FAIL/WARN results for FSL.

### Compliance Progress Table

| State | PASS | WARN | FAIL |
|---|---|---|---|
| FSL on main branch (original) | 14 | 2 | 21 |
| FSL after structural fixes | 28 | 2 | 12 |
| Full compliance (incl. metadata) | 46 | 1 | 0 |

### Specific Label Coverage

From automated term scan across all FSL modules (241 total terms):
- 19/241 terms missing rdfs:label@en (8%)
- 52/241 terms missing rdfs:comment@en (22%)

These are straightforward additions — no structural changes needed.

### What run_checks.py Covers

The custom checker implements Clauses 9.2, 9.3, 9.4.1, 9.4.2,
9.4.3.1, 9.4.3.2, 9.4.3.3, 9.4.4.1, 9.4.4.2, 9.4.5, 9.5,
9.6, 9.7, and 9.8 — all applicable requirements without
ETSI-specific constraints.

