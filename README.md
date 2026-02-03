# Suspicious Object Detection in Crowded Scenes

## Project Motivation
In public safety and security, identifying unattended or suspicious objects is critical. While standard object detection (YOLO, etc.) can find a "bag," it cannot inherently understand if that bag is "suspicious" based on context (e.g., being abandoned in a crowded area). This project aims to bridge the gap between simple detection and contextual security analysis.

## Problem Statement
The Home Front Command (HFC) defines a suspicious object by three main criteria:

1. **Lack of ownership (Unattended).**

2. **Unnatural placement (Out of place).**

2. **Physical anomalies (Protruding wires/metal).**

Current datasets lack high-quality, labeled examples of these specific scenarios in crowded environments. Our challenge was to detect these items using only static images, overcoming the lack of temporal (video) data to determine ownership.


## Datasets Used or Collected
**Background Scenes:** High-resolution crowded scenes generated via Z-ImageTurbo.

**Synthetic Suspicious Objects:** A custom collection of "Suspicious Items" (bags with wires, abandoned packages) used for inpainting.

**Human Detection Data:** Pre-trained weights from YOLO were used to identify human candidates for removal.

## Data Augmentation and Generation Methods
We developed a sophisticated Synthetic Data Pipeline:

1. **Human Detection:** Using YOLO to extract Bounding Boxes (BB).

2. **Candidate Selection:** Filtering the Top-3 largest BBs for high-resolution synthesis.

3. **Inpainting-based Removal:** Using FluxKontext (Diffusion Model) to remove a selected person while maintaining background consistency.

4. **Strategic Inpainting:** Placing a suspicious object in the vacated space to simulate an "abandoned" item.

5. **Auto-Labeling:** Calculating the Pixel-wise Difference between the "before" and "after" images to generate precise segmentation masks and BBs.

## Models and Pipelines Used
* Detection Backbone: YOLO (You Only Look Once)

* Generative Models: FluxKontext Diffusion for image editing and inpainting.

## Results

The model was evaluated on our custom synthetic test set, achieving high localization accuracy and a low false-alarm rate. The following metrics were obtained:

| Metric | Value | Description |
| :--- | :--- | :--- |
| **Precision** | 91.39% | Measures the accuracy of the detections (Low false positives). |
| **Recall** | 88.43% | Measures the ability to find all suspicious objects (Low false negatives). |
| **mAP50** | 92.55% | Mean Average Precision at an IoU threshold of 0.5. |
| **mAP50-95** | 87.29% | Average mAP across IoU thresholds from 0.5 to 0.95. |
| **Fitness** | 0.8729 | A weighted combination of metrics to indicate overall model health. |

### Performance Analysis
* **Robust Localization:** An **mAP50-95 of 87.29%** indicates that the model is highly precise in defining the boundaries of the suspicious objects, not just their general location.
* **Security Reliability:** The high **Precision (91.39%)** ensures that the system minimizes unnecessary alerts in crowded public spaces.

## Repository Structure
* `data/` - data folder
* `code/` - notebooks folder
* `slides/` - pptx and pdf slides folder
* `visuals/` - graphs folder
* `results/` - csv, json, and yaml metrics

## Team Members
* Natan Shick
* Orel Cohen
* Israel Peled