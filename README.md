# Academic Research Publication Ontology (ARPO)

> Knowledge Engineering and Ontologies — Course Project
> Phase 2 · May 2026

## Overview

**ARPO** is an OWL 2 DL ontology that formally represents the domain of academic research publications. It models publications, authors, institutions, venues, citation relationships, funding, open access status, and research topics — enabling semantic search, bibliometric reasoning, and cross-database knowledge integration.

---

## Version History

| Version | Date | Summary |
|---------|------|---------|
| v1.0 | April 25, 2026 | Initial ontology: 19 classes, 13 object properties, 15 data properties. Core publication, author, venue, and citation modelling. |
| v2.0 | May 5, 2026 | Phase 2 extension: 7 new classes, 7 new object properties, 4 new data properties. Added funding module, open access status, peer review record, affiliation record (MOMo record pattern), and LLM population integration plan. |

---

## Repository Structure

```
arpo-ontology/
├── arpo.ttl              # Main ontology file — OWL 2 DL, Turtle syntax (v2.0)
├── ARPO-ORSD-P1.docx     # Ontology Requirements Specification Document — Phase 1 (v1.0)
├── ARPO-ORSD-P2.docx     # Ontology Requirements Specification Document — Phase 2 (v2.0)
└── README.md             # This file
```

---

## Domain

Academic research publishing — the full lifecycle of a scholarly work, from the authors and institutions who produce it, to the venues where it is published, to the citation networks that connect it to other work, and the funding bodies that support it.

**In Scope:** Journal articles, conference papers, book chapters, theses, technical reports, preprints · Authors, researchers, reviewers · Universities, research institutes, companies, research groups · Journals, conferences, workshops · Bibliographic metadata (title, abstract, DOI, year, volume, issue, pages) · Citation and co-authorship relationships · Research topics and keywords · Funding information (grants, funding bodies) · Open access status

**Out of Scope:** Patents, grey literature, social media posts · Full-text content of publications · Non-academic publishing

---

## Classes

### v1.0 Classes

| Class | Description |
|-------|-------------|
| `Publication` | Top-level class for all academic research outputs |
| `JournalArticle` | Peer-reviewed article published in a journal |
| `ConferencePaper` | Paper presented at an academic conference |
| `BookChapter` | Chapter within an edited academic book |
| `Thesis` | Doctoral or master's dissertation |
| `TechnicalReport` | Institutional technical report |
| `Person` | A human being involved in academic research |
| `Researcher` | A person who conducts academic research |
| `Author` | Researcher who has authored publications |
| `Reviewer` | Researcher who peer-reviews manuscripts |
| `Institution` | Organisation with which researchers may be affiliated |
| `University` | Higher-education institution |
| `ResearchInstitute` | Dedicated research organisation |
| `Company` | Industrial organisation engaged in research |
| `PublicationVenue` | Channel where research is formally published |
| `Journal` | Periodical publication venue |
| `Conference` | Academic event venue |
| `Workshop` | Smaller event co-located with a conference |
| `ResearchTopic` | Thematic subject area |
| `Keyword` | Descriptor term for a publication |
| `Citation` | A formal reference between two publications |
| `Publisher` | Organisation that distributes publications |

### v2.0 New Classes

| Class | Description |
|-------|-------------|
| `Preprint` | Pre-peer-review version deposited on a preprint server (e.g. arXiv) |
| `ResearchGroup` | Named lab or group within a university or institute — MOMo membership pattern |
| `Grant` | A funded research grant associated with one or more publications |
| `FundingBody` | Organisation that provides research funding (e.g. NSF, EU Horizon) |
| `OpenAccessStatus` | OA category of a publication — MOMo controlled-vocabulary pattern |
| `PeerReviewRecord` | Record of a publication's peer-review status — MOMo provenance pattern |
| `AffiliationRecord` | Time-bounded affiliation link between Author and Institution — MOMo record pattern |

---

## Object Properties

### v1.0 Object Properties

