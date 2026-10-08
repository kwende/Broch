# Initial ingestion plan

The first milestone is deliberately narrow:

> **Determine how many candidate brochs/cARs have public chronological evidence that meaningfully constrains construction or earliest occupation.**

Do not build the diffusion visualization before this inventory exists.

## Phase 0 — acquisition manifest

Create a machine-readable manifest for every raw source:

```text
source_id
provider
url
acquired_at
license
version/date
filename
sha256
notes
```

Raw files are immutable.

## Phase 1 — NRHE / Trove site inventory

Input:
- Historic Environment Scotland NRHE spatial dataset.

Tasks:
1. download and checksum source archive;
2. inspect field names and encodings;
3. retain all records whose classifications plausibly intersect:
   - broch
   - possible broch
   - complex Atlantic roundhouse
   - galleried dun
   - related roundhouse categories worth auditing;
4. normalize coordinates to WGS84 if needed;
5. retain source classification verbatim;
6. produce `data/normalized/sites.parquet`;
7. emit QA:
   - total candidate sites;
   - counts by source classification;
   - missing/duplicate identifiers;
   - coordinate anomalies.

Do not de-duplicate sites by name alone.

## Phase 2 — Scottish Radiocarbon Index

Input:
- Scottish Radiocarbon Index database;
- site-location shapefile / associated identifiers.

Tasks:
1. inspect schema before coding assumptions;
2. normalize determinations without losing source columns;
3. preserve lab identifiers;
4. link to candidate broch/cAR sites using explicit IDs where possible;
5. record unmatched candidates;
6. use fuzzy name/spatial matching only as a proposed linkage requiring review;
7. produce `data/normalized/radiocarbon_index.parquet`;
8. emit QA:
   - determinations linked by explicit ID;
   - proposed fuzzy links;
   - unmatched records;
   - duplicate lab IDs;
   - missing material/context data.

At this stage, **do not claim a date represents broch construction**.

## Phase 3 — HighARF cross-check

Inputs:
- HighARF Datasheet 7.3 Complex Atlantic Roundhouses/brochs;
- HighARF Datasheet 2.1 Highland radiocarbon dates.

Tasks:
1. normalize site identifiers and names;
2. link HighARF records to NRHE/HER IDs;
3. compare dates against the Scottish Radiocarbon Index;
4. preserve HighARF's archaeological commentary;
5. flag:
   - newer dates absent from the national index;
   - classification disagreements;
   - context interpretations relevant to construction.

Output:
- a review queue, not silent reconciliation.

## Phase 4 — priority-site literature review

Begin with sites that strongly influence origin/diffusion hypotheses or have unusually good chronology.

Initial queue:

```text
Old Scatness
Dun Vulan
Howe
Clachtoll
Crosskirk
Upper Scalloway
Dun Mor Vaul
Dun Ardtreck
Dun Flodigarry
Elsay / Staxigoe
```

For each:
1. retrieve primary excavation/chronology publications where public;
2. enter individual chronological observations;
3. classify event relationship;
4. capture page/table/context provenance;
5. assign preliminary quality;
6. record ambiguity explicitly.

## Phase 5 — evidence matrix

Produce a human-reviewable table with one row per structure:

| site | class | construction evidence | earliest-use evidence | occupation only | best quality | source count |
|---|---|---|---|---|---|---|

Then answer:

- How many strict brochs have any scientific dating?
- How many have construction-related dating?
- How many have only occupation dates?
- How many rely primarily on artifact typology?
- How many are effectively undated for this research question?

This table is the first meaningful project result.

## Phase 6 — first map

Map:
- all candidate sites;
- strict/broad classification filter;
- evidence category;
- evidence quality.

The map should initially answer **where the chronological holes are**, not where the broch wave went.

## Phase 7 — chronology modeling

Only after enough evidence has been reviewed:

1. define construction-event constraints;
2. calibrate raw radiocarbon determinations where raw BP/sigma are available;
3. construct site/structure-level chronological models;
4. preserve posterior/grid samples;
5. validate against published models where available.

Do not recalibrate published ranges and overwrite them without recording both source and derived forms.

## Phase 8 — diffusion analysis

Begin with deliberately stupid baselines:

1. geographic distance from candidate origin vs chronology;
2. leave-one-site-out sensitivity;
3. strict vs broad site definition;
4. A-only vs A+B evidence.

Then add:
- maritime network distance;
- alternative origins;
- multiple-origin models;
- feature-level diffusion.

If removing Old Scatness destroys a conclusion, report that fact prominently.

## Definition of done for milestone 1

Milestone 1 is complete when the repository can reproducibly produce:

1. candidate broch/cAR site count from the public inventory;
2. count linked to public radiocarbon determinations;
3. count with manually reviewed construction/earliest-use constraints;
4. a provenance-backed evidence matrix;
5. a map of data coverage;
6. a machine-readable list of unresolved gaps.

Only then should the project spend serious effort on an animated diffusion visualization.
