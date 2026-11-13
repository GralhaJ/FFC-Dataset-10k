# Reproducibility guide

This project documents the dataset selection metadata and an **ArcFace-based example** of a face-verification experiment. **It does not claim to be an executable reproduction of all 11 published model comparisons.**

## Repository contents

| File | Purpose |
| :--- | :--- |
| [`selected_images.csv`](selected_images.csv) | Selection/mapping metadata for the curated FFC-10k collection |
| [`ArcFace-embeddings-v4.ipynb`](ArcFace-embeddings-v4.ipynb) | Reference notebook demonstrating an ArcFace-based embedding/evaluation workflow |
| [`BENCHMARK_RESULTS.md`](BENCHMARK_RESULTS.md) | Research protocol and metrics, carefully attributed to the manuscript |
| [`benchmark_results_10k.csv`](benchmark_results_10k.csv) | Machine-readable transcription of the paper's 10k-image performance/timing tables |

## Data preparation

The FFC-10k dataset has **10,000 selected images of 5,000 identities**, assembled from seven existing datasets: Selfies-and-Videos, Selfies-and-ID, Pins-Face, FEI-Face, FaceScrub, MORPH-2, and BUPT-CBFace-12.

1. Consult the **[institutional construction guide](https://github.com/CEIA-NoLeakIV/FFC-Dataset-10k)**.
2. Independently obtain each source dataset from its owner, subject to availability, permission, terms, and licenses. **Images are not hosted in this repository.**
3. Follow the institutional guide's folder naming and data construction instructions. Use [`selected_images.csv`](selected_images.csv) to understand the selection metadata.
4. Validate that the reconstructed identities and pairs align with your experiment. If a dataset is unavailable or differs, the reported numbers should **not** be assumed reproducible.

## Evaluating ArcFace

1. Set up a **Python/Jupyter environment** with the dependencies required by the current notebook. Dependency versions are **not pinned or independently tested** here; read the notebook's import and installation cells before executing.
2. Open [`ArcFace-embeddings-v4.ipynb`](ArcFace-embeddings-v4.ipynb) and adjust **all data, model-cache, and output paths** for your own machine. It may include environment-specific settings.
3. Prepare face images and class identifiers consistently with the notebook's preprocessing and pairing logic.
4. Run the cells and inspect intermediate outputs, normalized embeddings, genuine/impostor distance distributions, and evaluation metrics.
5. Compare results with the reported paper values **only if** your dataset, preprocessing, pair sampling, threshold selection, and software environment are equivalent.

## Methodology of the published comparison

```mermaid
flowchart LR
    A["FFC-10k image selection"] --> B["Resize (max width 640 px)"]
    B --> C["RetinaFace detection + alignment"]
    C --> D["Pretrained embedding models (11)"]
    D --> E["Embedding vectors"]
    E --> F["Genuine / impostor pairs"]
    F --> G["Cosine distance"]
    G --> H["ROC-AUC, EER, Precision, Recall, F1"]
```

The research compared **four subset sizes** (1k, 2.5k, 5k, 10k images) across **five evaluations**, using the same face preprocessing and verification procedure to reduce variation. The benchmark times reflect sequential extraction on a Lenovo laptop with an RTX 4050; do not reinterpret these as optimized serving throughput.

## Scope and ethics

- The dataset is intended for academic verification benchmarking. Face recognition has biometric privacy and bias implications; use appropriate permissions, evaluations, and safeguards.
- Dataset composition may not represent populations or scenarios found in production.
- The research manuscript itself notes that weak performance of some models may be affected by integration and preprocessing choices.
- The NIST FRTE 1:1 submission by the broader CEIA team is **not** the benchmark presented here.
- No license is asserted here for third-party source images or pretrained weights.

For evaluation numbers, read [`BENCHMARK_RESULTS.md`](BENCHMARK_RESULTS.md) and the related SIBGRAPI 2026 research manuscript.