| Property | Domain → Range | Notes |
|----------|---------------|-------|
| `hasAuthor` / `isAuthorOf` | Publication ↔ Author | Inverse pair |
| `hasCoAuthor` | Author ↔ Author | Symmetric |
| `isAffiliatedWith` / `hasAffiliation` | Researcher ↔ Institution | Inverse pair |
| `publishedIn` | Publication → Venue | |
| `publishedBy` | Publication → Publisher | |
| `cites` / `isCitedBy` | Publication ↔ Publication | Inverse pair; `cites` is irreflexive |
| `hasResearchTopic` | Publication → ResearchTopic | |
| `hasKeyword` | Publication → Keyword | |
| `representsArea` | Keyword → ResearchTopic | |

### v2.0 New Object Properties

| Property | Domain → Range | Notes |
|----------|---------------|-------|
| `hasAffiliationRecord` | Author → AffiliationRecord | MOMo record pattern |
| `affiliatedInstitution` | AffiliationRecord → Institution | MOMo record pattern |
| `hasFunding` | Publication → Grant | |
| `fundedBy` | Grant → FundingBody | |
| `hasOpenAccessStatus` | Publication → OpenAccessStatus | Functional |
| `hasPeerReviewRecord` | Publication → PeerReviewRecord | Functional |
| `memberOf` | Author → ResearchGroup | MOMo membership pattern |

---

## Data Properties

### v1.0 Data Properties

| Property | Domain | Range |
|----------|--------|-------|
| `hasTitle` | Publication | xsd:string |
| `hasAbstract` | Publication | xsd:string |
| `hasYear` | Publication | xsd:integer |
| `hasDOI` | Publication | xsd:string |
| `hasVolume` | JournalArticle | xsd:string |
| `hasIssue` | JournalArticle | xsd:string |
| `hasPageStart` | Publication | xsd:integer |
| `hasPageEnd` | Publication | xsd:integer |
| `hasCitationCount` | Publication | xsd:integer |
| `hasISSN` | Journal | xsd:string |
| `hasImpactFactor` | Journal | xsd:decimal |
| `hasName` | Person | xsd:string |
| `hasORCID` | Researcher | xsd:string |
| `hasLabel` | Keyword | xsd:string |
| `hasTopicName` | ResearchTopic | xsd:string |

### v2.0 New Data Properties

| Property | Domain | Range |
|----------|--------|-------|
| `hasStartYear` | AffiliationRecord | xsd:integer |
| `hasEndYear` | AffiliationRecord | xsd:integer |
| `hasGrantNumber` | Grant | xsd:string |
| `hasAccessType` | OpenAccessStatus | xsd:string |

---

## Ontology Details

| Item | Value |
|------|-------|
| Namespace | `https://example.org/arpo#` |
| Prefix | `arpo:` |
| OWL Profile | OWL 2 DL |
| Serialisation | Turtle (`.ttl`) |
| Current Version | 2.0 |
| Reasoner compatibility | HermiT, Pellet |
| Modelling methodology | Modular Ontology Modeling (MOMo) |
| Licence | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |

---

## Competency Questions

### Phase 1 (CQ1–CQ12)
1. What papers has a given author published?
2. Which papers cite a given publication?
3. In which venue was a specific paper published?
4. What research topics are covered by a specific paper?
5. Which authors are affiliated with a given institution?
6. What papers were published within a given date range?
7. Which papers are co-authored by researchers from two or more institutions?
8. How many times has a given paper been cited?
9. Which researchers have collaborated with a given author?
10. What is the ISSN or impact factor of a given journal?
11. Which papers belong to a given research topic?
12. What is the full list of authors of a given paper, in order?

### Phase 2 (CQ13–CQ15)
13. Which publications are openly accessible (gold or green open access)?
14. Which grants funded a given publication?
15. During which years was a given author affiliated with a given institution?

---

## Modelling Methodology — MOMo

The Phase 2 extension follows the **Modular Ontology Modeling (MOMo)** methodology using Ontology Design Patterns (ODPs) as reusable building blocks. Four patterns were applied:

