# BRIDGE, ICLR 2027 submission

LaTeX source for *BRIDGE: label-free cyclic data repair for self-supervised
learning*, split out of the experiment repository at
`github.com/Thiggel/FOMO` with the history of `paper_work/iclr_bridge_2027`
preserved.

## Building

```
latexmk -pdf bridge_iclr_2027.tex
```

Run it twice on a clean checkout so the table and figure references resolve.

## Where the numbers come from

Nothing in `tables/` should be edited by hand. Every file there is written by a
script in the experiment repository, which reads `result.json` from the run
checkpoints and refuses to average a row whose seeds are not all present. Two
mutually inconsistent SimCLR rows once reached a submitted version because the
tables were transcribed by hand, which is the reason for the arrangement.

From a checkout of the experiment repository, with the run checkpoints
available:

```
PYTHONPATH=$PWD python scripts/generate_iclr_tables.py \
  --checkpoint-root <checkpoints> --tables-dir <this repo>/tables

PYTHONPATH=$PWD python scripts/make_main_generalization_panel.py \
  --full-table <this repo>/tables/main_generalization_vits_full_linear.tex \
  --out <this repo>/tables/main_generalization.tex

PYTHONPATH=$PWD python scripts/make_main_policy_table.py \
  --full-table <this repo>/tables/main_policy_repair_controls_full_linear.tex \
  --out <this repo>/tables/main_policy_repair_controls.tex
```

The first command prints how many rows of each table are complete and warns when
two rows of a table resolve to identical numbers on every dataset, which is what
exposed a checkpointing fault that had made two conditions share an encoder.

The ablation tables for pretraining, generation, selection, cycles and
architecture predate this arrangement. They were produced for the NeurIPS
submission by `scripts/generate_neurips_paper_tables.py` from an exported CSV
that is no longer in the repository, so they cannot currently be regenerated.

## Layout

| path | contents |
| --- | --- |
| `bridge_iclr_2027.tex` | the manuscript |
| `tables/` | generated result tables, one file per table and protocol |
| `figures/` | figures |
| `references.bib`, `iclr2027_conference.bib` | bibliography |
| `REVISION_PLAN.md`, `REVIEWER_RISK_AUDIT.md`, `BACKGROUND_AUDIT.md` | working notes carried over from the resubmission |
