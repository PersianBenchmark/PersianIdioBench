# Cloze-Style Idiom Selection — Data Card

## Task

Given a Persian paragraph with an idiom position masked, rank a set of ten candidate idioms and select the one that fills the masked position correctly. This is the most pragmatically demanding of the three PersianIdioBench tasks: it requires joint reasoning over discourse content, evaluative polarity, and idiom-level semantic fit.

## File

`cloze.csv` — UTF-8 encoded, comma-separated, with header row. 2,457 data rows.

## Schema

| Column | Type | Description |
| --- | --- | --- |
| `idiom` | string | The gold idiom that was observed in the original (unmasked) paragraph — the correct answer. |
| `masked_text` | string | The Persian paragraph with the idiom position replaced by a mask token. |

## Candidate construction

The paper evaluates Cloze-Style Idiom Selection as a ten-way ranking task. At evaluation time, each item is presented with the gold idiom and nine distractors drawn from the PersianIdioBench repository. The specific sampling rule used in the paper (matched-length, polarity-controlled distractors with a fixed seed) is documented in §Experimental setup and can be reproduced from this file plus the connotation dataset.

For users who want to evaluate with a different distractor scheme (e.g., random negatives, hard negatives by embedding similarity, or a larger candidate pool), the gold idiom is the `idiom` column and the full candidate pool can be drawn from `data/connotation/connotation.csv`.

## Intended use

The cloze task tests whether a model can identify the idiomatic expression whose meaning best completes a paragraph. Success requires aligning discourse-level polarity, lexical-semantic fit, and pragmatic felicity with the correct expression.

## Known limitations

- Single-idiom cloze per paragraph; paragraphs with multiple idioms are either filtered or only one position is masked.
- The masked token does not encode morphological agreement cues that may otherwise narrow the candidate set.
- Paragraph length varies; longer paragraphs may provide stronger discourse cues.

## Evaluation

The paper reports Top-1 Accuracy and Mean Reciprocal Rank (MRR) over ten-way candidate ranking.

## License

Released under Creative Commons Attribution 4.0 International (CC BY 4.0). See `/LICENSE` at the repository root.

## Citation

See the top-level `README.md` and `CITATION.cff`.
