## Data
To import data from Roboflow, use your personal Roboflow API key when prompted to pull in the augmented images for training purposes:
```
!pip install roboflow

from roboflow import Roboflow
api_key = input("Enter your Roboflow API key: ")
rf = Roboflow(api_key=api_key)
project = rf.workspace("colins-workspace-zcf3w").project("frisbee-5swwf")
version = project.version(2)
dataset = version.download("yolov8")
```

The data consists of 649 total images spanning the 7 different classifications. There were 10 outputs per training example during augmentation,  which included a horizontal flip, rotation between -15° and +15°, and brightness adjustment between -25% and +25%. This data underwent futher data preprocessing, cleaning, and augmentation during training itself.
