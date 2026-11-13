# FFC-10k — Reported benchmark results

> **Source of truth:** Tables I and II of *A Comparative Evaluation of Pretrained Face Embedding Models for Face Verification*, presented at **SIBGRAPI 2026 / Workshop of Undergraduate Works (WUW)**. These figures are transcribed from the authors' research manuscript; they have **not been independently reproduced in this repository**. The public notebook illustrates the ArcFace pipeline, not the full 11-model grid.

## Evaluation configuration

| Setting | Value |
| :--- | :--- |
| Dataset | FFC-10k: 10,000 face images, 5,000 identities (2 images per identity) |
| Source datasets | 7 public face datasets, with access restrictions determined by their owners |
| Evaluation sizes | 1,000, 2,500, 5,000, 10,000 images |
| Repeated evaluations | Five folds (randomly sampled subsets) |
| Common face preprocessing | Resize to max width of 640 px, RetinaFace detection and alignment |
| Embeddings | Eleven pretrained models accessed through the DeepFace framework |
| Matching | Cosine distance, genuine vs. impostor pairs |
| Verification metrics | ROC-AUC, EER, precision, recall, F1 |
| Hardware for extraction timings | Intel Core i7-13700H, 16 GB RAM, NVIDIA RTX 4050 laptop GPU, Windows 11 Home |
| Timing convention | Sequential inference, one image at a time; 10,000 images; not production throughput |

## Full results — 10,000-image evaluation

| Model | ROC-AUC ↑ | EER ↓ | Precision ↑ | Recall ↑ | F1 ↑ | Embedding dim. | Extraction (hh:mm:ss) |
| :--- | ---: | ---: | ---: | ---: | ---: | ---: | ---: |
| VGG-Face | 0.9935 | 2.64% | 0.7585 | 0.5520 | 0.6390 | 4096 | 00:28:14 |
| FaceNet | 0.9980 | 1.60% | 0.8977 | 0.7146 | 0.7958 | 128 | 00:53:25 |
| FaceNet512 | 0.9980 | 1.03% | 0.8977 | 0.7146 | 0.7958 | 512 | 00:57:45 |
| OpenFace | 0.8963 | 18.76% | 0.0451 | 0.0356 | 0.0398 | 128 | 00:42:02 |
| DeepFace | 0.8038 | 27.14% | 0.2035 | 0.0808 | 0.1157 | 4096 | 06:22:17 |
| DeepID | 0.8963 | 18.76% | 0.0451 | 0.0356 | 0.0398 | 160 | 00:28:26 |
| ArcFace | 0.9978 | 1.34% | 0.9087 | 0.7422 | 0.8170 | 512 | 00:46:19 |
| Dlib | 0.9917 | 4.52% | 0.6393 | 0.3452 | 0.4483 | 128 | 01:26:13 |
| SFace | 0.9676 | 8.90% | 0.6868 | 0.3776 | 0.4873 | 128 | 00:32:23 |
| GhostFaceNet | 0.9856 | 5.30% | 0.7116 | 0.4926 | 0.5822 | 512 | 00:48:40 |
| Buffalo L | 0.7411 | 32.44% | 0.0486 | 0.0142 | 0.0220 | 512 | 05:02:53 |

[Download the machine-readable CSV](benchmark_results_10k.csv).

**Interpreting the results:**

- **ArcFace** achieved the **highest F1-score (0.8170)** and the highest precision (0.9087) in this benchmark; its EER was **1.34%**.
- **FaceNet512** had the **lowest EER (1.03%)** in the reported table; both FaceNet variants had the highest reported ROC-AUC (0.9980). Thus, calling any single model *best on every metric* would be incorrect.
- **Execution time is not production latency.** These are cumulative times to extract 10,000 image embeddings under the specific sequential hardware/software setup.
- **Embedding dimension does not determine quality.** All of ArcFace, FaceNet512, GhostFaceNet, and Buffalo L produce 512-dimensional vectors but differ substantially in measured performance.
- **Lower-scoring models require caution.** Differences may reflect model integration, normalization, detection or preprocessing details; this experiment does not isolate each cause.
- **Verification metrics depend on pair construction and thresholds.** F1 and precision should not be interpreted as deployment-wide false accept/reject guarantees.

## Provenance and limitations

The reported metrics are quoted from a research manuscript and should be considered **results for this particular FFC-10k evaluation protocol**, not a universal leaderboard or a production deployment claim. The manuscript reports fold-based experiments but this table shows its summarized 10,000-image metrics (not per-fold scores). Do not infer confidence intervals from this table.

This repository currently publishes:
- image selection metadata (`selected_images.csv`);
- a single-model reference notebook (`ArcFace-embeddings-v4.ipynb`);
- this summary and CSV, transcribed from the manuscript.

The repository does **not** currently publish all pretrained model weights, source images, a turnkey 11-model reproduction script, or per-fold result files. Model and data licensing terms apply.

## Research context

**Study:** *A Comparative Evaluation of Pretrained Face Embedding Models for Face Verification*. Co-authored and presented at **SIBGRAPI 2026 / WUW** by João Gabriel Gralha and collaborators.

**Institutional source:** [CEIA-NoLeakIV / FFC-Dataset-10k](https://github.com/CEIA-NoLeakIV/FFC-Dataset-10k).

**Separate related project:** The CEIA-UFG team's NIST FRTE 1:1 submission is a **separate model evaluation**. The results in this file are **not NIST results**.
