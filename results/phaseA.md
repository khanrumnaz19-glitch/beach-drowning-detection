# Phase A — Improving accuracy on pool images (same test set: 1,109 images)

| Model | Overall mAP50 | P | R | Drowning AP50 | Drowning recall | Person out of water AP50 | Swimming AP50 |
|---|---|---|---|---|---|---|---|
| YOLO11n (baseline) | 0.644 | 0.741 | 0.566 | 0.483 | 0.446 | 0.718 | 0.730 |
| YOLO11s (bigger model) | 0.657 | 0.761 | 0.579 | 0.513 | 0.439 | 0.733 | 0.726 |
| YOLO11n + Pool-Watch | 0.638 | 0.670 | 0.578 | 0.532 | 0.494 | 0.647 | 0.737 |

Notes:
- YOLO11s: 3.6x larger, only small gain; drowning recall unchanged -> model size is not the main limit.
- + Pool-Watch (1,417 distinct frames from one CCTV pool, 894 drowning boxes): best drowning AP50 and recall so far.
- Person-out-of-water fell because Pool-Watch has no such class (people on deck unlabelled).
- Precision fell (more false alarms) -> choose alert threshold carefully (A5).

## A5 — Alert threshold (YOLO11n + Pool-Watch, Drowning class)
Cutoff chosen on validation set, confirmed on test set.

| Cutoff | Test recall | Test precision |
|---|---|---|
| 0.05 | 0.72 | 0.29 |
| 0.10 | 0.63 | 0.39 |
| 0.15 (chosen) | 0.58 | 0.47 |
| 0.20 | 0.53 | 0.52 |
| 0.25 (default) | 0.49 | 0.56 |
| 0.30 | 0.44 | 0.60 |
| 0.40 | 0.37 | 0.69 |

- Lowering the cutoff 0.25 -> 0.15 raises drowning recall 0.49 -> 0.58 without retraining.
- Extra false alarms to be filtered by the tracking stage (alert only if drowning persists over several seconds).
