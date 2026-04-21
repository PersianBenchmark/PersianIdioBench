# PersianIdioBench

**A Multi-Task Benchmark for Persian Idiom Understanding and Generation.**

This repository hosts the data and documentation for **PersianIdioBench**, a publicly released benchmark for evaluating NLP systems on Persian idiomatic expressions. The benchmark accompanies the paper:

> Hashempour R, Sutcliffe R, Chamberlain J (2026). *PersianIdioBench: A Multi-Task Benchmark for Persian Idiom Understanding and Generation.* Submitted to *PLOS ONE*.

---

## Background

Persian is spoken by more than 100 million people but remains under-resourced for idiom processing. Idiomatic expressions are non-compositional multi-word units whose meaning cannot be derived from their constituent words, which makes them a long-standing challenge for NLP systems. Prior Persian work has been limited to narrow tasks such as sentiment polarity or machine translation. PersianIdioBench provides a curated resource for three complementary tasks that probe idiom competence at the lexical, contextual, and discourse levels.

## Tasks

PersianIdioBench defines three tasks of increasing pragmatic difficulty:

1. **Connotation Classification** — predict the intrinsic evaluative polarity of a Persian idiom (`Positive` or `Negative`) from the idiom form and its Persian gloss.
2. **Appropriateness in Context** — binary classification distinguishing naturally occurring idiom usages from adversarial distractors constrained by polarity mismatch (`appropriate` or `inappropriate`).
3. **Cloze-Style Idiom Selection** — ranking task over ten candidate idioms for a masked paragraph position.

## Repository layout

```
PersianIdioBench/
├── README.md                          # this file
├── LICENSE                            # CC BY 4.0
├── CITATION.cff                       # machine-readable citation
├── CHANGELOG.md
├── .zenodo.json                       # metadata for Zenodo DOI archival
├── .gitignore
├── data/
│   ├── connotation/
│   │   ├── connotation.csv
│   │   └── README.md                  # data card
│   ├── appropriateness/
│   │   ├── appropriateness.csv
│   │   └── README.md                  # data card
│   └── cloze/
│       ├── cloze.csv
│       └── README.md                  # data card
```

## Datasets at a glance

| Task | File | Rows | Columns |
| --- | --- | ---: | --- |
| Connotation Classification | `data/connotation/connotation.csv` | 2,706 | `idiom`, `label`, `source`, `meaning` |
| Appropriateness in Context | `data/appropriateness/appropriateness.csv` | 5,089 | `idiom_in_text`, `correct_idiom`, `text`, `label` |
| Cloze-Style Idiom Selection | `data/cloze/cloze.csv` | 2,457 | `idiom`, `masked_text` |

Field-level descriptions, source provenance, label distributions, and the annotation protocol for each task are in the corresponding `data/<task>/README.md` (data card). All files are UTF-8 comma-separated CSVs.

## Evaluation metrics

For **Connotation** and **Appropriateness**, the paper reports Accuracy, Macro F1, Matthews Correlation Coefficient (MCC), and Cohen's κ. For **Cloze**, the paper reports Top-1 Accuracy and Mean Reciprocal Rank (MRR).

## Licensing

All data and documentation in this repository are released under the **Creative Commons Attribution 4.0 International License (CC BY 4.0)**. See `LICENSE` for the full legal text. Users may share and adapt the material for any purpose, including commercial use, provided that appropriate credit is given to the authors and the benchmark.

The underlying lexicographic sources (Abadis, Moein, Dehkhoda, Amid, Paarsadab, Dyanati, and previously published academic collections) remain the property of their respective authors. The gold connotation labels, adversarial distractors, masked contexts, and curated metadata in this repository are original contributions by the authors of PersianIdioBench.

## Citation

If you use PersianIdioBench in your research, please cite:

```bibtex
@article{hashempour2026persianidiobench,
  title   = {PersianIdioBench: A Multi-Task Benchmark for Persian Idiom Understanding and Generation},
  author  = {Hashempour, Reyhaneh and Sutcliffe, Richard and Chamberlain, Jon},
  journal = {PLOS ONE},
  year    = {2026},
  note    = {Under review}
}
```

A machine-readable citation is provided in `CITATION.cff`.

## Authors

- **Reyhaneh Hashempour** — corresponding author
- **Richard Sutcliffe**
- **Jon Chamberlain**

### CRediT author contributions

- **Reyhaneh Hashempour** — Conceptualization; Data curation; Formal analysis; Investigation; Methodology; Resources; Software; Validation; Visualization; Writing – original draft; Writing – review & editing.
- **Richard Sutcliffe** — Methodology; Supervision; Writing – review & editing.
- **Jon Chamberlain** — Methodology; Supervision; Writing – review & editing.

## Contact

Please open a GitHub issue for questions about the benchmark, bug reports, or requests for clarification on the data. For correspondence, see the paper.

## Changelog

See `CHANGELOG.md`.
