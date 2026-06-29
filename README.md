# Formula Extraction Benchmark

A small, public knowledge base for studying efficient mathematical formula extraction from scientific and educational documents.

The starting question is deliberately practical:

> For mathematical formula extraction, when is a small VLM like CodeFormulaV2 the right answer, and when is a lighter or more specialized non-VLM approach faster, cheaper, or more reliable on-device?

## Problem Frame

The problem is not "make formula OCR exist." The problem is bulk, reliable formula extraction under real constraints:

- local/on-device inference rather than expensive GPU services;
- clean and messy sources, from textbooks to MOOC slides to dense engineering PDFs;
- inline formulas, display equations, equation numbers, multilingual text, blurry scans, and low-resolution crops;
- outputs that are accurate, syntactically valid, and fast enough to use in real workflows.

Docling is a useful downstream integration target because it already has formula/code enrichment, but the research problem is broader than Docling.

## Three Plausible Directions

### 1. Review and Benchmark

Compare VLM and non-VLM formula extraction approaches on accuracy, latency, memory, LaTeX validity, and layout robustness.

This is the lowest-risk path and the best way to learn the field quickly.

### 2. Dataset and Evaluation Suite

Build a hard benchmark for under-served formula cases: inline formulas, blurry images, multilingual surrounding text, equation numbers, dense engineering matrices, and low-resolution crops.

This becomes valuable even before training a new model.

### 3. Efficient Formula Adapter / Model

Train or adapt a model that is SOTA on practical non-functional requirements: local latency, memory footprint, compile pass rate, and robustness at acceptable accuracy.

The likely winning system may be a hybrid cascade: PDF-native extraction first, small formula OCR second, VLM fallback only for hard cases.

## Current Hypothesis

The useful comparison should include:

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
- [`docs/project-options.md`](docs/project-options.md): three plausible project directions.
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
