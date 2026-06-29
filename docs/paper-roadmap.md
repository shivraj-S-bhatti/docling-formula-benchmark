# Paper Roadmap

Updated: 2026-06-18

## Working Title

Formula Extraction for On-device Document Intelligence: A Review and Benchmark of VLM and Non-VLM Approaches

## Core Claim

Formula extraction is already usable in several systems, but practical deployments need a clear answer to:

> Which formula extraction approach should a developer choose when local speed, memory, accuracy, and trust all matter?

## Possible Paper Contributions

1. **Taxonomy:** VLM adapters, specialized formula OCR, PDF-native extraction, symbol-layout parsers, and hybrid cascades.
2. **Benchmark:** compare representative models across clean, medium, and dense formula slices.
3. **Metrics:** report not only accuracy, but time-to-parse, RAM/VRAM, compile pass rate, layout failures, and render similarity.
4. **Practical recommendation:** identify where CodeFormulaV2 is best and where smaller non-VLM models are cheaper/faster.
5. **Deployment perspective:** explain how a production document parser could route formulas through a cascade.

## Proposed Structure

1. Introduction and motivation
2. Background: formula extraction and document parsing
3. Taxonomy of approaches
4. Candidate models and systems
5. Benchmark design
6. Metrics and hardware setup
7. Results
8. Discussion: VLM vs non-VLM tradeoffs
9. Recommendations for efficient deployment and document-parser integration
10. Limitations and future work

## What Would Make This Useful

- It should be honest that formula extraction already exists.
- It should explain why on-device runtime matters.
- It should compare against CodeFormulaV2 rather than ignore it.
- It should include at least one non-VLM or specialized formula OCR baseline.
- It should show practical failure modes, not just aggregate scores.

## Open Questions

- Which exact datasets should represent NCERT, MOOC, and NPTEL-style difficulty?
- Which models can be run locally with reasonable setup effort?
- Can render similarity be automated robustly enough for a benchmark?
- Should Lean validation be included now or left as future work?
- What is the minimal benchmark size that still tells a useful story?
