# Connotation Classification — Data Card

## Task

Predict the intrinsic evaluative polarity of a Persian idiom in isolation, given the surface form and a Persian gloss. This probes whether a model has learned the affective/connotative content that idioms typically carry independently of surrounding context.

## File

`connotation.csv` — UTF-8 encoded, comma-separated, with header row. 2,706 data rows.

## Schema

| Column | Type | Description |
| --- | --- | --- |
| `idiom` | string | Persian idiom in surface form (original orthography, with ZWNJ where applicable). |
| `label` | string | Gold evaluative polarity. One of `Positive`, `Negative`. |
| `source` | string | Provenance tag identifying the lexicographic source from which the idiom was drawn. |
| `meaning` | string | Persian gloss / definition of the idiom. |

## Label distribution

| Label | Count | Proportion |
| --- | ---: | ---: |
| Negative | 2,155 | 79.6 % |
| Positive | 551 | 20.4 % |

The label distribution is skewed toward `Negative`, reflecting a known tendency in idiomatic lexicons for negatively-valenced expressions to outnumber positive ones. Evaluation in the paper uses Macro-F1, MCC, and Cohen's κ in addition to Accuracy to control for this class imbalance.

## Source distribution

| Source tag | Count |
| --- | ---: |
| `abadis_proverb` | 1,839 |
| `moeen_idioms` | 461 |
| `ostovar_idioms` | 193 |
| `dyanati_proverb` | 181 |
| `paarsadab_proverb` | 30 |
| `persian_idioms` | 2 |

## Annotation protocol

Two native Persian speakers independently annotated each idiom for evaluative polarity using a binary `Positive` / `Negative` scheme, based on the idiom and its gloss. Disagreements were adjudicated by discussion. Inter-annotator agreement before adjudication was Cohen's κ = 0.68, which indicates substantial agreement under Landis and Koch (1977).

## Intended use

The connotation task is designed as a lexical-semantic probe. Systems are expected to predict polarity from the idiom and gloss alone, without external context.

## Known limitations

- Class imbalance (see above).
- A small number of idioms have polysemous readings whose polarity is context-dependent; these were labelled with the majority polarity as judged by the annotators.
- Labels reflect modern Iranian Persian usage; polarities may differ for Dari or Tajik Persian.

## License

Released under Creative Commons Attribution 4.0 International (CC BY 4.0). See `/LICENSE` at the repository root.

## Citation

See the top-level `README.md` and `CITATION.cff`.
