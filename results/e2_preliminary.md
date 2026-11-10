# E2 — Cross-domain test (preliminary)

Model: YOLO11n trained on Swimming & Drowning Detection (split by source), tested unchanged.
Second dataset: water-rescue (Roboflow). Only its 550 un-augmented valid/test images used
(train folder contained 3x augmented copies). "float" boxes (floating debris) removed.
Images labelled by setting from content (pool / open water / unclear);
20 images that duplicated our training data were removed.

| Test set | Images | 3-class mAP50 | Drowning AP50 | Swimming AP50 | Person-only mAP50 |
|---|---|---|---|---|---|
| Our test (pools, same dataset) | 1,109 | 0.644 | 0.483 | 0.730 | 0.623 |
| New pools (water-rescue) | 316 | 0.062 | 0.115 | 0.009 | 0.060 |
| Open water (water-rescue) | 208 | 0.282 | 0.434 | 0.129 | 0.437 |

Observations:
- Large drop on any new dataset; the drop comes from dataset shift in general
  (scene, camera, image processing), not only pool vs open water.
- New pools: small lap swimmers mostly missed; model often draws one box over the whole
  image, likely a shortcut learned from close-up stock photos in the training data.
- Open-water set is mostly close-up stock photos -> not representative of beach cameras.
- Label noise: some unlabelled people; one pool image tagged as open water.
- Setting labels done by one person; to be double-checked by a second team member.

## SeaDronesSee (realistic open water, drone view, Roboflow copy, 688 images, 2,386 people)
92% of people are tiny (<1% of image area). Only people in water are labelled (not on boats).
Images were stretched to 640x640 by the uploader.

| Test | Person-only P | R | mAP50 | mAP50-95 |
|---|---|---|---|---|
| @ 640 px | 0.385 | 0.376 | 0.261 | 0.084 |
| @ 1280 px (no retraining) | 0.437 | 0.504 | 0.359 | 0.106 |

- Person-only mAP50 drops from 0.623 (our pool test) to 0.261 at sea.
- Testing at higher resolution alone recovers ~0.10 mAP50 -> small objects are the main problem.
- "Whole-image box" error appears at 640 px, disappears at 1280 px.
