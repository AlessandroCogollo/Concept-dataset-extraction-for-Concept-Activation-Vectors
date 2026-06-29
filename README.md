# Concept Dataset Extraction for CAVs

## Overview
This repository contains the research pipeline and experiments developed for the Master's Thesis: "Concept dataset extraction for Concept Activation Vectors: A study on open-vocabulary grounding and segmentation."
The project focuses on automating the generation of concept datasets to compute Concept Activation Vectors (CAVs), addressing the bottleneck of manual data collection by leveraging open-vocabulary models (SAM3).

## Pipeline Architecture
The pipeline follows a modular architecture described in §3.2 of the thesis:
1. **Extractor:** Utilizes zero-shot segmentation models to ground concepts from textual prompts.
2. **Cropper:** Applies multiple cropping policies (bbox, center_mask, sliding_window, largest_bbox) to isolate the concept
3. **Augmenter:** Performs data augmentation to enhance the robustness of the resulting datasets.

## Repository Structure
The repository is organized into experimental notebooks that map directly to the thesis chapters:

- `extraction-pipeline-deliverable-4.ipynb`: Core architecture; manages extraction and preprocessing on ImageNet.
- `experiment-1-1-intrinsic-evaluation-deliverable-2.ipynb`: Intrinsic quality assessment using VLM-as-judge (Qwen2-VL).
- `experiment-1-2-stability-and-robustness-delivera-4.ipynb`: Analysis of CAV stability across configurations.
- `experiment-2-1-cavs-similarity-deliverable.ipynb`: Cross-source similarity study.
- **Ablation Studies:**
  - `ablation-4-3-2-4-3-3.ipynb`: Comparison of cropping policies and augmentation strategies.
  - `ablation-4-3-6-campi-comparison.ipynb`: Comparative benchmark against the generative pipeline by Campi et al. (CVPRW 2025).

## Prerequisites & Optimization
The codebase is optimized for GPU-accelerated environments (tested on NVIDIA Tesla T4, 16GB VRAM).
Memory Management: To avoid CUDA fragmentation when running SAM3, we utilize:
`os.environ["PYTORCH_CUDA_ALLOC_CONF"] = "expandable_segments:True"`
Authentication: Ensure your `HF_TOKEN` is configured in the environment/Kaggle Secrets to download the SAM3 weights.

## Utilizzo
1. Configuration: Adjust the `DatasetConfig` parameters in the extraction notebook.
2. Extraction: Run the pipeline to generate the concept datasets.
3. Evaluation: Execute the experiment-*.ipynb notebooks to reproduce the quantitative results and tables presented in Chapter 4 of the thesis.

## Credits
- **Author:** Alessandro Cogollo (233022)
- **Advisor:** Prof. Marco Brambilla
- **Co-advisors:** A. De Santis, M. Bianchi, R. Campi
- **Academic Year:** 2025-2026