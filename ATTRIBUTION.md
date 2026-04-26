# Attribution

## Dataset

**Frisbee-2 Dataset**  
Source: [Roboflow Universe](https://roboflow.com)  
Used for training the YOLO player/disc detection model and generating dot map training data.  
License: Per Roboflow project terms.

---

## Models and Frameworks

**YOLOv8 (Ultralytics)**  
Repository: https://github.com/ultralytics/ultralytics  
License: AGPL-3.0  
Used for player and frisbee detection in game images.

**ResNet18 (PyTorch / torchvision)**  
Source: https://pytorch.org/vision/stable/models/resnet.html  
Pretrained weights: ImageNet (via `torchvision.models.ResNet18_Weights.DEFAULT`)  
Used as the base architecture for the play classification model.

**PyTorch**  
Source: https://pytorch.org  
License: BSD-3-Clause  
Used for model definition, training loop, and inference.

**OpenCV (cv2)**  
Source: https://opencv.org  
License: Apache 2.0  
Used for dot map generation and image processing.

---

## AI Assistance

This project was developed with assistance from **Claude (Anthropic)**, an AI assistant as well as Codex from OpenAI.

AI was used to help with:
- Debugging CUDA errors and model loading issues
- Designing the dot map feature extraction approach
- Writing and refactoring training loop code (augmentation, early stopping, scheduler)
- Structuring the end-to-end `predict_play` inference pipeline
- Diagnosing overfitting and suggesting architectural changes
- Writing this documentation

All code was reviewed, tested, and run by the project team. AI-generated suggestions were adapted and validated by team members throughout development.

---

## Tools

| Tool | Purpose |
|------|---------|
| Google Colab | Development environment and GPU access |
| Google Drive | Model and dataset storage |
| Roboflow | Dataset management and export |
| GitHub | Version control and submission |
| Matplotlib | Visualization and result display |
