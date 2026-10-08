# Broch

An open-data research project for asking a deceptively simple question:

> **Did broch architecture spread through Iron Age Scotland as a spatial-temporal cultural diffusion process, or did similar forms emerge through multiple regional developments?**

The motivating analogy is a cultural movement such as 1990s grunge: an identifiable form may emerge in one or more connected communities, then propagate through social and transport networks. For brochs, the relevant network may have been strongly maritime.

## Core principle

**Do not turn archaeological uncertainty into fake precision.**

A radiocarbon range such as 390–200 BC is not `295 BC`. The primary analytical object is a chronological constraint or probability distribution, not a single construction year.

Likewise, a date from a hearth inside a broch dates an occupation event unless context justifies a stronger relationship to construction.

## Research questions

1. Where and when do securely identified brochs / Complex Atlantic Roundhouses first appear?
2. Do construction dates show a spatial gradient compatible with diffusion?
3. Is geographic distance less explanatory than maritime-network distance?
4. Do individual architectural features propagate before the mature broch form?
5. Are the data better explained by:
   - a single origin and outward diffusion,
   - multiple regional origins,
   - diffusion through a maritime interaction network,
   - gradual regional evolution from precursor roundhouses,
   - or insufficient evidence to distinguish these models?

## Project stages

### 1. Build the evidence corpus

Collect and normalize:

- Historic Environment Scotland NRHE / Trove site records
- Scottish Radiocarbon Index determinations
- ScARF broch / Complex Atlantic Roundhouse datasets
- published excavation reports and chronologies
- Archaeology Data Service material
- later radiocarbon results not represented in the older national index

For every chronological observation, preserve its archaeological context and source.

### 2. Model chronology

Represent evidence as relationships to events:

```text
pre-construction
construction
initial occupation
occupation
destruction / collapse
post-broch reuse
unknown
```

Derive construction-age distributions only when the evidence supports doing so.

### 3. Visualize before modeling

First produce an honest map showing:

- all candidate broch/cAR sites
- classification confidence
- which sites have chronological evidence
- what that evidence actually dates
- uncertainty / quality

A beautiful absence of data is still a result.

### 4. Test diffusion hypotheses

Candidate models include:

```text
H1  single-origin diffusion
H2  multiple regional origins
H3  maritime-network diffusion
H4  local precursor evolution + exchange of architectural ideas
H5  available chronology is insufficient to distinguish the above
```

Potential analyses include distance-vs-date relationships, network-distance models, Bayesian chronology, feature-level diffusion, and sensitivity analysis over site classification.

## Repository layout

```text
data/
  raw/          immutable source downloads
  normalized/   cleaned source-shaped records
  derived/      analytical outputs; reproducible from normalized data

docs/
  methodology.md
  sources.md

src/broch/
  ingestion/
  chronology/
  analysis/
  visualization/

tests/
```

Directories will be added as the corresponding code or data exists; empty placeholder trees are deliberately avoided.

## Reproducibility

Every derived datum should answer:

1. **Where did this come from?**
2. **What archaeological event does it constrain?**
3. **What transformation produced the value being analyzed?**

Raw source material must never be silently edited.

## Research diary and uncertainties

[Diary.md](Diary.md) records open uncertainties, source inspections, barriers, workarounds, and research decisions. Start there when joining or reviewing the project. In particular, **U-001** tracks whether the available chronological evidence can distinguish diffusion hypotheses; the current evidence has not established adequacy.

The diary includes the initial source-audit counts and their provenance. These are recorded inspection results; a reproducible ingestion pipeline has not yet been implemented. The logical schema remains provisional and may change with evidence.

## Status

Bootstrap phase. The first milestone is to ingest the public site inventory and radiocarbon corpus and determine how many brochs actually possess useful construction-related chronological evidence.
