# Research diary

This is the working record of uncertainties, investigations, barriers, and decisions in the Broch project. Read it alongside [methodology](docs/methodology.md), [sources](docs/sources.md), and the [ingestion plan](docs/ingestion-plan.md).

The purpose is to let another researcher reconstruct **what we questioned, what we checked, what we learned, and why we chose the next research path**. A resolved access problem does not resolve a scientific uncertainty.

## How to maintain this diary

- Give each uncertainty a stable ID. Use **Open**, **Mitigated**, **Accepted limitation**, or **Resolved**, with evidence explaining any status change. A workaround may mitigate a problem without resolving it.
- Append dated entries describing the question, sources or experiment, observations, interpretation, decision or workaround, and remaining work. Identify the investigator/reviewer and relevant uncertainty IDs.
- For consequential choices, explain the alternatives actually considered, why they were rejected or deferred, the inferential steps and assumptions supporting the selected path, its limits, and what would cause reconsideration. Record unsuccessful investigations or inaccessible sources when they affect coverage. Follow the [research diary requirements in AGENTS.md](AGENTS.md#research-diary).
- Distinguish completed work from proposed work, source measurements from interpretations, and interpretations from derived model outputs.
- Preserve earlier reasoning when a decision changes. Add a correction or superseding entry rather than silently rewriting the history. Update the current status and link to that entry.
- For new data, record the publication/dataset identifier, version or acquisition date, page/table/context where applicable, and file checksum when available. Identify the exact selection and counting unit.
- Current schemas are provisional. Revise or discard them when inspected evidence demonstrates a mismatch; record the reason here.
- External reviewers should cite the evidence behind their findings and distinguish verified findings from leads. Record disagreements as reviewable alternatives.

## Uncertainties

### U-001 — Can the available evidence distinguish diffusion hypotheses?

**Status: Open. Raised: 2026-10-07.**

**Concern:** The user questioned whether approximately 21 dated candidate sites could support an adequate determination, particularly if geographically clustered. The relevant quantity is the number and distribution of independently informative structure/event constraints, not the number of laboratory measurements.

**What we have checked:** The initial national inventory/workbook join identifies 20 broch-labelled site records. The Clachtoll publication adds one further site. Those 21 span Shetland, Orkney, the Western Isles, Highland/Skye, Argyll and Bute, and Stirling, but include local clusters. Five sites account for 165 of the 239 national workbook rows. Classification and event relevance have not been systematically reviewed. See D-002 through D-005 and the evidence snapshot below.

**Interpretation:** The sites are not all confined to one locality, but regional spread alone does not establish adequacy. Repeated measurements at a site can improve its chronology without adding independent examples of architectural adoption. Broad temporal uncertainty and occupation-only evidence may leave alternative histories indistinguishable.

**Current working decision:** Continue the evidence inventory and assess adequacy before making origin, direction, propagation-rate, or maritime-route claims. There is no justified minimum site-count threshold yet. The corpus has not been demonstrated sufficient or insufficient; H5 remains live.

**Investigations proposed, not completed:**

1. Reconcile regional and publication sources to establish coverage beyond the national export.
2. Review source classifications and sample contexts; count structures with meaningful construction or earliest-use constraints separately from sites with any dating.
3. Map relevant evidence, uncertainty, regional gaps, and clustering under strict and broad inclusion criteria.
4. Assess dependence on individual sites and regions using leave-one-site/region-out sensitivity.
5. If modeling becomes justified, simulate competing histories at the observed locations and assess whether the dating evidence could distinguish them. Declare chronology, sampling, and travel assumptions; do not turn published intervals into assumed uniform distributions without justification.

**What would change the decision:** An expanded, reviewed evidence matrix and explicit assessment of distinguishability. A successful model fit alone would not resolve this concern. If plausible competing histories remain indistinguishable, report the limitation and narrow the question rather than manufacture precision.

**Workaround:** No scientific workaround adopted. Descriptive coverage analysis remains useful while adequacy is unresolved.

### U-002 — How incomplete is the assembled chronology corpus?

**Status: Open; source-access barrier partly mitigated. Raised: 2026-10-07.**

The national workbook's explanatory sheet says it has not been systematically updated since 2009. The separate spatial-index metadata gives older coverage/update notes. Neither establishes a complete present-day corpus. HighARF already lists dated sites absent from the national 20-site selection, and Clachtoll has 20 published determinations compared with one HighARF row and none found by those SUERC IDs in the national workbook.

The user supplied national downloads and the Clachtoll PDF when automated access was restricted or the reader did not expose the file. This resolves those particular retrieval barriers, not completeness. Full HighARF reconciliation and publication supplementation remain pending. Missing from an export must not be recorded as never dated.

### U-003 — Which structures and events do the dates actually constrain?

**Status: Open. Raised: 2026-10-07.**

Some source records explicitly classify a broch as possible, and a site may contain earlier activity, other buildings, burials, and later reuse. The 21-site count is not a count of confirmed brochs or reviewed construction chronologies. The earliest radiocarbon measurement is a starting point for context review, not an automatic construction date.

Clachtoll demonstrates the distinction: the authors interpret two early determinations as residual material and associate scarcement charcoal with the final burning event. Their interpretations must remain attributable and revisable. Review classification and archaeological association before using observations in a construction or trait-transmission analysis.

### U-004 — How should source inconsistencies and missing-value conventions be handled?

**Status: Open; several issues identified. Raised: 2026-10-07.**

Observed issues include zero age/error placeholders, literal `No` calibration metadata alongside supplied calibrated ranges, conflicting laboratory-ID assignments, and inconsistent outlier identifiers in Clachtoll's prose versus Table 3.1. The national `Lab Age Bc` field generally equals `Lab Age - 1950`; it is not a calibrated calendar-date field. Applying that arithmetic to a zero placeholder produces `-1950` without supplying a usable archaeological date.

Working approach: preserve source values; flag unusable measurements and unresolved conflicts; distinguish unknown metadata from negative evidence; never silently correct, deduplicate, average, or discard records. Verify semantics against source documentation or primary reports. Parser rules and adjudications have not yet been implemented.

### U-005 — Can architectural traits be compared and dated at the required resolution?

**Status: Open. Raised: 2026-10-07.**

The user's motivating example is the regional transmission of a distinctive floor-support method. A trait variant describes how something was built; a phase describes an evidenced construction or alteration episode. Observing a trait does not necessarily date its installation, and resemblance alone does not establish genealogy.

The national inventory export lacks detailed trait columns. HighARF offers an intramural-feature indicator and notes; excavation publications provide richer descriptions and interpretations. Inspect those sources before deciding whether trait variants or phase associations can be encoded consistently. No expanded trait/phase schema has been adopted.

## Dated diary entries

### D-001 — 2026-10-07: establish a data-first research direction

**Participants:** User and Codex. **Related:** U-001, U-003, U-005.

The repository began as methodology, source notes, a logical schema, and a Python scaffold. Initial discussion explored structures, phases, and potentially transmitted architectural traits. The user redirected the work toward inspecting actual data before extending the design and explicitly clarified that schemas should be **mutable with evidence**.

**Decision:** Treat schema and modeling suggestions as provisional. Acquire and inspect sources before implementing assumptions. Architectural traits remain a research interest, not an established extractable dataset.

### D-002 — 2026-10-07: inspect the supplied national datasets

**Investigator:** Codex; files downloaded and supplied by the user. **Related:** U-001 through U-004.

Inspected archive contents, DBF schemas and records, accompanying metadata/readmes, and both workbook sheets. Used source attributes rather than hand-normalizing classifications. Selected inventory records using case-insensitive `\bBROCHS?\b` in `SITETYPE`, then joined `CANMOREID` to positive integer `Numlink` values in the workbook. No fuzzy matching or archaeological reclassification was used.

**Observed:** 733 selected inventory records; 239 associated workbook rows across 20 identifiers; 236 rows with positive laboratory age and error. All 967 positive site IDs in the full workbook match the point inventory and radiocarbon location layer. The remaining 325 workbook rows have `Numlink = 0`. All 239 selected rows have sample descriptions, but these have not been systematically classified by event relevance.

**Issues found:** Three selected rows contain zero age/error values. Some calibration metadata is literal `No`. One lab ID, `GU-2415`, occurs in two full-workbook records with different measurements; one description explicitly disputes that identifier. `Lab Age Bc = Lab Age - 1950` holds in 5,404 of the 5,414 workbook rows.

**Decision:** Use this as an initial evidence-coverage audit. Do not describe its 20 sites as the complete dated-broch corpus or its rows as construction dates. No source files were changed and no production ingestion pipeline was implemented.

### D-003 — 2026-10-07: follow regional and primary-publication leads

**Investigators:** Codex and user. **Related:** U-002, U-004, U-005.

Downloaded and inspected HighARF Datasheets 2.1 and 7.3. Broch-related radiocarbon rows include additional sites such as Applecross, Thrumster, Nybster, Whitegate, and Clachtoll. These are leads supported by spreadsheet records; the union of datasets has not yet been fully reconciled.

The Trove download pages initially returned HTTP 403 to the web reader. The user supplied the downloads locally. Clachtoll's publisher offered a free open-access monograph, but its linked reader exposed only a loading page to the web tool. The user downloaded the full PDF. Public PDFs for Thrumster and Old Scatness were accessible to the web reader; detailed extraction/reconciliation remains pending.

**Workaround:** Human-assisted retrieval of specified public files. Preserve acquisition details and checksums; use narrow download requests when automated access fails. No contact with researchers was made.

### D-004 — 2026-10-07: inspect Clachtoll and correct the counting ambiguity

**Investigator:** Codex; PDF supplied by user. **Related:** U-002 through U-005.

Read the radiocarbon chapter, printed pp. 40-48, and visually checked Table 3.1, printed p. 43 (PDF page 54). The table contains 20 distinct SUERC laboratory IDs, none found under those IDs in the supplied national workbook. HighARF includes one of them, `SUERC-36728`. The book therefore adds **19 determinations beyond HighARF's Clachtoll row, but only one site beyond the national 20-site selection**.

The table preserves context, sample type/species, BP age/error, and calibrated 2-sigma interval. The chapter states calibration using OxCal 4.4/IntCal20, while a later passage describes phase modeling using OxCal 4.3.2; preserve the distinction. The authors discuss two early residual determinations, a core group of 17, and one late determination interpreted as displaced material. A footnote records two undatable samples. These are published interpretations, not newly established project conclusions.

**Source conflict:** On printed p. 41 the outlier discussion names `SUERC-87247` and `SUERC-87246`; Table 3.1 assigns those codes to 2088 +/- 24 BP and 2053 +/- 21 BP. Its two earliest rows are instead `SUERC-78231` (2371 +/- 26 BP) and `SUERC-78230` (2325 +/- 26 BP). The intended correction is unadjudicated.

**Correction recorded:** Ambiguous conversational wording led to a question about 39 sites. The scoped total is 21 candidate site records and 259 source rows/determinations (239 national rows + 20 Clachtoll determinations), including the three national zero placeholders. It is not 39 sites, 21 confirmed brochs, or 259 construction dates. Other HighARF sites are not included in that total.

### D-005 — 2026-10-07: raise adequacy as an explicit unresolved question

**Participants:** User and Codex. **Related:** U-001.

The user questioned whether 21 sites, especially if clustered, could support an adequate determination. Checked the national workbook's site coordinates and council assignments, adding Clachtoll to Highland for the scoped 21-site summary. The sites span six administrative regions; local proximity remains evident. The five largest national site groups contribute 165 rows, showing concentration of measurements.

**Assessment:** There is enough evidence to investigate adequacy, but sufficiency for discriminating diffusion hypotheses has not been established. Geographic spread is only one prerequisite. Relevant event constraints, temporal resolution, classification, sampling coverage, and dependence between observations remain unresolved.

**Research path:** Continue source reconciliation and context review. Coverage mapping and sensitivity/recovery experiments are proposed next steps, not completed validation. No diffusion model, statistical power calculation, or maritime network analysis has been run.

### D-006 — 2026-10-07: make research decisions reviewable across agents

**Requested by:** User. **Implemented by:** Codex. **Related:** U-001 through U-005.

The user requested a repository diary so ChatGPT and other agents can investigate sources and review the research paths, and then explicitly requested full explanations of choices and reasoning in `AGENTS.md`.

**Decision:** Use this root-level Markdown diary with stable uncertainty IDs, dated entries, a scoped evidence snapshot, source checksums, and public references. Link it from the README and require consequential decisions to record actual alternatives, assumptions, evidence, verification, consequences, and reconsideration criteria. This keeps the handoff readable on GitHub and makes unresolved questions visible without implying that a completed task resolves them.

**Limit:** This document preserves the investigation record, but does not replace the planned immutable source archive, tested transforms, or reproducible analysis runs. Local inputs have not been added to Git. External reviewers must establish access to matching sources before claiming an independent reproduction of the initial counts.

## Evidence snapshot — 2026-10-07

These are recorded results of local source inspection, not outputs of a checked-in ingestion pipeline. The source files and temporary inspection scripts/results are not currently committed to this repository. A reviewer can inspect the public sources and verify the recorded IDs and counts; exact reruns require the matching source snapshots. Checksums below identify those snapshots without depending on local filesystem paths.

### Counting units and scope

| Quantity | Recorded result | What it means |
|---|---:|---|
| Main point-inventory records | 314,241 | `Canmore_Points.dbf`; separate maritime layer excluded |
| Records with a broch classification token | 733 | Lexical source selection; possible brochs included |
| National radiocarbon workbook rows | 5,414 | Header excluded; not all rows are usable measurements |
| Selected national rows / site IDs | 239 / 20 | Exact inventory-to-workbook identifier join |
| Selected national rows with positive age/error | 236 | Numeric screening only, not archaeological quality review |
| Clachtoll table determinations / added site | 20 / 1 | Table 3.1; Clachtoll NRHE/Canmore ID 4499, HER MHG13002 |
| Scoped national-plus-Clachtoll total | 259 records / 21 sites | Includes three zero placeholders; other HighARF additions excluded |

### Geographic distribution of the scoped 21 sites

Council regions are used here for description, not as archaeological interaction regions.

| Region | Sites | NRHE/Canmore identifiers |
|---|---:|---|
| Shetland | 3 | 556, 918, 995 |
| Orkney | 5 | 1483, 1560, 1731, 2838, 2867 |
| Western Isles | 4 | 4020, 4100, 4121, 9825 |
| Highland, including Skye and Clachtoll | 6 | 4499, 6546, 8019, 11064, 11388, 12146 |
| Argyll and Bute | 1 | 21524 |
| Stirling | 2 | 44651, 45379 |

The five largest national groups are 556 (46 rows), 9825 (40), 2867 (29), 1731 (26), and 995 (24), totaling 165. These counts include zero placeholders. Their source names are SUMBURGH AIRPORT, SOUTH UIST, BORNISH, DUN VULAN, PAPA WESTRAY, MUNKERHOOSE, THE HOWE, and UPPER SCALLOWAY respectively. Retain the identifiers rather than assuming a preferred name or one-to-one building identity.

### Source snapshots

Original files were inspected without modification. National files and the Clachtoll PDF were supplied locally by the user on 2026-10-07; HighARF files were retrieved during the same investigation. Retrieval date is not publication date or evidence of complete coverage. See [sources](docs/sources.md) for provider and licensing notes.

| Filename | Bytes | SHA-256 |
|---|---:|---|
| `Canmore_Points.zip` | 35,955,064 | `2875058f4ad10547e835d5a16e23b7db0cbebe0ab3354758292d5e66881c52bd` |
| `scottish-radiocarbon-database-with-location.xlsx` | 1,470,113 | `f22b539ca83083ae6ca9495885700c65a7cfffa24aeef72275c8b411c2e2c0b0` |
| `scottish-c14-site-locations.zip` | 100,914 | `e5f12a943f9cdca00402837866cf8cf5adb35341af7b871d2d909f3dec37143b` |
| `nrhe_areas.zip` | 39,527,835 | `33a45cbdbf477f4ebd8acaf20cf7880122e530008627f1ec7aa948a345677a0e` |
| `7da21b37-875f-4dad-9c09-e7fe99755a15.zip` | 11,021 | `de352464b16d196774fb0df7d723eae0a739e5225031a0b69164397df445d6ce` |
| `Datasheet-2.1-Radiocarbon-Data-table-22-9-2021.xls` | 1,080,832 | `e913b69f22f06f3b2c2fee6f85583594ec5439d4f27f71011109d4e8d9b869ad` |
| `Datasheet-7.3-Brochs-cARs.xlsx` | 53,963 | `9658c9b07589481d2e5405048aa4e64b93a522e0f0bd492b3548cb18a3436285` |
| `Clachtoll-2022.pdf` | 13,087,801 | `f83cbca3571a152123346f0d8c1d50794c5f5aa3a767720013aa70f6c76dc604` |

### Public source and review leads

- [NRHE/Trove inventory download page](https://www.trove.scot/explore/datasets/national-record-of-the-historic-environment-data-for-download).
- [Scottish Radiocarbon Index download page](https://www.trove.scot/explore/download-our-data/scottish-radiocarbon-index-data-for-download).
- [HighARF datasheet index](https://scarf.scot/regional/higharf/1-introduction/introduction/), [radiocarbon XLS](https://scarf.scot/wp-content/uploads/sites/15/2021/09/Datasheet-2.1-Radiocarbon-Data-table-22-9-2021.xls), and [broch/cAR XLSX](https://scarf.scot/wp-content/uploads/sites/15/2021/09/Datasheet-7.3-Brochs-cARs.xlsx).
- Cavers, G. (ed.), 2022, *Clachtoll: An Iron Age Broch Settlement in Assynt, North-west Scotland*, Oxbow Books. [Publisher/open-access link](https://www.oxbowbooks.com/9781789258479/clachtoll/). Barber and Cavers, chapter 3, printed pp. 40-48, Table 3.1 p. 43; [chapter DOI](https://doi.org/10.2307/jj.5699284.8).
- [Clachtoll HER record MHG13002](https://her.highland.gov.uk/Monument/MHG13002).
- [Thrumster 2011 excavation final report](https://her.highland.gov.uk/api/LibraryLink5WebServiceProxy/FetchResourceFromStub/1-2-0-2-3-7_7879232f72f8847-120237_3ae90d76f222fa3.pdf), Barber with Humphreys, report dated 29 February 2012; detailed review pending.
- [Old Scatness chronology paper](https://archaeologydataservice.ac.uk/catalogue/adsdata/arch-352-1/dissemination/pdf/vol_136/136_089_110.pdf), Dockrill, Outram and Batt, 2006, *Proceedings of the Society of Antiquaries of Scotland* 136, pp. 89-110; detailed extraction/reconciliation pending.

## Questions for incoming reviewers

1. What published determinations or securely identified sites are missing from this scoped corpus? Supply IDs, primary citations, and contexts; separate new measurements from duplicate reports or recalibrations.
2. Which observations genuinely constrain construction or earliest use, and which only date other activity? Explain the stratigraphic argument and alternatives.
3. Which classifications or apparently separate site records need review before counting independent architectural examples?
4. What geographical and temporal contrasts could these observations resolve? Suggest a discriminating experiment rather than asserting sufficiency from a count or model fit.
5. Which architectural variants are documented consistently enough for comparison, and how securely can they be assigned to structures or phases?

Review findings should update the relevant uncertainty through a dated entry. Acquisition leads, reviewer recommendations, and proposed experiments do not by themselves resolve an uncertainty.
