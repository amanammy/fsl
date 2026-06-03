# FSL vs SAREF Clause 9 — Systematic Requirements Mapping
**Date:** June 2026
**Authors:** Aman Karim, Shravan Balasubramanian
**Purpose:** Map every SAREF Clause 9 requirement to FSL's current 
state as requested in the experiment specification (Step B).

**Categories used:**
- ✅ Compliant — FSL already meets this requirement
- 🔧 Small fix — Missing but easy to add
- 🚨 Significant work — Structurally incompatible or major effort
- ⛔ Not applicable — Requirement is ETSI-specific, cannot apply to FSL

---

## Clause 9.2 — Project Repository Structure

| Requirement | FSL State (main branch) | FSL State (saref-compatibility) | Category |
|---|---|---|---|
| README.md exists | ✅ Present | ✅ Present | ✅ Compliant |
| LICENSE file exists | ❌ Missing | ✅ Added CC BY 4.0 | 🔧 Small fix |
| LICENSE first line = "Copyright YYYY ETSI" | ❌ Missing | ❌ Cannot comply | ⛔ Not applicable |
| requirements/ folder exists | ❌ Missing | ✅ Added | 🔧 Small fix |
| ontology/ folder exists | ❌ Has /ontologies instead | ✅ Added ontology/ | 🔧 Small fix |
| tests/ folder exists | ❌ Missing | ✅ Added | 🔧 Small fix |
| examples/ folder exists | ❌ Missing | ✅ Added | 🔧 Small fix |
| documentation/ folder exists | ❌ Missing | ✅ Added | 🔧 Small fix |
| .gitignore includes target, *~ etc. | ❌ Incomplete | ✅ Updated | 🔧 Small fix |

**Clause 9.2 Summary:** 7 small fixes applied. 1 permanently not applicable (ETSI license format).

---

## Clause 9.3 — Requirements Specification

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| requirements/requirements.csv exists | ❌ Missing | ✅ Added | 🔧 Small fix |
| CSV header = "Id;Category;Requirement" | ❌ Missing | ✅ Correct header | 🔧 Small fix |
| File is UTF-8 encoded | ❌ Missing | ✅ UTF-8 | 🔧 Small fix |
| Requirements reflect actual ontology goals | ❌ Missing | ✅ 7 real FSL requirements | 🔧 Small fix |

**Clause 9.3 Summary:** All 4 requirements addressed with small fixes.

---

## Clause 9.4 — Ontology Document

### Clause 9.4.1 — File Format

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| Ontology in Turtle 1.1 format (.ttl) | ✅ Already uses Turtle | ✅ Already uses Turtle | ✅ Compliant |
| File named saref.ttl (for core) | ❌ Named fsl.ttl | ✅ ontology/saref.ttl added | 🚨 Significant work |

### Clause 9.4.2 — Namespace Declarations

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| Prefix schema = http://schema.org/ | ❌ Missing | ✅ Fixed (https → http) | 🔧 Small fix |
| Must contain saref.etsi.org namespace | ❌ Missing | ❌ Cannot comply | ⛔ Not applicable |

### Clause 9.4.3.1 — Ontology IRI and Version

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| owl:versionIRI present | ❌ Missing | ✅ Added to all 8 ontologies | 🔧 Small fix |
| owl:versionInfo present | ❌ Missing | ✅ Added to all 8 ontologies | 🔧 Small fix |
| Ontology IRI = saref.etsi.org/core/ | ❌ Missing | ❌ Cannot comply | ⛔ Not applicable |
| Naming convention (4-letter SAREF code) | ❌ fsl = 3 letters | ❌ Cannot comply | ⛔ Not applicable |
| owl:priorVersion if applicable | N/A (first version) | N/A (first version) | ✅ Compliant |

### Clause 9.4.3.2 — Ontology Metadata

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| dcterms:title | ❌ Missing | ✅ Added | 🔧 Small fix |
| dcterms:description | ❌ Missing | ✅ Added | 🔧 Small fix |
| dcterms:creator with schema:Person | ❌ Missing | ✅ Added | 🔧 Small fix |
| dcterms:license | ❌ Missing | ✅ Added CC BY 4.0 | 🔧 Small fix |
| dcterms:license = ETSI forge license | ❌ Missing | ❌ Cannot comply | ⛔ Not applicable |
| dcterms:publisher = www.etsi.org | ❌ Missing | ❌ Cannot comply | ⛔ Not applicable |
| dcterms:source = saref.etsi.org | ❌ Missing | ❌ Cannot comply | ⛔ Not applicable |
| dcterms:modified | ❌ Missing | ❌ Still missing | 🔧 Small fix |
| dcterms:issued | ❌ Missing | ❌ Still missing | 🔧 Small fix |
| dcterms:abstract | ❌ Missing | ❌ Still missing | 🔧 Small fix |
| vann:preferredNamespacePrefix | ❌ Missing | ✅ Added | 🔧 Small fix |
| vann:preferredNamespaceUri | ❌ Missing | ✅ Added | 🔧 Small fix |

