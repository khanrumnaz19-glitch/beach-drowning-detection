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
