# Source registry

This file records candidate source datasets and publications for the first ingestion pass.

**Acquisition baseline:** 2026-10-07

## Historic Environment Scotland — NRHE / Trove

**Purpose:** master spatial/site inventory and stable archaeological identifiers.

- Dataset page: https://www.trove.scot/explore/datasets/national-record-of-the-historic-environment-data-for-download
- Provider: Historic Environment Scotland
- Coverage: Scotland
- Contents: spatial index for more than 320,000 NRHE site locations plus associated records
- License: Open Government Licence v3 (per provider page)

### Planned use

1. download the untouched spatial dataset into `data/raw/nrhe/<version>/`;
2. retain the original archive and metadata;
3. identify records classified as broch and related Atlantic roundhouse categories;
4. preserve original classifications rather than normalizing them in-place;
5. assign stable project site IDs while retaining NRHE/Trove identifiers.

Do not assume every record labeled "broch" is equally secure archaeologically.

---

## Historic Environment Scotland — Scottish Radiocarbon Index

**Purpose:** national baseline of archaeological radiocarbon determinations and site associations.

- Dataset page: https://www.trove.scot/explore/download-our-data/scottish-radiocarbon-index-data-for-download
- Provider: Historic Environment Scotland
- License: Open Government Licence v3 (per provider page)
- Important limitation: HES states that the index **has not been systematically updated since 2009**.

### Planned use

1. preserve the original database and site-location download;
2. inspect field definitions before designing normalization assumptions;
3. join determinations to NRHE/Trove sites where identifiers permit;
4. preserve lab IDs and source context;
5. flag records whose archaeological relationship to broch construction is unknown.

The index is a baseline, not a complete modern corpus.

HES lists `c14@hes.scot` for questions about the index and current updating work. Do not contact HES until the public-data corpus has been audited and specific gaps are known.

---

## Scottish Archaeological Research Framework — HighARF

### Datasheets

- Index: https://scarf.scot/regional/higharf/1-introduction/introduction/
- Relevant dataset: **Datasheet 7.3 — Complex Atlantic Roundhouses/brochs**
- Relevant chronology dataset: **Datasheet 2.1 — Highland radiocarbon dates**

**Purpose:** curated regional synthesis linking sites, classifications, dates, HER references, and archaeological commentary.

### Narrative/table source

- https://scarf.scot/regional/higharf/iron-age/7-3-settlement-evidence/7-3-5-buildings/7-3-5-2-complex-atlantic-roundhouses-brochs-galleried-duns/

This page includes a table of cAR/broch sites with dating evidence and explicitly warns about terminological problems and poor phasing at many antiquarian excavations.

### Planned use

Treat ScARF as both:
- a source of structured regional records;
- a human-readable cross-check on context and classification.

Do not overwrite primary radiocarbon data with ScARF summaries. Preserve both and link them.

---

## Archaeology Data Service / Proceedings of the Society of Antiquaries of Scotland

**Purpose:** primary excavation publications, chronology papers, context interpretation, and later specialist analyses.

### Old Scatness chronology

Dockrill, Outram & Batt, *Time and place: a new chronology for the origin of the broch based on the scientific dating programme at the Old Scatness Broch, Shetland*.

- ADS PDF:
  https://archaeologydataservice.ac.uk/catalogue/adsdata/arch-352-1/dissemination/pdf/vol_136/136_089_110.pdf
- Volume contents:
  https://archaeologydataservice.ac.uk/archives/view/psas/contents.cfm?vol=136

This paper is methodologically important because it discusses the distinction between primary, secondary, and tertiary deposits and the consequences for claims about broch construction chronology.

### Planned use

Do not scrape publication prose blindly into structured data.

For important sites:
1. identify tables / context descriptions;
2. capture the radiocarbon determinations;
3. record what archaeological event each sample actually constrains;
4. cite page/table/context;
5. assign a transparent project quality category.

---

## Additional source classes to investigate

These are not yet ingested and should not be treated as complete:

- Project Radiocarbon / newer UK radiocarbon corpus
- regional Historic Environment Records
- individual excavation monographs
- Discovery and Excavation in Scotland reports
- recent AOC Archaeology broch excavations
- Old Scatness project publications
- Dun Vulan publications
- Howe, Orkney chronology
- Clachtoll broch publications and datasets
- Upper Scalloway
- Crosskirk
- Dun Mor Vaul
- artifact-based chronologies where scientific dates are absent

## Provenance policy

For every downloaded source, capture:

```text
source_name
source_url
provider
license
acquired_at
source_version_or_date
local_path
checksum
notes
```

If the provider later updates the dataset, do not silently replace the evidentiary basis of previous analyses. Retain acquisition/version information so results can be reproduced.

## Contact strategy

Do **not** begin by asking archaeologists for "broch dates."

First construct the public evidence matrix.

Then contact researchers with narrow, falsifiable questions such as:

> We have site X represented by determinations A/B/C. Our reading is that these constrain occupation but not construction. Is there a published or unpublished construction-related determination or phasing model we are missing?

The gaps in the public corpus should determine whom we contact and what we ask.
