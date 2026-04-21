# Changelog

All notable changes to PersianIdioBench are documented in this file.
The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.1.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.0.0] - 2026-04-21

### Added
- Initial public release of PersianIdioBench.
- Task 1 dataset: `data/connotation/connotation.csv` (2,706 idioms with gold evaluative-polarity labels).
- Task 2 dataset: `data/appropriateness/appropriateness.csv` (5,089 idiom-in-text pairs with binary appropriateness labels).
- Task 3 dataset: `data/cloze/cloze.csv` (2,457 masked paragraphs for cloze-style idiom selection).
- Per-task data cards under `data/<task>/README.md`.
- `README.md` describing the benchmark, task definitions, and evaluation metrics.
- `LICENSE` (Creative Commons Attribution 4.0 International).
- `CITATION.cff` for machine-readable citation.
- `.zenodo.json` for DOI archival on first GitHub release.
