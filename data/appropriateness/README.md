# Appropriateness in Context — Data Card

## Task

Binary classification: given a Persian paragraph containing an idiom, decide whether that idiom is used appropriately in the given context (`appropriate`) or whether it has been substituted with a distractor idiom whose evaluative polarity is mismatched (`inappropriate`). This probes context-sensitive idiom interpretation beyond lexical polarity.

## File

`appropriateness.csv` — UTF-8 encoded, comma-separated, with header row. 5,089 data rows.

## Schema

| Column | Type | Description |
| --- | --- | --- |
| `idiom_in_text` | string | The idiom that actually appears inside the `text` field. |
| `correct_idiom` | string | The idiom originally observed in this context (i.e., the naturally occurring idiom for this passage). |
| `text` | string | A Persian paragraph drawn from news or social media corpora, with `idiom_in_text` present in the passage. |
| `label` | string | `appropriate` if `idiom_in_text == correct_idiom`; `inappropriate` if `idiom_in_text` is an adversarial distractor swapped in to replace `correct_idiom`. |

## Label distribution

| Label | Count | Proportion |
| --- | ---: | ---: |
| `inappropriate` | 2,632 | 51.7 % |
| `appropriate` | 2,457 | 48.3 % |

The dataset is approximately balanced by construction: each naturally-occurring `(correct_idiom, text)` pair is paired with at least one adversarial variant where the idiom has been replaced by a distractor whose polarity is opposite (so the swap is detectable in principle from context-polarity alignment, not from surface form alone).

## Construction

- **Positive (`appropriate`) instances** are extracted from naturally-occurring Persian text where the idiom was observed in situ (news articles, social-media posts). See the paper for corpus provenance and filtering rules.
- **Negative (`inappropriate`) instances** are constructed by replacing the observed idiom with a distractor idiom drawn from the PersianIdioBench repository, selected under the constraint that the distractor's gold polarity is opposite to that of `correct_idiom`. This ensures the task requires contextual reasoning rather than simple string matching.

## Intended use

Evaluates pragmatic competence with idioms: a system must determine whether the *meaning* of the present idiom fits the surrounding discourse, not merely whether it is grammatically well-formed.

## Known limitations

- Distractors are drawn only from the Positive/Negative subset of the PersianIdioBench repository; idioms without a gold polarity label cannot appear as distractors.
- Text snippets are single paragraphs and may not capture longer-range discourse cues.
- Some passages may contain other idiomatic material that is not annotated.

## Evaluation

The paper reports Accuracy, Macro F1, Matthews Correlation Coefficient (MCC), and Cohen's κ on a held-out test split.

## License

Released under Creative Commons Attribution 4.0 International (CC BY 4.0). See `/LICENSE` at the repository root.

## Citation

See the top-level `README.md` and `CITATION.cff`.