### Clause 9.4.3.3 — Creator and Contributor

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| dcterms:creator with schema:Person | ❌ Missing | ✅ Added | 🔧 Small fix |
| schema:givenName and schema:familyName | ❌ Missing | ✅ Added | 🔧 Small fix |
| schema:Organization for affiliation | ❌ Missing | ✅ Added | 🔧 Small fix |

### Clause 9.4.4.1 — Naming Conventions

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| Classes start with capital letter | ✅ Already follows | ✅ Already follows | ✅ Compliant |
| Properties start with lowercase | ✅ Already follows | ✅ Already follows | ✅ Compliant |
| Namespace used for defined terms | ✅ Already follows | ✅ Already follows | ✅ Compliant |

### Clause 9.4.4.2 — Term Metadata (Labels and Comments)

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| rdfs:label on all classes | ✅ Present on most | ✅ Present on most | 🔧 Small fix |
| rdfs:comment on all classes | ✅ Present on most | ✅ Present on most | 🔧 Small fix |
| @en language tag on labels | ✅ Already uses @en | ✅ Already uses @en | ✅ Compliant |
| rdfs:label on all properties | ✅ Present on most | ✅ Present on most | 🔧 Small fix |
| rdfs:comment on all properties | ✅ Present on most | ✅ Present on most | 🔧 Small fix |

### Clause 9.4.5 — OWL2 DL Compliance

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| OWL2 DL profile satisfied | ❌ Violations found | ❌ Violations remain | 🚨 Significant work |
| tbox annotation properties declared | ❌ Undeclared | ❌ Still undeclared | 🚨 Significant work |
| Dublin Core terms declared | ❌ Undeclared | ❌ Still undeclared | 🚨 Significant work |
| schema.org terms declared | ❌ Undeclared | ❌ Still undeclared | 🚨 Significant work |
| Ontology is consistent | ✅ No contradictions | ✅ No contradictions | ✅ Compliant |
| All classes satisfiable | ✅ No unsatisfiable | ✅ No unsatisfiable | ✅ Compliant |

---

## Clause 9.5 — Tests Specification

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| tests/tests.csv exists | ❌ Missing | ✅ Added | 🔧 Small fix |
| CSV header = "Id;Requirement;Category;Test" | ❌ Missing | ✅ Correct header | 🔧 Small fix |
| Tests reflect ontology requirements | ❌ Missing | ✅ 4 real FSL tests | 🔧 Small fix |

**Clause 9.5 Summary:** All 3 requirements addressed with small fixes.

---

## Clause 9.6 — Examples

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| examples/ folder exists | ❌ Missing | ✅ Added | 🔧 Small fix |
| At least one example .ttl file | ❌ Missing | ✅ python-example.ttl | 🔧 Small fix |
| Examples are valid OWL2 DL | ❌ Missing | ❌ Violations remain | 🚨 Significant work |
| Example IRI = saref.etsi.org format | ❌ Missing | ❌ Cannot comply | ⛔ Not applicable |
| Example conforms to saref.etsi.org | ❌ Missing | ❌ Cannot comply | ⛔ Not applicable |

---

## Clause 9.7 — Documentation

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| documentation/ folder exists | ❌ Missing | ✅ Added | 🔧 Small fix |
| Abstract provided | ❌ Missing | ✅ abstract.md added | 🔧 Small fix |
| Description provided | ❌ Missing | ✅ description.md added | 🔧 Small fix |
| Diagrams in documentation/diagrams/ | ❌ Missing | ❌ Still missing | 🔧 Small fix |

---

## Clause 9.8 — Vocabularies (Optional)

| Requirement | FSL State (main) | FSL State (branch) | Category |
|---|---|---|---|
| vocabularies/ folder (optional) | ❌ Missing | ❌ Missing | 🔧 Small fix (optional) |

**Clause 9.8 Note:** This is optional for SAREF and not relevant for FSL's purpose.

---

## Overall Summary

| Category | Count | Percentage |
|---|---|---|
| ✅ Already Compliant | 9 | 20% |
| 🔧 Small fix applied | 22 | 49% |
| 🔧 Small fix still needed | 6 | 13% |
| 🚨 Significant work needed | 5 | 11% |
| ⛔ Not applicable (ETSI-specific) | 10 | 22% |

**Total requirements checked: 45**

---

## Key Insight from This Mapping

Of the 10 permanently not-applicable requirements, ALL are 
ETSI membership requirements — license, publisher, IRI format, 
naming convention, source URL. These are hardcoded into 
saref-pypeline and cannot be met by any non-ETSI ontology.

Of the 5 significant work items, ALL relate to OWL2 DL 
compliance — specifically undeclared annotation properties 
from tbox.ttl, Dublin Core, and schema.org. These are genuine 
FSL quality issues worth fixing independently of SAREF.

The 6 remaining small fixes (dcterms:modified, dcterms:issued, 
dcterms:abstract, diagrams, labels verification, example OWL2 DL) 
are straightforward additions for future milestones.

