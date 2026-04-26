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

### 4. Install dependecies
```bash
!pip install ultralytics
!pip install roboflow
```
All other dependencies (PyTorch, torchvision, OpenCV, matplotlib) come pre-installed in Colab.

### 5. Upload the public Google Drive files with the following cells:

```
from ultralytics import YOLO
import gdown

file_id = "1s-m6kymo4Ob5_sulFJ_2TiG-gZ-NlkWT"
gdown.download(f"https://drive.google.com/uc?id={file_id}", "best.pt", quiet=False)

model = YOLO('best.pt')

file_id = "1R_dRzF-X1R4dZm2u5cSfza6KiootRz-1"
gdown.download(f"https://drive.google.com/uc?id={file_id}", "frisbee_dotmaps_cnn_resnet18.pth", quiet=False)
```

Place the following in your Drive before running the notebook:

```
MyDrive/
├── frisbee_model/
│   └── run1/
│       └── weights/
│           └── best.pt          ← your trained YOLO model
└── frisbee_dotmaps_cnn_resnet18.pth  ← saved classifier
```

### 7. Run Up to the Play Predicting Function (For Testing Purposes)

Run up to this cell:
```
from google.colab import files
uploaded = files.upload()

import shutil
for filename in uploaded.keys():
    shutil.move(filename, f'/content/Frisbee-2/test/images/{filename}')
    print(f"Moved {filename}")

predict_play(f'/content/Frisbee-2/test/images/{filename}')
```

### 8. Run All Cells in Order (For Full Training Only)

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
Users will need the correct file path for frisbee_mode/ and frisbee_dotmaps/ folder in Drive if they want to run the models.

**Mounting Google Drive**
When mounting the google drive, ensure that the specified folder and file path is accurate.
```
from google.colab import drive
drive.mount('/content/drive')
```
