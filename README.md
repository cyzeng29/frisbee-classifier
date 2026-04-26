# Frisbee Play Classifier

In the fast-paced sport of ultimate frisbee, an effective way to create progress is to create formations/plays that allow players to be in pre-planned positions to initiate actions to score, similar to other sports. Using pre-trained, fine-tuned, and self-built models, this project is designed to classify different formations from unknown images, by translating bounding boxes into dot maps, which are eventually classified.

## What it Does

This project builds an end-to-end pipeline for automatically classifying Ultimate Frisbee plays from game footage images. A custom-trained YOLOv8 model first detects players and the disc in each frame, assigning them to three categories: teammates (green), opponents (red), and the frisbee (orange). Those detections are then converted into simplified "dot maps" — white 640×640 canvases where each player and disc is represented by a single colored dot. Finally, a fine-tuned ResNet18 classifier is trained on these dot maps to recognize seven distinct play types: 32Twist, Dominator, Dump, Flash, Go, HoStack, and Wheel. The result is a system where you can feed in a raw game image and receive a predicted play classification along with a three-step visual breakdown of how the prediction was made.

---

## Quick Start

1. Open the notebook in Google Colab:  
   [![Open in Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/)

2. **For testing existing trained models:** Run cells in order, as the notebook is fully sequential.
   - **1:** Install dependencies (`ultralytics` and `roboflow`) <- Have your roboflow API key ready
   - **2:** Import best weights from drive for YOLOv8 fine-tuned model and ResNet18/CNN model
   - **3:** Define the classifier and load weights
   - **4:** Define the predict_play function for bounding boxes to dot map to classification process
   - **5:** Run `predict_play('path/to/image.jpg')` on any new image

3. **Optional, For training models resulting in new weights**
   - **1:** Data split (train, val, test) and train the pre-trained Yolov8 model
   - **2:** Display sample bounding boxes and accuracy from model
   - **3:** Rename any `Ho` prefixed images to `HoStack` for data cleaning
   - **4:** Generate dot maps for all images
   - **5:** Merge numbered class folders into 7 base classes for each formation
   - **6:** Train the selected CNN model and display sample classifications
   - **7:** Save new weights


5. To classify a new image:
```python
from google.colab import files
uploaded = files.upload()

import shutil
for filename in uploaded.keys():
    shutil.move(filename, f'/content/Frisbee-2/test/images/{filename}')
    print(f"Moved {filename}")

predict_play(f'/content/Frisbee-2/test/images/{filename}')
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

| Epoch | Train Loss | Train Acc | Val Loss | Val Acc |
|-------|------------|-----------|----------|---------|
| 1 | 2.0090 | 18.06% | 1.9932 | 16.15% |
| 5 | 1.4463 | 47.14% | 1.4997 | 36.15% |
| 10 | 1.1449 | 60.13% | 1.2528 | 40.00% |
| 15 | 0.8126 | 74.89% | 1.0093 | 60.77% |
| 20 | 0.6156 | 81.50% | 0.6989 | 77.69% |
| 25 | 0.4182 | 88.11% | 0.5024 | 85.38% |
| 30 | 0.3373 | 90.75% | 0.3387 | 92.31% |

### Key Findings

- The ResNet18 classifier improved steadily from 16% to 92% validation accuracy over 30 epochs, with no signs of overfitting according to its high validation accuracy
- As random chance for 7 classes is ~14%, the final result is a strong outcome given the dataset size.
- For future improvements, add complex temporal information from video sequences, or train different CNN models better at recognizing spatial relationships.

---

## Individual Contributions

| Team Member | Contributions |
|-------------|---------------|
| _Colin Zeng_ | Data Collection and Augmentation, Yolov8 model fine-tuning, Dot-map translation, Displaying and loading images |
| _Andrew Ploskunak_ | Data Collection, ResNet18/CNN model training, Saving and Loading Weights, Video Recordings  |
