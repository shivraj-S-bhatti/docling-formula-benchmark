# Docling Formula Benchmark

A small, public knowledge base for studying formula extraction in Docling-like document pipelines.

The starting question is deliberately practical:

> For mathematical formula extraction, when is a small VLM like CodeFormulaV2 the right answer, and when is a lighter or more specialized non-VLM approach faster, cheaper, or more reliable on-device?

## Current Hypothesis

Docling already has formula extraction, so the gap is not "make formula OCR exist." The useful contribution is a simple benchmark and literature-backed comparison across:

- VLM formula/code adapters, such as CodeFormulaV2
- compact document VLMs, such as SmolDocling and Granite-Docling
- formula-specialized OCR models, such as Pix2Text-MFR, LaTeX-OCR/Pix2Tex, PP-FormulaNet, UniMERNet, and Texo
- document OCR/layout systems, such as Chandra OCR, MinerU, olmOCR, PaddleOCR, and related parsers
- hybrid approaches, such as PDF-native extraction first, formula OCR second, VLM fallback only for hard cases

## What We Want To Measure

The benchmark should care about real use, not just leaderboard accuracy.

- **Accuracy:** normalized LaTeX match, edit distance, CER, BLEU, symbol accuracy, structural nesting.
- **Syntactic validity:** LaTeX compilation/render pass rate.
- **Speed:** time-to-first-token, total inference time, formulas/second, seconds/page, time to parse 10-page/50-page PDFs.
- **On-device footprint:** model size, peak RAM/VRAM, CPU/MPS latency, energy proxy.
- **Layout behavior:** formula detection recall, inline vs display formulas, multi-line equations, equation numbers, reading order.
- **Trust:** render similarity, confidence calibration, abstention quality, validation metadata.

## Repository Map

- [`docs/lit-survey.md`](docs/lit-survey.md): compressed literature survey and field map.
- [`docs/model-candidates.md`](docs/model-candidates.md): candidate models/systems to compare.
- [`docs/benchmark-plan.md`](docs/benchmark-plan.md): metrics, targets, dataset slices, and logging schema.
- [`docs/paper-roadmap.md`](docs/paper-roadmap.md): simple plan for a review/benchmark paper.
- [`experiments/results_template.csv`](experiments/results_template.csv): starting CSV schema for benchmark runs.
- [`briefs/`](briefs/): shareable two-page conversation brief.
- [`whitepaper/`](whitepaper/): longer steering draft.

## First Milestone

Build a tiny benchmark harness:

1. collect 100-500 formula crops across clean textbook, MOOC, and dense engineering/scientific material;
2. run 3-5 candidate models locally;
3. log accuracy, syntactic validity, time, memory, and failure type;
4. report the Pareto frontier: accuracy vs latency vs memory vs trust.

## Status

Early research scratchpad. Expect notes to change as papers are read and experiments are run.

