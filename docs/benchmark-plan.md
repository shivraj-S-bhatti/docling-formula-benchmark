# Benchmark Plan

Updated: 2026-06-18

## Benchmark Goal

Compare VLM and non-VLM formula extraction approaches for local/on-device scientific and educational document workflows.

Primary question:

> At what point does a tiny formula OCR model lose to a heavier model like CodeFormulaV2 or UniMERNet as formula complexity rises?

## Dataset Slices

Start with three practical slices:

| Slice | Expected difficulty | Examples |
| --- | --- | --- |
| Clean textbook | low | NCERT-style school math, clean crops, simple fractions/sums |
| MOOC/course notes | medium | slides, web PDFs, mixed prose/formulas |
| Dense engineering/scientific | high | NPTEL-style equations, matrices, nested fractions, line breaks |

Later additions:

- scanned PDFs
- handwritten formulas
- cropped/partial formulas
- formulas with equation numbers
- multi-line aligned equations
- matrices and cases environments

## Metrics

### 1. Architecture and On-device Efficiency

- **Time-to-first-token (TTFT):** delay before first generated token/character.
- **Tokens per second:** generation throughput.
- **Inference time per crop:** total model time.
- **Total parse time:** time to process 10-page and 50-page documents.
- **Peak RAM / VRAM:** max memory during inference.
- **Model size:** disk footprint and loaded memory.
- **Energy proxy:** sustained CPU/GPU utilization during 100-crop batch.

### 2. Syntactic and Structural Soundness

- **LaTeX compilation pass rate:** percent of generated formulas that compile/render.
- **Levenshtein distance:** character edit distance to ground truth.
- **Character error rate (CER):** edit distance normalized by target length.
- **BLEU-1 / BLEU-4:** token n-gram overlap for symbols and structural groups.
- **Render similarity:** visual similarity between source crop and rendered prediction.
- **Structure/nesting depth:** max fraction/matrix/subscript nesting parsed correctly.

### 3. Mathematical / Domain-specific Precision

- **Symbol recognition accuracy:** especially lookalikes like `\nu` vs `v`, `\times` vs `x`, `l` vs `1`.
- **Structural nesting boundary:** point where model starts dropping nested terms.
- **Dataset-segmented CER:** report separately for clean textbook, MOOC, and dense engineering.
- **Hard-case tags:** matrices, aligned equations, integrals, summations, piecewise functions.

### 4. Layout Behavior

- **Formula detection recall:** did the pipeline find the formula at all?
- **False positives:** prose/code mistaken for formula.
- **Crop quality:** did the crop include the whole formula without extra prose/equation numbers?
- **Inline vs display handling:** correct treatment of inline and standalone equations.
- **Equation-number handling:** excludes/handles equation numbers appropriately.
- **Reading order:** maintains row/column/order in multi-line formulas.

## Target Ranges

These are working targets, not claims.

- Clean textbook CER: less than 2%.
- Dense engineering CER: less than 8% initially.
- LaTeX compile pass rate: greater than 95% on clean data.
- 10-page local parse time: measured and reported; avoid any system that takes tens of minutes.
- Memory: fit comfortably alongside a document parser on a consumer laptop.

## Result Logging Schema

Use one row per `(crop, model)` pair.

See [`../experiments/results_template.csv`](../experiments/results_template.csv).

Required columns:

```text
crop_id,dataset_slice,source_doc,model_name,model_version,approach_family,
device,runtime,quantization,input_width,input_height,
ttft_ms,inference_time_ms,tokens_per_second,peak_ram_mb,peak_vram_mb,
predicted_latex,ground_truth_latex,compilation_valid,
levenshtein_distance,cer,bleu_1,bleu_4,render_similarity,
symbol_error_tags,structure_error_tags,layout_error_tags,notes
```

## First Experiment

1. Create 100 clean textbook crops, 100 MOOC crops, and 100 dense engineering crops.
2. Run CodeFormulaV2, Pix2Text-MFR, LaTeX-OCR/Pix2Tex, UniMERNet-S, and one tiny model like Texo if available.
3. Track accuracy, time, memory, compile pass, and failure tags.
4. Plot Pareto frontier: accuracy vs latency vs memory.