- **Record Pattern** — `AffiliationRecord` reifies the Author–Institution relationship with time bounds (`hasStartYear`, `hasEndYear`), replacing a direct link that cannot represent change over time.
- **Membership Pattern** — `ResearchGroup` as a subclass of `Institution` with `memberOf` relating Authors to groups.
- **Controlled Vocabulary Pattern** — `OpenAccessStatus` with four named individuals: `GoldOA`, `GreenOA`, `BronzeOA`, `ClosedAccess`.
- **Provenance Pattern** — `PeerReviewRecord` captures whether and where a publication was peer reviewed.

---

## Research Integration — Phase 2

**Selected Study (Week 11):** Norouzi et al. (2025), *Ontology Population using LLMs*, Kansas State University & Wright State University.

The study demonstrates that LLMs can extract structured triples from natural language with ~90% coverage when guided by a modular ontology schema. The integration plan for ARPO uses this pipeline to populate the knowledge graph from open bibliographic APIs (Semantic Scholar, OpenAlex), with ARPO's modules serving as schema guidance for few-shot prompting.

---

## Data Sources

| Source | Type | Content |
|--------|------|---------|
| [Semantic Scholar](https://api.semanticscholar.org/) | REST API | Paper metadata, authors, citations, affiliations |
| [OpenAlex](https://api.openalex.org/) | REST API (CC0) | Works, authors, institutions, venues, concepts |
| [CrossRef](https://api.crossref.org/) | REST API | DOI metadata, ISSN, publisher, funding |
| [DBLP](https://dblp.org/xml/) | XML bulk download | CS publications, author disambiguation |

---

## Usage

### Loading in Protégé
1. Open [Protégé](https://protege.stanford.edu/) (version 5.x recommended)
2. **File → Open** and select `arpo.ttl`
3. **Reasoner → HermiT → Start Reasoner** to verify consistency and infer new facts

### Example SPARQL Queries

**CQ1 — Papers by a given author:**
```sparql
PREFIX arpo: <https://example.org/arpo#>
SELECT ?paper ?title WHERE {
    ?author arpo:hasName "Alice Smith" .
    ?paper  arpo:hasAuthor ?author ;
            arpo:hasTitle  ?title .
}
```

**CQ13 — Gold or green open access publications:**
```sparql
PREFIX arpo: <https://example.org/arpo#>
SELECT ?paper ?title WHERE {
    ?paper arpo:hasOpenAccessStatus ?status ;
           arpo:hasTitle ?title .
    FILTER (?status IN (arpo:GoldOA, arpo:GreenOA))
}
```

**CQ14 — Grants that funded a given publication:**
```sparql
PREFIX arpo: <https://example.org/arpo#>
SELECT ?grantNumber ?funder WHERE {
    arpo:paper_001 arpo:hasFunding ?grant .
    ?grant arpo:hasGrantNumber ?grantNumber ;
           arpo:fundedBy ?fundingBody .
    ?fundingBody rdfs:label ?funder .
}
```

---

## Design Decisions

- **OWL 2 DL** chosen for decidability while supporting inverse properties, disjointness, and functional constraints.
- **Flat single-inheritance** for publication types keeps reasoning tractable.
- `hasCoAuthor` declared **symmetric** — co-authorship inferred in both directions automatically.
- `cites` declared **irreflexive** — a publication cannot cite itself.
- **MOMo record pattern** used for `AffiliationRecord` to handle time-varying affiliations cleanly.
- **Controlled vocabulary** for `OpenAccessStatus` uses named individuals with `owl:AllDifferent` to enforce mutual exclusivity.
- Aligned with but not importing **BIBO**, **DC Terms**, and **FaBiO** to keep the ontology self-contained while maintaining semantic compatibility.

---

## Future Work

- `owl:sameAs` alignments to Wikidata, DBLP, and OpenAlex entity URIs
- SHACL shapes for data validation
- Implement the LLM population pipeline using Semantic Scholar / OpenAlex as input
- Extend with a full peer-review module (review scores, reviewer assignments)
- Generate and publish Widoco HTML documentation via GitHub Pages

---

## Authors

**Fırat Kaya Özgenç** — Knowledge Engineering and Ontologies, Spring 2026
