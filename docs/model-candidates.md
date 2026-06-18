# Model Candidates

Updated: 2026-06-18

This is a living list. Claims should be verified before being used in the paper.

## Formula-focused Models

| Model | Type | Approx. size | Why compare it | Status |
| --- | --- | ---: | --- | --- |
| Texo | formula OCR | 20M | tiny model designed for browser/local inference; useful low-footprint baseline | verified paper/repo |
| PP-FormulaNet-S | formula OCR | 58M | high-speed small formula model from PaddleOCR family | verified paper |
| LaTeX-OCR / Pix2Tex | formula OCR | ~100M class | mature image-to-LaTeX baseline; easy deployment | needs exact size verification |
| Pix2Text-MFR | formula OCR inside Pix2Text | small/local | practical open-source math formula recognizer and Mathpix-like tool | verified repo, details TBD |
| UniMERNet-S | formula OCR | ~313M class | robust real-world mathematical expression recognition | verified paper/repo |
| RapidLaTeXOCR | formula OCR wrapper | depends on backend | ONNX-oriented formula OCR path; useful deployment baseline | candidate |
| TexTeller | formula OCR | TBD | community formula OCR model with strong generalization claims | candidate |

## Docling / Document VLM Models

| Model | Type | Approx. size | Why compare it | Status |
| --- | --- | ---: | --- | --- |
| CodeFormulaV2 | code/formula VLM adapter | ~300M | Docling-native formula/code baseline; runs on Mac according to project discussion | verified model card |
| SmolDocling | compact document VLM | 256M | Docling-native full-page document conversion to structured output | verified paper |
| Granite-Docling | document VLM | TBD | Docling family model; useful if available locally | candidate |
| GOT-OCR2.0 | unified OCR-2.0 | 580M | strong compact OCR baseline for text/formulas/tables/charts | verified paper |

## General Document OCR / Layout Systems

| System | Type | Why compare it | Status |
| --- | --- | --- | --- |
| Chandra OCR | document OCR/layout | handles complex tables/forms/handwriting and full layout; likely what "chardra-ocr" referred to | spelling corrected, details TBD |
| MinerU | document parser | strong open-source PDF extraction baseline | candidate |
| olmOCR / olmOCR 2 | document OCR | relevant for verifiable rewards and document-level OCR benchmark design | candidate |
| PaddleOCR / PaddleOCR-VL | OCR/document parser | efficient small-model family; PP-FormulaNet connection | candidate |
| Dolphin | document parser | compare full document parsing behavior if local model is usable | candidate |

## Non-VLM Approach Families

| Approach | Why it matters |
| --- | --- |
| PDF-native extraction | fastest when PDFs contain embedded glyph/text structure; avoids vision model when possible |
| specialized formula OCR | smaller/faster than general VLMs for image-to-LaTeX |
| symbol detection + structural parser | interpretable; can expose formula trees and layout failures |
| OCR + grammar/LaTeX repair | cheap baseline for simple formulas |
| render-and-rerank | uses LaTeX rendering to select visually closest candidate |
| hybrid cascade | PDF-native first, formula OCR second, VLM fallback for hard crops |

## Notes From Current Discussion

- CodeFormulaV2 is a VLM, but small enough to run locally on a MacBook Air according to Taru's test.
- The comparison should not assume VLM is always best.
- Time-to-parse is a core metric: accurate but slow systems are not practically useful.
- NCERT/MOOC/NPTEL-style dataset slices were proposed as useful difficulty levels: clean textbook, online course, and dense engineering formulas.

