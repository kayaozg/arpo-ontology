# Academic Research Publication Ontology (ARPO)

> Knowledge Engineering and Ontologies — Course Project  
> Initial Phase · April 2026

## Overview

**ARPO** is an OWL 2 DL ontology that formally represents the domain of academic research publications. It models publications, authors, institutions, venues, citation relationships, and research topics, enabling semantic search, bibliometric reasoning, and cross-database knowledge integration.

---

## Domain

Academic research publishing — the full lifecycle of a scholarly work, from the authors and institutions who produce it, to the venues where it is published, to the citation networks that connect it to other work.

---

## Repository Structure

```
arpo/
├── arpo.ttl              # Main ontology file (OWL 2 DL, Turtle syntax)
├── ARPO-ORSD.docx        # Ontology Requirements Specification Document (draft)
└── README.md             # This file
```

---

## Key Concepts

### Classes

| Class | Description |
|-------|-------------|
| `Publication` | Top-level class for all academic research outputs |
| `JournalArticle` | Peer-reviewed article published in a journal |
| `ConferencePaper` | Paper presented at an academic conference |
| `BookChapter` | Chapter within an edited academic book |
| `Thesis` | Doctoral or master's dissertation |
| `TechnicalReport` | Institutional technical report |
| `Author` | Researcher who has authored publications |
| `Institution` | University, research institute, or company |
| `Journal` | Periodical publication venue |
| `Conference` | Academic event venue |
| `ResearchTopic` | Thematic subject area |
| `Keyword` | Descriptor term for a publication |
| `Citation` | A formal reference between two publications |

### Object Properties

| Property | Domain → Range | Description |
|----------|---------------|-------------|
| `hasAuthor` / `isAuthorOf` | Publication ↔ Author | Authorship relation |
| `hasCoAuthor` | Author ↔ Author | Symmetric co-authorship |
| `isAffiliatedWith` / `hasAffiliation` | Researcher ↔ Institution | Affiliation |
| `publishedIn` | Publication → Venue | Publication venue |
| `cites` / `isCitedBy` | Publication ↔ Publication | Citation network |
| `hasResearchTopic` | Publication → Topic | Topical coverage |
| `hasKeyword` | Publication → Keyword | Descriptor keywords |

### Data Properties

| Property | Domain | Range |
|----------|--------|-------|
| `hasTitle` | Publication | xsd:string |
| `hasAbstract` | Publication | xsd:string |
| `hasYear` | Publication | xsd:integer |
| `hasDOI` | Publication | xsd:string |
| `hasCitationCount` | Publication | xsd:integer |
| `hasISSN` | Journal | xsd:string |
| `hasImpactFactor` | Journal | xsd:decimal |
| `hasName` | Person | xsd:string |
| `hasORCID` | Researcher | xsd:string |

---

## Ontology Details

| Item | Value |
|------|-------|
| Namespace | `https://example.org/arpo#` |
| Prefix | `arpo:` |
| OWL Profile | OWL 2 DL |
| Serialisation | Turtle (`.ttl`) |
| Reasoner compatibility | HermiT, Pellet |
| Licence | [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) |

---

## Competency Questions

The ontology is designed to answer the following competency questions:

1. What papers has a given author published?
2. Which papers cite a given publication?
3. In which venue (journal or conference) was a specific paper published?
4. What research topics are covered by a specific paper?
5. Which authors are affiliated with a given institution?
6. What papers were published within a given date range?
7. Which papers are co-authored by researchers from two or more different institutions?
8. How many times has a given paper been cited?
9. Which researchers have collaborated with a given author?
10. What is the ISSN or impact factor of a given journal?
11. Which papers belong to a given research topic?
12. What is the full list of authors of a given paper, in order?

---

## Usage

### Loading in Protégé

1. Open [Protégé](https://protege.stanford.edu/) (version 5.x recommended).
2. **File → Open** and select `arpo.ttl`.
3. Run the HermiT or Pellet reasoner via **Reasoner → Start Reasoner**.

### Example SPARQL Query

**CQ1 — What papers has Alice Smith published?**

```sparql
PREFIX arpo: <https://example.org/arpo#>

SELECT ?paper ?title WHERE {
    ?author arpo:hasName "Alice Smith" .
    ?paper  arpo:hasAuthor ?author ;
            arpo:hasTitle  ?title .
}
```

**CQ2 — Which papers cite paper_001?**

```sparql
PREFIX arpo: <https://example.org/arpo#>

SELECT ?citing ?title WHERE {
    ?citing arpo:cites arpo:paper_001 ;
            arpo:hasTitle ?title .
}
```

---

## Design Decisions

- **OWL 2 DL** was chosen over Full to maintain decidability while supporting rich axioms (inverse properties, cardinality, disjointness).
- **Subclass hierarchy** uses a flat, single-inheritance pattern for publication types to keep reasoning tractable.
- `hasCoAuthor` is declared **symmetric** so that co-authorship is inferred in both directions automatically.
- `cites` is declared **irreflexive** to prevent a publication from citing itself.
- Functional properties (e.g., `hasTitle`, `hasYear`, `hasDOI`) enforce single-value constraints.
- The ontology is designed to be **aligned in future iterations** with BIBO, DC Terms, and SPAR/FaBiO.

---

## Future Work

- Add `owl:sameAs` alignments to Wikidata, DBLP, and OpenAlex entity URIs.
- Extend with a `PeerReview` module (review process, review scores).
- Add a `Funding` module (grant, funder, award number).
- Create SHACL shapes for data validation.
- Populate with real-world instances from an open bibliographic dataset.

---

## Authors

Fırat Kaya Özgenç — Knowledge Engineering and Ontologies, Spring 2026
