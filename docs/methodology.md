# Methodology

## 1. Unit of analysis

The project separates three concepts that are easy to conflate:

1. **Site** — a named archaeological place.
2. **Structure / phase** — a particular broch, roundhouse, rebuilding phase, or related architectural episode at that site.
3. **Observation** — a radiocarbon determination, artifact chronology, stratigraphic relationship, or other datum constraining a phase.

A single site may contain multiple structures and multiple occupation episodes. Do not force all evidence into one site-level date.

## 2. Evidence model

A chronological observation should minimally preserve:

| Field | Meaning |
|---|---|
| observation_id | Stable project ID |
| site_id | Project site ID |
| structure_phase_id | Optional structure/phase link |
| source_id | Publication/dataset provenance |
| source_record_id | Original identifier |
| lab_id | Radiocarbon lab code when applicable |
| dating_method | radiocarbon, dendrochronology, artifact, stratigraphy, etc. |
| material | bone, cereal grain, charcoal, antler, etc. |
| context | Archaeological context / layer / feature |
| event_relation | What event the observation constrains |
| relation_type | before / contemporary / after / uncertain |
| uncal_bp | Conventional radiocarbon age when applicable |
| sigma | Measurement uncertainty |
| calibrated_from | Published calibrated bound if only a range is available |
| calibrated_to | Published calibrated bound if only a range is available |
| probability | Published confidence level, if stated |
| quality | Project assessment of chronological usefulness |
| notes | Caveats |
| citation | Human-readable source |

### event_relation vocabulary

Initial controlled vocabulary:

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

This vocabulary may evolve, but changes must remain backwards interpretable.

## 3. Chronological inference

The target variable is not "the date of the broch" but an event distribution:

```text
P(T_construction | evidence)
```

Evidence may constrain this directly or indirectly.

Examples:

- short-lived material sealed beneath a foundation:
  - primarily constrains a **terminus post quem** for construction.
- short-lived material in a construction deposit:
  - may closely constrain construction, depending on context.
- earliest securely stratified occupation floor:
  - constrains construction to be earlier than or approximately contemporary with first use.
- later hearth:
  - demonstrates occupation at that date, not construction.
- destruction deposit:
  - constrains the end of a phase, not its beginning.

### Do not midpoint intervals

If a publication gives 390–200 BC, preserve that interval and its stated confidence.

Do not silently derive:

```text
construction_year = -295
```

If an algorithm later requires a scalar, that scalar is a model input or sampled latent value, not source data.

## 4. Dating quality

Each observation should receive a transparent, revisable quality assessment.

Initial categories:

```text
A  direct, well-published construction-related context
B  strong indirect constraint on construction / earliest use
C  useful occupation or destruction chronology
D  disturbed, poorly phased, old measurement, long-lived material, or weak association
U  unassessed / unknown
```

The category is not a judgment of the excavation as a whole; it describes usefulness for the specific construction-diffusion question.

Analyses must be rerunnable under thresholds such as A-only, A+B, and all evidence.

## 5. Site classification

Maintain both the original source label and normalized project classification.

Initial normalized classes:

```text
broch
complex_atlantic_roundhouse
galleried_dun
simple_atlantic_roundhouse
possible_broch
other
unknown
```

Also store classification confidence and diagnostic architectural features when known.

A central sensitivity analysis will ask whether conclusions change under:

- strict broch-only inclusion,
- broch + cAR,
- broader Atlantic roundhouse definitions.

## 6. Architectural features

Where publications support them, record features independently:

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

Presence, absence, unknown, and not-preserved must remain distinguishable.

This allows testing whether particular architectural ideas spread before the complete broch package.

## 7. Spatial models

Begin with latitude/longitude and great-circle distance as a null baseline.

Later compare against historically motivated alternatives:

- coastline-following distance
- island-hopping graphs
- navigable sounds / firths
- estimated maritime travel cost
- overland barriers

A "wave" should not be declared merely because sites farther from a chosen origin happen to have later midpoint dates.

## 8. Candidate diffusion models

### H1 — single-origin wave

A simple starting model:

```text
T_i = T_0 + d(O, i) / v + epsilon_i
```

where:

- `O` = candidate origin
- `T_0` = emergence time
- `v` = effective propagation rate
- `d` = selected spatial/network distance
- `epsilon_i` = local adoption delay + unmodeled effects

Dates are latent distributions, not exact observations.

### H2 — multiple origins

Use mixture / clustering approaches or compare region-specific emergence models.

### H3 — network diffusion

Replace geographic distance with graph distance or travel cost over a maritime interaction network.

### H4 — precursor evolution

Model individual architectural features and precursor forms, allowing regional development before mature brochs appear.

### H5 — insufficient information

Quantify how strongly the posterior / model comparison depends on a small number of sites or broad chronological intervals.

This is not a fallback embarrassment. It may be the scientifically correct result.

## 9. Visualization

The first map should show evidence coverage, not a diffusion wave.

Recommended views:

1. all candidate sites by classification;
2. sites with any scientific dating;
3. sites with construction-related evidence;
4. evidence quality;
5. temporal probability at a user-selected date;
6. architectural-feature distributions.

An animated map should make uncertainty visually explicit, for example by using temporal probability as intensity rather than switching sites on at an arbitrary midpoint.

## 10. Reproducibility and review

Manual archaeological interpretation is unavoidable, so make it auditable.

For every manual classification or context judgment, preserve:

- source
- relevant page/table/context
- interpretation
- confidence
- reviewer
- date reviewed

The long-term ideal is that an archaeologist can disagree with an interpretation, change one row, and rerun the analysis without reverse-engineering the code.
