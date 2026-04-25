# Frisbee Play Classifier

## What it Does

This project builds an end-to-end pipeline for automatically classifying Ultimate Frisbee plays from game footage images. A custom-trained YOLOv8 model first detects players and the disc in each frame, assigning them to three categories: teammates (green), opponents (red), and the frisbee (orange). Those detections are then converted into simplified "dot maps" — white 640×640 canvases where each player and disc is represented by a single colored dot. Finally, a fine-tuned ResNet18 classifier is trained on these dot maps to recognize seven distinct play types: 32Twist, Dominator, Dump, Flash, Go, HoStack, and Wheel. The result is a system where you can feed in a raw game image and receive a predicted play classification along with a three-step visual breakdown of how the prediction was made.

---

## Quick Start

1. Open the notebook in Google Colab:  
   [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

2. Mount your Google Drive when prompted.

3. Run cells in order — the notebook is fully sequential. Key steps:
   - **Cell 1:** Install dependencies (`ultralytics`)
   - **Cell 2:** Mount Drive and load YOLO model
   - **Cell 3:** Rename any `Ho` prefixed images to `HoStack`
   - **Cell 4:** Generate dot maps from all images
   - **Cell 5:** Merge numbered class folders into 7 base classes
   - **Cell 6:** Load dataset and train ResNet18 classifier
   - **Cell 7:** Run `predict_play('path/to/image.jpg')` on any new image

4. To classify a new image:
```python
from google.colab import files
uploaded = files.upload()
predict_play(f'/content/Frisbee-2/test/images/{list(uploaded.keys())[0]}')
```

---

## Video Links

| Description | Link |
|-------------|------|
| Demo Video | (https://youtu.be/USpsTr_W6iE)|
| Presentation | _Coming soon_ |

---

## Evaluation

### Model Performance

| Model | Train Acc | Val Acc | Notes |
|-------|-----------|---------|-------|
| Custom CNN | ~32% | ~12% | Too many parameters for dataset size |
| MobileNetV2 | ~22% | ~8% | Underfitting due to small dataset |
| ResNet18 (final) | ~42% | ~15% | Best result; still limited by data size |

### Key Findings

- **Dataset size was the primary bottleneck.** With only ~130 images per class after merging, all models struggled to generalize. Random chance for 7 classes is ~14%, so results are meaningful but modest.
- **Dot maps lose spatial context.** Representing players as single dots discards body orientation, movement direction, and formation shape, making the classification task harder than expected.
- **The YOLO detection step performs well.** Player and disc detection was reliable at `conf=0.3`, which kept the dot map generation clean.
- **Future improvements:** Collect more labeled data (300+ images per class), experiment with graph neural networks that better capture spatial relationships between dots, or add temporal information from video sequences.

---

## Individual Contributions

| Team Member | Contributions |
|-------------|---------------|
| _Name_ | YOLO model training, dataset collection |
| _Name_ | Dot map generation pipeline, folder merging logic |
| _Name_ | ResNet18 classifier, training loop, evaluation |
| _Name_ | `predict_play` inference pipeline, README and documentation |

_Update this table with your actual names and contributions._
