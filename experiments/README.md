# Experiments

Keep experiments boring and reproducible.

## Suggested Workflow

1. Put crops in a local data directory that is not committed.
2. Run each model on the same crop IDs.
3. Save one row per crop/model pair using `results_template.csv`.
4. Commit only scripts, metadata, and small aggregate results unless data licenses allow sharing.

## Naming

Use:

```text
YYYY-MM-DD_model_dataset_slice.csv
```

Example:

```text
2026-06-18_codeformulav2_clean-textbook.csv
```

## Local Data

Do not commit raw copyrighted PDFs or private screenshots. Prefer derived metadata and links.

