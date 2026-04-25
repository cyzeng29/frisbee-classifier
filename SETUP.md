# Setup Instructions

## Requirements

- Google Account (for Colab and Drive)
- Google Drive with at least 2GB free
- The Frisbee-2 dataset exported from Roboflow
- Trained YOLO weights (`best.pt`) saved to Drive

---

## Step-by-Step Setup

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/frisbee-play-classifier.git
```

### 2. Upload the Notebook to Google Colab

Go to [colab.research.google.com](https://colab.research.google.com), click **File → Upload notebook**, and select `FrisbeeClassification.ipynb`.

### 3. Set Runtime to GPU

In Colab: **Runtime → Change runtime type (Tested on T4 GPU)**

### 4. Mount Google Drive

Run the Drive mount cell and authorize when prompted to save best weights from model training:
```python
from google.colab import drive
drive.mount('/content/drive')
```

### 5. Upload Required Files to Google Drive

Place the following in your Drive before running the notebook:

```
MyDrive/
├── frisbee_model/
│   └── run1/
│       └── weights/
│           └── best.pt          ← your trained YOLO model
└── frisbee_dotmaps_cnn_resnet18.pth  ← saved classifier
```

### 6. Upload the Dataset to Colab

Download the Frisbee-2 dataset from Roboflow and upload it to Colab at:
```
/content/Frisbee-2/
├── train/images/
├── valid/images/
└── test/images/
```

You can do this via the Colab file browser (left sidebar) or with:
```python
from google.colab import files
files.upload()
```

### 7. Install Dependencies

The first couple cells handle this automatically:
```bash
!pip install ultralytics
!pip install roboflow
```

All other dependencies (PyTorch, torchvision, OpenCV, matplotlib) come pre-installed in Colab.

### 8. Run All Cells in Order

Go to **Runtime → Run all**, or run each cell sequentially. The self-built CNN is optional if the user wants to compare the ResNet and CNN models together.

---

## Local Setup (Optional)

If you want to run outside Colab, install dependencies with:

```bash
pip install -r requirements.txt
```

You will need to adjust all file paths (remove `/content/drive/MyDrive/` prefixes) to match your local directory structure.

---

## Troubleshooting

**Ho/HoStack folder mismatch**  
Run the rename + merge cell before loading the dataset. It consolidates all numbered variants (e.g. `HoStack3`, `Ho`) into the 7 base class folders, which was previously mismatched when loaded from Roboflow.

**Folder Management**
Users will also need the frisbee_dotmaps/ folder in Drive if they want to run the dotmap to CNN section.
