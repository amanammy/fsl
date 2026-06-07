# FSL SAREF Audit — Round 1
**Date:** May 2026
**Authors:** Aman Karim, Shravan Balasubramanian
**Tool:** saref-pypeline v0.3.1
**Mode:** develop
**FSL Version:** main branch as-is

---

## Summary

This document records the findings from running saref-pypeline 
against the FSL ontology in its current unmodified state.

---

## Finding 1 — Project Naming Convention

**SAREF Expects:**
Project names must be either:
- "core" for the main SAREF ontology
- A 4-letter acronym (e.g. ener, bldg, city)
- Something containing "saref" or "pattern"

**FSL Has:**
Project name is "fsl" — only 3 letters, does not follow SAREF convention.

**Error produced:**
ValueError: Illegal project name

**Category:** 🚨 Significant incompatibility

**Assessment:**
This is a fundamental assumption SAREF makes about all projects 
being part of the SAREF family. FSL is an independent research 
ontology and is not a SAREF extension. This naming requirement 
does not make sense to enforce on FSL.

---

## Finding 2 — Ontology Folder and File Naming

**SAREF Expects:**
- Folder named: ontology/
- Main file named: saref.ttl (for core) or saref4abcd.ttl (for extensions)

**FSL Has:**
- Folder named: ontologies/
- Main file named: fsl.ttl

**Error produced:**
Could not find a version for the project. 
No such file or directory: /saref/ontology/saref.ttl

**Category:** 🚨 Significant incompatibility

**Assessment:**
FSL uses plural "ontologies" and its own naming. Renaming would 
require changes throughout the codebase including catalog-v001.xml 
and all import statements.

---

## Finding 3 — Missing projects_metadata.yaml

**SAREF Expects:**
A file at target/sources/projects_metadata.yaml listing all 
project dependencies.

**FSL Has:**
No target/ folder at all.

**Error produced:**
FileNotFoundError: No such file or directory: 
/project/target/sources/projects_metadata.yaml

**Category:** 🔧 Small fix — easy to add

**Assessment:**
This file can be created with an empty projects list since FSL 
has no SAREF dependencies. Not a fundamental incompatibility.

---

## Finding 4 — Missing Required Folders

**SAREF Expects (Clause 9.2):**
- LICENSE
- README.md
- requirements/
- ontology/
- tests/
- examples/
- documentation/

**FSL Has:**
- README.md ✅
- ontologies/ (wrong name) ⚠️
- validation/ (not a SAREF requirement but good) ✅
- queries/ (not a SAREF requirement but good) ✅
- misc/ ✅

**Missing:**
- LICENSE ❌
- requirements/ ❌
- tests/ ❌
- examples/ ❌
- documentation/ ❌

**Category:** 🚨 Multiple missing items

---

## Finding 5 — Missing Ontology Metadata

**SAREF Expects (Clause 9.4.3):**
- owl:versionIRI
- owl:versionInfo
- dc:title
- dc:description
- dc:creator with schema:Person
- dct:license

**FSL Has:**
- rdfs:comment ✅
- tbox:commentingPolicy ✅ (FSL-specific — keep)
- tbox:formattingPolicy ✅ (FSL-specific — keep)
- tbox:linkingPolicy ✅ (FSL-specific — keep)
- tbox:metamodelingPolicy ✅ (FSL-specific — keep)
- owl:imports ✅

**Missing:**
- owl:versionIRI ❌
- owl:versionInfo ❌
- dc:title ❌
- dc:description ❌
- dc:creator ❌
- dct:license ❌

**Category:** 🔧 Small fixes — all can be added

---

## Finding 6 — FSL Has Things SAREF Does Not Expect

Interestingly FSL has things that SAREF does not account for:

| FSL Feature | What it is | SAREF equivalent |
|---|---|---|
| validation/ folder | SHACL shapes for FSL | SAREF has different validation approach |
| queries/ folder | SPARQL queries | Not in SAREF at all |
| tbox policies | Custom annotation properties | Not in SAREF at all |
| foaf:isPrimaryTopicOf | Wikipedia links | Not required by SAREF |
| catalog-v001.xml | OWL catalog for imports | Not in SAREF |

These are things FSL does that go beyond SAREF requirements.
This shows FSL has its own quality framework already.

---

## Round 1 Overall Assessment

| Category | Count |
|---|---|
| Fundamental incompatibilities | 2 |
| Missing required items | 7 |
| Small fixes needed | 4 |
| Already compliant | 3 |
| FSL has extra beyond SAREF | 5 |

### Key Conclusion from Round 1:
SAREF-pypeline cannot run on FSL in its current state because 
of fundamental naming assumptions. The tool was designed 
specifically for SAREF family projects and makes assumptions 
that do not apply to independent research ontologies like FSL.

---

## Next Steps — Round 2

Create a proper adapted branch of FSL that:
1. Addresses the naming issues
2. Adds the missing required files with real content
3. Adds the missing metadata to ontology files
4. Allows saref-pypeline to complete a full run

