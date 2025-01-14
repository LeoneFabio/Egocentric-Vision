# Bridging Vision and Language: NLQ with Textual Answer Generation

## Table of Contents

- [Introduction](#introduction)
- [Project Structure](#project-structure)
- [Usage](#usage)
  - [Running the Notebook](#running-the-notebook)
  - [Results and Outputs](#results-and-outputs)
- [Models and Features](#models-and-features)
- [Contributions](#contributions)
- [Collaborations](#collaborations)
- [Report](#report)
- [Acknowledgments](#acknowledgments)

---

## Introduction

Egocentric video analysis, as exemplified by the Ego4D dataset, captures complex human activities from a first-person perspective. However, the dataset poses challenges due to its unstructured and untrimmed nature. The **Natural Language Query (NLQ)** benchmark identifies temporal segments answering specific queries but requires manual review of these intervals.

To address this limitation, this project proposes a pipeline that:
1. Employs **temporal localization models** (VSLBase, VSLNet, 2D-TAN) to predict video timestamps relevant to user queries.
2. Integrates timestamp predictions with the **Video-LLaVA VideoQA model**, transforming video segments into actionable textual answers.

This pipeline optimizes computational efficiency while maintaining detail and usability, paving the way for applications in episodic memory retrieval, assistive technologies, and advanced video understanding.

---

## Project Structure

```
Egocentric-Vision/
├── Egocentric_Vision.ipynb       # Main notebook implementing the methodology
├── nlq_files/                    # Contains NLQ dataset splits and analysis plots
├── temporal_localization_files/  # Outputs and results related to temporal localization models
├── video_LLaVa_files/            # Outputs and results related to Video-LLaVa
├── Bridging_Vision_and_Language__NLQ_with_Textual_Answer_Generation.pdf #Report
```

## Usage

### Running the Notebook

1. Open the `Egocentric_Vision.ipynb` notebook in Google Colab.
2. Execute the cells step-by-step to:
   - Preprocess the NLQ dataset.
   - Train and evaluate temporal localization models (**VSLBase**, **VSLNet**, **2D-TAN**).
   - Generate and evaluate textual answers using **Video-LLaVA**.

### Results and Outputs

- **Temporal Localization Results**:
  - Found in `temporal_localization_files/` with metrics and timestamp predictions.
- **VideoQA Results**:
  - Located in `video_LLaVa_files/`, including textual answers, evaluation metrics, and visualizations.

---

## Models and Features

### Temporal Localization Models

- **VSLBase** and **VSLNet**:
  - Trained with **Omnivore** and **EgoVLP** features.
  - Predict start and end timestamps for NLQ queries.
- **2D-TAN**:
  - Uses a sliding window approach to process videos with enhanced temporal resolution.

### VideoQA Model

- **Video-LLaVA**:
  - Converts trimmed video segments into textual answers, enabling actionable insights from video data.

### Features

- **Omnivore** and **EgoVLP** feature sets were used to benchmark the temporal localization models.
- Comparisons to baseline models trained on **SlowFast** features were performed.

---

## Contributions

1. **Benchmark Analysis**: Evaluated **VSLBase**, **VSLNet**, and **2D-TAN** with advanced features (**Omnivore**, **EgoVLP**).
2. **Pipeline Integration**: Combined temporal localization with **VideoQA** for precise textual answers.
3. **Enhanced Usability**: Streamlined video query processing, reducing user overhead.

---

## Collaborations

This project was developed collaboratively with [Gabriele Raffaele](https://github.com/Gabriele-Raffaele) and [Peppe2212](https://github.com/Peppe2212).

---

## Report

For a detailed explanation of the methodology, experiments, results, and conclusions, refer to the [project report](./Bridging_Vision_and_Language__NLQ_with_Textual_Answer_Generation.pdf).

---

## Acknowledgments

This work builds upon the resources and tools provided by the following:

- **Ego4D Dataset and NLQ Benchmark** for their comprehensive egocentric data.
- **Omnivore and EgoVLP Features** for enhancing temporal localization capabilities.
- **Video-LLaVA** for  VideoQA.

We express gratitude to the creators and maintainers of these resources for their contributions to the research community.




