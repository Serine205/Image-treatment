# A Comparative Study of RAG Techniques for Generating Image Captions — Multimodal RAG

**Image Processing Mini-Project — Group 13 — Phase 1: data exploration and pre-processing**

## Group 13 — Students

- SOUCHANE Serine
- SEBA Bouchra
- MERADI Serine Feriel
- AGGOUNE Abderrahim

## Project description

The mini-project compares Retrieval-Augmented Generation (RAG) techniques for image captioning on a subset of MS COCO 2017. RAG grounds caption generation in external evidence (similar images, reference captions, metadata) to reduce omitted or hallucinated objects. This submission contains the data-preparation phase: a clean, reproducible and frozen knowledge base on which the retrieval techniques operate.

## Project objectives

1. Audit and explore COCO 2017 (object classes, scene complexity, caption statistics, diversity).
2. Create frozen, disjoint splits (knowledge base, validation, test) with an anti-leakage control.
3. Pre-process images and captions, extract metadata (COCO annotations and an optional YOLO branch).
4. Generate CLIP embeddings and build exact FAISS indexes.
5. Validate the release (quality control and retrieval sanity check).

## Dataset

COCO 2017: 10,000 knowledge-base images and 100 validation images from `train2017`, test images from `val2017`; 50,028 captions; CLIP ViT-B/32 embeddings (512-d). Full description in [DATASET.md](DATASET.md). The COCO images and annotations are not included and must be downloaded from https://cocodataset.org/.

## Methodology / workflow

`audit_dataset.py` → `explore_dataset.py` → `create_splits.py` → `preprocess_images.py` → `preprocess_captions.py` → `extract_metadata.py` → `generate_embeddings.py` → `check_embeddings.py` → `build_knowledge_base.py` → `quality_control.py` → `validate_retrieval.py`

Optional YOLO branch: `pilot_yolo_100.py`, `experiment_yolo_thresholds.py`, `extract_yolo_10000.py`, `merge_yolo_metadata.py`. Fixed random seed: 42. Scripts use paths relative to the project root.

## Project structure

```
.
├── README.md
├── DATASET.md
├── requirements.txt
├── .gitignore
├── data/splits/      image-ID lists of the splits
├── scripts/          the 25 Python scripts of the pipeline
├── reports/          audit, exploration, quality control, retrieval validation, YOLO merge
├── figures/          figures used in the report
└── docs/             final report (PDF) and its LaTeX source
```

## Results

- Audit: 118,287 train2017 and 5,000 val2017 images, no missing or corrupted image (`reports/dataset_audit.json`).
- Quality control: 10/10 checks passed, no data leakage (`reports/quality_control_report.json`).
- Retrieval sanity check with the 100 validation images (`reports/validation/`).
- YOLO26n detections on the 10,000 images: 49,375 objects (`reports/yolo_metadata_merge_report.json`).

## Submission files

| Item | Location |
|---|---|
| Source code | `scripts/` |
| Dataset information | `DATASET.md`, `data/splits/` |
| Results | `reports/`, `figures/` |
| Final report | `docs/final_report.pdf` |

## Documentation

- [Dataset Description](DATASET.md)
- [Final Report](docs/final_report.pdf)

## Full project repository

Complete history and large artefacts (embeddings, FAISS indexes, metadata, stored with Git LFS): https://github.com/Serine205/rag-coco-image-captioning
