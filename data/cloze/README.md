# Cloze-Style Idiom Selection — Data Card

## Task

Given a Persian paragraph with an idiom position masked, rank a set of candidate idioms and select the one that fills the masked position correctly. This is the most pragmatically demanding of the three PersianIdioBench tasks: it requires joint reasoning over discourse content, evaluative polarity, and idiom-level semantic fit.

## File

`cloze.csv` — UTF-8 encoded, comma-separated, with header row. 2,211 data rows covering 597 unique gold idioms.

## Schema

| Column | Type | Description |
| --- | --- | --- |
| `idiom` | string | The gold idiom observed in the original (unmasked) paragraph — the correct answer for the cloze position. |
| `masked_text` | string | The Persian paragraph with the idiom position replaced by a mask token. |
| `candidates` | string (Python-list literal) | A stringified Python list of ten distractor idioms drawn from the PersianIdioBench repository. The gold idiom is **not** included in this list. |

## Loading `candidates` correctly

The `candidates` column is stored as a Python-list literal (for example: `['از چاله به چاه افتادن', 'درجا زدن', ...]`). Parse it safely with `ast.literal_eval`:

```python
import pandas as pd
import ast

df = pd.read_csv("cloze.csv")
df["candidates"] = df["candidates"].apply(ast.literal_eval)

row = df.iloc[0]
row["idiom"]         # gold idiom (string)
row["masked_text"]   # paragraph with masked position (string)
row["candidates"]    # list of 10 distractor idioms
```

Using `eval` is discouraged; `ast.literal_eval` is safe because it only accepts Python literals.

## Candidate pool and evaluation protocol

Each row contains the gold idiom in the `idiom` column and ten distractor idioms in the `candidates` column. At evaluation time, the candidate pool is kept at exactly ten by **replacing one of the distractors with the gold idiom**, so the model ranks a ten-way pool consisting of nine distractors and the gold.

A minimal reference implementation:

```python
import ast, random
import pandas as pd

df = pd.read_csv("cloze.csv")
df["candidates"] = df["candidates"].apply(ast.literal_eval)

def build_pool(row, rng):
    pool = list(row["candidates"])        # 10 distractors
    swap_idx = rng.randrange(len(pool))   # pick one slot uniformly at random
    pool[swap_idx] = row["idiom"]         # replace it with the gold
    return pool, swap_idx                 # swap_idx is the gold's position

rng = random.Random(42)  # fixed seed for reproducibility
df[["pool", "gold_index"]] = df.apply(
    lambda r: pd.Series(build_pool(r, rng)), axis=1
)
```

The resulting `pool` is a ten-way ranking task; the correct answer is at `gold_index`. Use Top-1 Accuracy and Mean Reciprocal Rank (MRR) as the evaluation metrics. Use a fixed random seed when reporting results so scores are comparable across systems and runs.

## Intended use

The cloze task tests whether a model can identify the idiomatic expression whose meaning best completes a paragraph. Success requires aligning discourse-level polarity, lexical-semantic fit, and pragmatic felicity with the correct expression.

## Known limitations

- Single-idiom cloze per paragraph; paragraphs with multiple idioms are either filtered or only one position is masked.
- The mask token does not encode morphological agreement cues that may otherwise narrow the candidate set.
- Paragraph length varies; longer paragraphs may provide stronger discourse cues than shorter ones.
- The same gold idiom may appear in multiple rows with different masked paragraphs (the file covers 597 unique idioms across 2,211 rows).

## Evaluation

The paper reports Top-1 Accuracy and Mean Reciprocal Rank (MRR).

## License

Released under Creative Commons Attribution 4.0 International (CC BY 4.0). See `/LICENSE` at the repository root.

## Citation

See the top-level `README.md` and `CITATION.cff`.
