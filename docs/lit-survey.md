# Literature Survey: Formula Extraction For Docling-like Pipelines

Updated: 2026-06-18

## Premise

Docling is useful because it is already an infrastructure layer for document conversion. It does layout, tables, formulas, code enrichment, and structured output. The research question is not whether formulas can be extracted at all. The question is:

> Which formula extraction approach is accurate enough, fast enough, small enough, and trustworthy enough for practical on-device Docling workflows?

## What Has Worked Well

### 1. Document parsers are becoming structured converters

Docling, MinerU, olmOCR, Dolphin, PaddleOCR, and related systems treat documents as structured artifacts: text blocks, tables, charts, formulas, reading order, and layout. This is stronger than classical OCR because the output is closer to Markdown, HTML, DocTags, or LaTeX.

### 2. Small document VLMs are viable

SmolDocling shows that a compact VLM can produce structured document output. CodeFormulaV2 shows that a roughly 300M model can run locally and handle code/formula image crops. GOT-OCR2.0 and PaddleOCR-VL point toward compact models that handle many document element types.

### 3. Formula-specific OCR is still competitive

Formula OCR does not have to be a general VLM. Specialized systems like LaTeX-OCR/Pix2Tex, Pix2Text-MFR, PP-FormulaNet, UniMERNet, Texo, and RapidLaTeXOCR can be smaller or faster because they only solve image-to-LaTeX.

### 4. Detection and recognition are different problems

FormulaNet is a useful reminder that formula extraction has at least two stages: mathematical formula detection and mathematical formula recognition. A perfect recognizer is not enough if the document parser misses inline formulas, crops display equations poorly, or includes equation numbers/prose in the crop.

### 5. Synthetic and mined data are central

SynthFormulaNet, SynthCodeNet, UniMER, PP-FormulaNet's mining system, and ChartNet show that large, controlled, checkable datasets matter. The key is not just scale. It is alignment between image, target markup, rendering, layout, and validation.

### 6. Verification is becoming a differentiator

Recent document OCR work increasingly uses compile/render checks, unit-test-like rewards, and structural constraints. For formulas, this suggests tracking whether generated LaTeX compiles and whether it renders similarly to the source crop.

## What Is Still Not Solved

- **Exact-match accuracy is not enough.** Equivalent LaTeX can render the same while differing textually.
- **Real PDFs are messy.** Equation numbers, line breaks, scans, fonts, cropped symbols, and low resolution remain difficult.
- **On-device practicality is under-measured.** A model that is accurate but slow is not useful for local document parsing.
- **Layout context matters.** Inline formulas, display equations, multi-line alignments, and nearby text all affect extraction.
- **Trust metadata is missing.** Downstream systems need compile/render status, confidence, alternatives, and failure tags.
- **Lean validation is narrow but valuable.** Lean cannot validate arbitrary LaTeX, but it can validate selected typed formulas/statements.

## Current Gap

A useful project is a review/benchmark comparing VLM and non-VLM formula extraction approaches for Docling-like systems, especially on-device. The benchmark should identify where CodeFormulaV2 or current SOTA is best, and where a smaller specialized model or hybrid cascade is cheaper, faster, or more reliable.

## Suggested Paper Framing

Working title:

> Formula Extraction for On-device Document Intelligence: A Review and Benchmark of VLM and Non-VLM Approaches

Possible contribution:

1. taxonomy of formula extraction approaches;
2. model/system comparison on local hardware;
3. practical metrics beyond accuracy: latency, memory, compile pass rate, and layout failure modes;
4. recommendations for Docling-like adapter design.

## Source Pointers

- Docling: https://github.com/docling-project/docling
- CodeFormulaV2: https://huggingface.co/docling-project/CodeFormulaV2
- SynthFormulaNet: https://huggingface.co/datasets/docling-project/SynthFormulaNet
- SmolDocling: https://arxiv.org/abs/2503.11576
- Texo: https://arxiv.org/abs/2602.17189
- PP-FormulaNet: https://arxiv.org/abs/2503.18382
- UniMERNet: https://arxiv.org/abs/2404.15254
- FormulaNet detection benchmark: https://ieeexplore.ieee.org/document/9869643
- General OCR Theory / GOT-OCR2.0: https://arxiv.org/abs/2409.01704
- Pix2Text: https://github.com/breezedeus/Pix2Text
- UniMERNet code: https://github.com/opendatalab/UniMERNet
- Texo code: https://github.com/alephpi/Texo
