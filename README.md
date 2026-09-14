# FFC-Dataset-10k

This repository contains the dataset and reproducibility resources for the paper:

**A Comparative Evaluation of Pretrained Face Embedding Models for Face Verification**

## Overview

FFC-Dataset-10k is a face image dataset created for the evaluation of pretrained face embedding models in face verification tasks.

The dataset contains **10,000 images from 5,000 identities**, constructed from images originating from seven publicly available face datasets.

The dataset was used to benchmark eleven pretrained face embedding models under a standardized evaluation pipeline.

## Source Datasets

FFC-Dataset-10k was constructed using images from the following datasets:

* Selfies-and-Videos
* Selfies-and-ID
* Pins-Face
* FEI-Face
* FaceScrub
* MORPH-2
* BUPT-CBFace-12

## Evaluated Models

The following pretrained face embedding models were evaluated:

* VGG-Face
* FaceNet
* FaceNet512
* OpenFace
* DeepFace
* DeepID
* ArcFace
* Dlib
* SFace
* GhostFaceNet
* Buffalo_L

All models were accessed through the DeepFace framework.

## Experimental Protocol

The evaluation pipeline consists of the following main steps:

1. Image resizing while preserving the original aspect ratio, with a maximum dimension of 640 pixels.
2. Face detection and alignment.
3. Face embedding extraction.
4. L2 normalization of the resulting embeddings.
5. Face verification using cosine distance.
6. Evaluation using ROC-AUC, Equal Error Rate (EER), Precision, Recall, and F1-score.

The experiments were conducted using five folds and four dataset sizes:

* 1,000 images
* 2,500 images
* 5,000 images
* 10,000 images

## Repository Structure

```text
FFC-Dataset-10k/
├── README.md
├── dataset/
├── notebooks/
└── results/
```

Additional files will be added to this repository as part of the reproducibility resources for the study.

## Reproducibility

The repository will contain the resources necessary to reproduce the dataset construction and evaluation experiments described in the paper, including the experimental notebook and information about the images selected from the source datasets.

## Citation

If you use this dataset or the associated evaluation pipeline, please cite the following paper:

**A Comparative Evaluation of Pretrained Face Embedding Models for Face Verification**

## License

The licensing and redistribution conditions of the original source datasets apply to the corresponding data included in this repository.
