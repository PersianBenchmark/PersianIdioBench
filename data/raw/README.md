# Raw Idiom Repository — Data Card

## Purpose

`raw_idioms.csv` is the starting inventory of PersianIdioBench. It is the cleaned, de-duplicated pool of Persian idioms from which all three downstream task datasets (Connotation, Appropriateness, Cloze) are derived. It is released so that researchers can reproduce the construction pipeline, audit source coverage, or build alternative tasks on the same vocabulary.

## File

`raw_idioms.csv` — UTF-8 encoded, comma-separated, with header row. 4,352 data rows.

## Schema

| Column | Type | Description |
| --- | --- | --- |
| `proverb` | string | Persian idiom in surface form (original orthography, including ZWNJ where applicable). |
| `normalized` | string | Normalised form used for de-duplication: lower-cased, ZWNJ stripped, diacritics removed, punctuation collapsed. |
| `source` | string | Provenance tag identifying the lexicographic source from which the idiom was drawn. |
| `tokens` | string | Whitespace-tokenised form of the normalised idiom, stored as a Python-style list literal (e.g. `['اب', 'از', 'دریا', 'بخشیدن']`). Useful for downstream tokenisation-aware matching. |

## Source distribution

| Source tag | Count | Description |
| --- | ---: | --- |
| `abadis_proverb` | 2,619 | Crawled from Abadis, an online Persian dictionary. |
| `moeen_idioms` | 1,112 | Extracted from the Moein Persian dictionary. |
| `ostovar_idioms` | 312 | Compiled from previously published academic lists (Ostovar and related collections). |
| `dyanati_proverb` | 256 | Parsed from the Dyanati educational website. |
| `paarsadab_proverb` | 51 | Parsed from the Paarsadab educational website. |
| `persian_idioms` | 2 | Residual entries retained after de-duplication against larger sources. |
| **Total** | **4,352** | |

## Construction protocol

Idioms were collected from the lexicographic and educational sources listed above and from previously published academic lists. Each entry was normalised (lower-casing, ZWNJ stripping, diacritic and punctuation removal) and de-duplicated both within and across sources. The cleaning pass identified 4,299 cross-source duplicate pairs and 123 hard duplicates within individual sources; merging and resolving these produced the final inventory of 4,352 unique idioms.

## Relation to the three task datasets

- **Connotation** — All 4,352 idioms were submitted for human polarity annotation. The released Connotation dataset (`data/connotation/connotation.csv`) contains the binary `Positive` / `Negative` subset used for evaluation.
- **Appropriateness** — Authentic usage contexts were mined for the 4,352 idioms across newspapers (Hamshahri, Tasnim, Asriran, Tarjoman), social and emotion corpora (EmoPars, ParsABSA, DeepSentiPers, ArmanEmo) and forum data (including Ninisite, a Persian equivalent of Reddit). Even with this diverse mix of sources, only 839 of the 4,352 idioms had at least one genuinely idiomatic occurrence after automatic verification with GPT-4o-mini and a minimum-length filter, because dictionary-listed idioms are long-tail by nature and a substantial share are archaic, regional or dialectal. These 839 idioms produced 3,425 validated idiom–context pairs, which were then expanded with polarity-mismatched distractor substitutions to form the Appropriateness dataset.
- **Cloze** — The Cloze dataset is a subset of the 3,425 Appropriateness contexts, restricted to those in which the idiom appears as an exact contiguous canonical string for unambiguous masking.

## Intended use

`raw_idioms.csv` is intended as a reference vocabulary and provenance record. It is *not* a labelled task dataset: the only column with task-relevant information is the source tag. Researchers building new Persian idiom resources are encouraged to use it as a controlled idiom pool and to credit the underlying lexicographic sources.

## Known limitations

- The repository over-represents formal lexicographic Persian and under-represents colloquial, regional, and Dari/Tajik variants.
- Surface forms are recorded as listed in their source; minor orthographic variants of the same idiom may persist where the normalisation pass could not unify them safely.
- The `tokens` column reflects a simple whitespace tokenisation over the normalised form and is not a linguistic morphological analysis.

## License

Released under Creative Commons Attribution 4.0 International (CC BY 4.0). See `/LICENSE` at the repository root. The underlying lexicographic sources (Abadis, Moein, Dehkhoda, Amid, Paarsadab, Dyanati, and previously published academic collections) remain the property of their respective authors; the curated, de-duplicated, normalised release in this file is an original contribution by the authors of PersianIdioBench.

## Citation

See the top-level `README.md` and `CITATION.cff`.
