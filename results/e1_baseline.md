# E1 — Baseline results (test set)

Dataset: Swimming and Drowning Detection (Roboflow, CC BY 4.0), 7,295 images, 3 classes.
Our split: by source video (2,128 sources; 70/15/15; 5,080 / 1,106 / 1,109 images).
Roboflow's original split leaked 275 sources across train/valid/test.
Training: 50 epochs, imgsz 640, seed 0, Google Colab Tesla T4.

| Model | Split | P | R | F1 | mAP50 | mAP50-95 | Drowning AP50 | Params |
|---|---|---|---|---|---|---|---|---|
| YOLOv8n | by source | 0.699 | 0.579 | 0.633 | 0.630 | 0.322 | 0.456 | 3.1M |
| YOLO11n | by source | 0.741 | 0.566 | 0.642 | 0.644 | 0.334 | 0.483 | 2.6M |
| YOLOv8n | original (leaky) | 0.846 | 0.741 | 0.790 | 0.845 | 0.501 | 0.896 | 3.1M |

Notes:
- Leakage inflates mAP50 by ~0.22 and drowning AP50 by ~0.44 (different test sets: 747 vs 1,109 images).
- YOLO11n slightly better and smaller; chosen as main model. Single run each.
- Drowning is the hardest class: recall ~0.45.
