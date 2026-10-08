# Data schema

This is the initial logical schema. Storage format may begin as Parquet/CSV and later move to DuckDB/PostgreSQL if useful. The logical model should remain stable enough that storage choices do not determine archaeological interpretation.

## sites

One row per archaeological place.

| field | type | required | description |
|---|---|---:|---|
| site_id | string | yes | Stable project identifier |
| name | string | yes | Preferred display name |
| latitude | float | yes | WGS84 |
| longitude | float | yes | WGS84 |
| nrhe_id | string | no | Historic Environment Scotland NRHE/Trove identifier |
| her_id | string | no | Regional HER identifier |
| source_classification | string | no | Classification exactly as supplied by source |
| normalized_classification | enum | yes | Project classification |
| classification_confidence | enum | yes | high / medium / low / unknown |
| region | string | no | Analytical/administrative region |
| notes | string | no | Human notes |

### normalized_classification

```text
broch
possible_broch
complex_atlantic_roundhouse
galleried_dun
simple_atlantic_roundhouse
other
unknown
```

## structures

A site may contain more than one relevant building or major structural phase.

| field | type | required | description |
|---|---|---:|---|
| structure_id | string | yes | Stable project ID |
| site_id | string | yes | FK -> sites |
| label | string | yes | e.g. broch tower, earlier roundhouse, rebuild |
| phase_order | integer | no | Relative order where known |
| normalized_classification | enum | no | Structure-level classification |
| confidence | enum | yes | high / medium / low / unknown |
| notes | string | no | Interpretation notes |

## sources

Bibliographic/dataset provenance.

| field | type | required | description |
|---|---|---:|---|
| source_id | string | yes | Stable project ID |
| title | string | yes | Dataset/publication title |
| authors_or_provider | string | no | Authors / organization |
| year | integer | no | Publication/release year |
| url | string | no | Stable URL where possible |
| doi | string | no | DOI |
| license | string | no | Source license |
| acquired_at | date | no | Dataset acquisition date |
| citation | string | no | Human citation |
| notes | string | no | Limitations/version info |

## observations

One row per chronological observation or constraint.

| field | type | required | description |
|---|---|---:|---|
| observation_id | string | yes | Stable project ID |
| site_id | string | yes | FK -> sites |
| structure_id | string | no | FK -> structures |
| source_id | string | yes | FK -> sources |
| source_record_id | string | no | Original dataset/context identifier |
| dating_method | enum | yes | radiocarbon / dendro / artifact / stratigraphy / other |
| lab_id | string | no | Radiocarbon laboratory identifier |
| material | string | no | Sample material |
| species | string | no | Taxon if known |
| context | string | no | Excavation context / feature |
| event_relation | enum | yes | Event being constrained |
| relation_type | enum | yes | Relationship of sample to event |
| uncal_bp | float | no | Conventional radiocarbon age BP |
| sigma | float | no | 1-sigma measurement error |
| cal_start | integer | no | Published calibrated lower calendar bound |
| cal_end | integer | no | Published calibrated upper calendar bound |
| calendar_system | string | no | e.g. astronomical year or BC/AD encoded convention |
| confidence_level | float | no | e.g. 0.954 |
| quality | enum | yes | A / B / C / D / U |
| residual_risk | bool | no | Possible residual/redeposited material |
| inbuilt_age_risk | bool | no | Old-wood / long-lived material concern |
| disturbed_context | bool | no | Context known/suspected disturbed |
| interpretation | string | no | Why this observation constrains the stated event |
| notes | string | no | Caveats |

### event_relation

```text
pre_construction
construction
initial_occupation
occupation
repair
destruction
collapse
post_broch_reuse
unknown
```

### relation_type

```text
terminus_post_quem
terminus_ante_quem
contemporary
approximately_contemporary
after
before
uncertain
```

### quality

```text
A  direct, well-published construction-related context
B  strong indirect constraint on construction / earliest use
C  useful occupation/destruction chronology
D  weak/disturbed/poorly phased/old or problematic evidence
U  unassessed
```

## architectural_features

Long-form feature observations.

| field | type | required | description |
|---|---|---:|---|
| structure_id | string | yes | FK -> structures |
| feature | string | yes | Controlled feature name |
| state | enum | yes | present / absent / unknown / not_preserved |
| source_id | string | yes | FK -> sources |
| confidence | enum | yes | high / medium / low / unknown |
| notes | string | no | Evidence / caveats |

Initial features:

```text
intramural_cells
galleries
stairways
double_wall_skin
scarcement
guard_cell
wall_batter
tie_or_lintel_slabs
tower_form
```

## interpretations

Manual research judgments should be represented explicitly rather than overwriting source data.

| field | type | required | description |
|---|---|---:|---|
| interpretation_id | string | yes | Stable project ID |
| entity_type | string | yes | site / structure / observation / feature |
| entity_id | string | yes | Target ID |
| field | string | yes | Interpreted property |
| value | string | yes | Interpretation |
| confidence | enum | yes | high / medium / low / unknown |
| rationale | string | yes | Why |
| source_id | string | no | Supporting source |
| reviewer | string | no | Person/agent making judgment |
| reviewed_at | date | no | Date |

This table allows an archaeologist to disagree with a project judgment without requiring mutation of imported source records.

## construction_models

Derived model outputs. Never source data.

| field | type | required | description |
|---|---|---:|---|
| model_id | string | yes | Stable run/model ID |
| structure_id | string | yes | FK -> structures |
| method | string | yes | Model description/version |
| evidence_filter | string | yes | e.g. A+B only |
| distribution_path | string | no | File containing sampled/grid distribution |
| summary_start | integer | no | Optional summary interval |
| summary_end | integer | no | Optional summary interval |
| notes | string | no | Assumptions |

## analysis_runs

Enough metadata to reproduce every published figure/model.

| field | type | required |
|---|---|---:|
| run_id | string | yes |
| git_commit | string | yes |
| created_at | datetime | yes |
| config_path | string | yes |
| input_manifest | string | yes |
| output_path | string | yes |
| notes | string | no |

## Calendar-year convention

Internally prefer **astronomical year numbering** for computation:

```text
1 BC  -> 0
2 BC  -> -1
3 BC  -> -2
AD 1  -> 1
```

Never expose this convention to readers without formatting it back to conventional BC/AD notation.

The raw source representation must also be preserved so conversion bugs are auditable.
