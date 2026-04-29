# Changelog

All notable changes to PersianIdioBench are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.1.0] - 2026-04-29

### Added
- `data/raw/raw_idioms.csv` — the cleaned, de-duplicated 4,352-idiom inventory used as the starting pool for all three task datasets. Columns: `proverb`, `normalized`, `source`, `tokens`.
- `data/raw/README.md` data card describing schema, source distribution, construction protocol, and relation to the Connotation, Appropriateness, and Cloze datasets.

### Changed
- Top-level `README.md` repository layout and "Datasets at a glance" table updated to include the raw idiom repository.

## [1.0.1] - 2026-04-21

### Changed
- Replaced `data/cloze/cloze.csv` with the self-contained version of the Task 3 dataset. The file now includes a `candidates` column providing ten distractor idioms per row, so the cloze task can be evaluated directly from a single file without needing to sample distractors from `data/connotation/`. Row count adjusted from 2,457 to 2,211 after the update.
- Updated `data/cloze/README.md` data card to describe the new schema and document how to parse the `candidates` column with `ast.literal_eval`.

## [1.0.0] - 2026-04-21

### Added
- Initial public release of PersianIdioBench.
- Task 1 dataset: `data/connotation/connotation.csv` (2,706 idioms with gold evaluative-polarity labels).
- Task 2 dataset: `data/appropriateness/appropriateness.csv` (5,089 idiom-in-text pairs with binary appropriateness labels).
- Task 3 dataset: `data/cloze/cloze.csv` (masked paragraphs for cloze-style idiom selection).
- Per-task data cards under `data/<task>/README.md`.
- `README.md` describing the benchmark, task definitions, and evaluation metrics.
- `LICENSE` (Creative Commons Attribution 4.0 International).
- `CITATION.cff` for machine-readable citation.
- `.zenodo.json` for DOI archival on first GitHub release.
