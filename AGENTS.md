# AGENTS.md

This repository is a research instrument before it is a visualization project.

## Prime directive

Preserve the distinction between **evidence**, **interpretation**, and **derived model output**.

Do not make the data cleaner by making it less true.

## Chronology rules

1. **Never replace an archaeological date range with its midpoint as if that midpoint were an observed date.**
2. Preserve original radiocarbon determinations, calibration information, laboratory IDs, sample material, context, and source whenever available.
3. Distinguish what a sample dates:
   - pre-construction
   - construction-associated
   - initial occupation
   - occupation
   - destruction/collapse
   - later reuse
   - unknown
4. A date from inside a broch does not automatically date broch construction.
5. Prefer explicit probability distributions or intervals over point estimates.
6. When a point estimate is required by an algorithm, document the transformation and perform sensitivity analysis.
7. Treat old-wood / inbuilt-age effects, residual material, redeposition, antiquarian excavation, disturbed deposits, and unclear stratigraphy as first-class uncertainty.
8. Do not combine dates merely because they belong to the same named site; phase and context matter.

## Site-classification rules

"Broch" is not a perfectly stable archaeological category.

Preserve:
- source classification,
- normalized classification,
- classification confidence,
- architectural evidence supporting the classification.

Do not silently promote a possible broch, galleried dun, simple Atlantic roundhouse, or generic roundhouse into a certain broch.

Analyses should make it possible to rerun results under stricter and broader classification criteria.

## Provenance

Every normalized or derived record must retain enough provenance to reconstruct its origin.

Prefer stable identifiers such as:
- NRHE / Trove identifiers
- HER identifiers
- radiocarbon laboratory IDs
- DOI / publication identifiers
- excavation context numbers where available

For manually interpreted records, preserve:
- citation
- quoted or paraphrased contextual basis
- reviewer / method
- confidence
- notes

## Data layers

### data/raw

Immutable copies of downloaded source datasets.

- Never hand-edit.
- Record acquisition date and source URL/identifier.
- Preserve source licenses.
- If a source changes, add a new version rather than overwriting historical source material when practical.

### data/normalized

Machine-cleaned, source-shaped data.

- Reproducible from raw data.
- No research conclusions should be smuggled into cleaning code.

### data/derived

Products of explicit interpretation/modeling.

Examples:
- inferred construction probability distributions
- maritime-distance matrices
- feature diffusion matrices
- model fits

Everything here should be reproducible from normalized data plus declared assumptions.

## Research hypotheses

Keep these competing explanations alive unless the evidence discriminates among them:

- **H1:** single-origin diffusion
- **H2:** multiple regional origins
- **H3:** maritime-network diffusion
- **H4:** local precursor evolution with exchange of architectural ideas
- **H5:** chronology is too sparse or imprecise to distinguish the above

Do not optimize the analysis to make the "wave" hypothesis look interesting.

A failure to detect diffusion is a valid result.

## Spatial reasoning

Do not assume Euclidean distance is the historically relevant metric.

Atlantic Iron Age interaction may be better represented by:
- coastal travel,
- navigable sounds,
- island hopping,
- maritime routes,
- topographic barriers.

Start with simple geographic distance as a baseline, then compare against explicit network/travel-cost models.

## Architectural-feature analysis

Where source data permit it, model architecture as features rather than only a binary broch label.

Possible features include:
- intramural cells
- galleries
- stairways
- double wall skins
- scarcement ledges
- guard cells
- wall batter
- tie/lintel slabs
- tower-like proportions

Do not infer absent features merely because a site is labeled "broch."

## Coding standards

- Prefer small, inspectable transforms.
- Use typed data structures at normalization boundaries.
- Write tests for parsers, date transformations, classification rules, and joins.
- Keep notebooks exploratory; move repeatable logic into `src/`.
- Avoid hidden state and manual spreadsheet-only transformations.
- Generate intermediate QA summaries after ingestion.
- Log dropped or unjoinable records rather than silently discarding them.

## Visualization rules

Visualizations must make uncertainty visible.

Avoid:
- one dot = one exact construction year
- animations that imply certainty unsupported by the chronology
- interpolated propagation fronts presented as observed history

Prefer:
- opacity/intensity derived from temporal probability
- interval or uncertainty overlays
- explicit data-quality filters
- toggles for strict/broad broch classification
- toggles for construction vs occupation evidence

## Working style

When extending this repository:

1. inspect existing methodology and source notes first;
2. identify whether a change affects evidence, interpretation, or presentation;
3. preserve provenance;
4. add tests where code transforms evidence;
5. update documentation when assumptions change;
6. state uncertainty rather than resolving ambiguity by convenience.

The goal is not to produce a persuasive map.

The goal is to find out whether the broch phenomenon actually contains a detectable spatiotemporal pattern.

## Research diary

Read [Diary.md](Diary.md) when resuming research or reviewing the project. The diary is part of the research record, not an optional progress summary. Other researchers must be able to reconstruct and challenge the paths we took, including unsuccessful investigations and choices that limited the available evidence.

For every consequential research choice, uncertainty, or barrier that changes the research path, append a dated entry explaining:

1. **Question or trigger:** What problem, observation, or uncertainty required a choice?
2. **Evidence examined:** Which datasets, publications, records, contexts, or experiments were actually checked? Include stable identifiers and precise locators where possible; distinguish verified evidence from unexamined leads.
3. **Alternatives:** What plausible approaches or explanations were considered? Why were alternatives rejected, deferred, or left open? Do not invent alternatives retrospectively.
4. **Reasoning and assumptions:** How does the evidence support the decision? State the mechanism or inferential steps, assumptions, confidence, and evidence that challenges the interpretation. Preserve the distinction between observation and judgment.
5. **Decision and consequences:** What did we choose, why, and what does it permit or prevent us from concluding? For a workaround, identify what it bypasses and which uncertainty remains.
6. **Verification and reconsideration:** What was tested, what happened, what remains untested, and what evidence or result would cause us to revisit the decision?
7. **Attribution and follow-through:** Who investigated or reviewed it, which uncertainty IDs it affects, and what work remains?

Record failed searches and unavailable sources when they affect coverage or the interpretation of absence. Record changes to inclusion criteria, joins, date transformations, classifications, schema, models, and uncertainty treatment with enough detail to reconstruct the earlier and later choices. A bare statement such as "cleaned the data" or "selected this model" is insufficient.

Update uncertainty statuses with supporting evidence and links to dated entries. Preserve earlier reasoning, disagreements, and corrections; append a superseding explanation when our understanding changes. Distinguish a user-directed choice from an investigator's recommendation, and a proposed investigation from completed work. Agent review is not automatically archaeological expert review.

Treat the schema as provisional and mutable with evidence. Distinguish proposed investigations from completed work, and never mark scientific uncertainty resolved merely because a file was acquired or a model fitted successfully.

Scale detail to the significance of the choice: explain substantive research paths fully, while keeping routine mechanical work concise. The standard is whether a skeptical researcher can identify the assumptions, reproduce the relevant check, and disagree without having to infer missing reasoning from code or chat history.
