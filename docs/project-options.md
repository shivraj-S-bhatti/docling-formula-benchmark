# Project Options

Updated: 2026-06-28

The problem space is efficient, trustworthy mathematical formula extraction from scientific and educational documents. Docling is a useful implementation target, not the central framing.

## Option 1: Review and Benchmark

**Question:** Which existing approach should someone use for formula extraction when accuracy, latency, memory, and local deployment all matter?

**Artifact:** A review paper plus benchmark comparing VLM and non-VLM approaches.

**Compare:**

- CodeFormulaV2, SmolDocling, Granite-Docling, GOT-OCR2.0
- Pix2Text-MFR, LaTeX-OCR/Pix2Tex, PP-FormulaNet, UniMERNet, Texo
- PDF-native extraction and hybrid cascades

**Metrics:**

- normalized LaTeX accuracy
- character error rate
- LaTeX compile/render pass rate
- time-to-first-token
- inference time per crop
- total parse time for 10-page and 50-page documents
- peak RAM/VRAM
- layout failures

**Why it is plausible:** Low training burden, publishable if the comparison is careful, and immediately clarifies what is actually missing.

**Risk:** It may become "just a survey" unless paired with real benchmark numbers.

## Option 2: Dataset and Evaluation Suite

**Question:** What formula cases are still poorly covered by current datasets and benchmarks?

**Artifact:** A curated formula extraction benchmark focused on hard practical slices.

**Open slices:**

- inline formulas
- blurry/low-resolution crops
- multilingual surrounding text
- equation numbers
- dense engineering matrices
- nested fractions and radicals
- multi-line aligned equations
- scanned textbook and MOOC material

**Why it is plausible:** Better data can be a real contribution even before training a model. It also makes any future adapter/model work more credible.

**Risk:** Dataset licensing and annotation quality need care.

## Option 3: Efficient Formula Adapter / Model

**Question:** Can we build a formula extraction system that is SOTA on practical non-functional requirements, not just accuracy?

**Artifact:** A small model or hybrid adapter optimized for local inference.

**Possible shape:**

1. PDF-native extraction when the formula is recoverable from the document.
2. Specialized formula OCR for ordinary formula crops.
3. VLM fallback for hard layout/context cases.
4. Render/compile validation and reranking.

**Target wins:**

- lower total parse time
- lower memory footprint
- high LaTeX compile pass rate
- competitive accuracy on hard slices
- robust inline/display/layout handling

**Why it is plausible:** The field has strong baselines, but practical deployment tradeoffs are still not cleanly solved.

**Risk:** Highest engineering and training burden. Should come after Option 1 or 2 gives evidence of a real gap.

## Recommended Sequence

1. Start with Option 1 to understand and compare existing approaches.
2. Use the failures from Option 1 to define Option 2.
3. Only pursue Option 3 after the benchmark shows where current systems fail.

This keeps the work forward-looking without pretending we already know the novel model contribution.
