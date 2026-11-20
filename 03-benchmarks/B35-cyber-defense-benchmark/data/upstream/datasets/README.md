# Datasets

The two files the public benchmark consumes ship as a single tracked archive,
`sample.zip` (~12 MB). The pipeline transparently unpacks it into
`sample.json` + `sample_flags.json` on first run; the unpacked JSONs are
gitignored. To force-unpack manually:

```bash
python -c "from benchmark.dataset_prep import ensure_unpacked; from pathlib import Path; ensure_unpacked(Path('datasets'))"
```

## `sample.json`

```json
{
  "briefing": "<generic threat briefing for the agent>",
  "seed": 176,
  "logs": [{"TimeCreated": "2026-01-14T00:06:46.532856Z", "EventID": 11, "...": "..."}, ...]
}
```

`sample.json` is the only file the public harness sees at run time.

## `sample_flags.json`

Opaque ground truth used **only** by `benchmark/scorer.py` and
`benchmark/make_plots.py`. Not visible to the agent.

```json
{
  "seed": 176,
  "tactic_ids": ["TA0001", "TA0002", "TA0003", "TA0011"],
  "chains": [
    {"chain_idx": 0, "steps": [{"step_idx": 1, "tactics": ["TA0003", "TA0004"]}]}
  ],
  "flags": [
    {"value": "2026-01-14T00:06:55.655856Z", "chain_idx": 0, "step_idx": 1, "narrative_steps": [4], "relevance": 2}
  ]
}
```

Each flag is a malicious-event timestamp tagged with its position in the
attack tree (`chain_idx`, `step_idx`) and the MITRE tactic ids covered at
that step. `narrative_steps` and `relevance` are diagnostic fields used by
the scorer.

## Full dataset

For the full multi-seed benchmark dataset, see the "Full dataset" section of
the root `README.md`.
