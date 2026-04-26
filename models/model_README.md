## Models
To import the weights for the models, import using the installed packaged gdown and upload from a public google drive:

```
import gdown

file_id = "1s-m6kymo4Ob5_sulFJ_2TiG-gZ-NlkWT"
gdown.download(f"https://drive.google.com/uc?id={file_id}", "best.pt", quiet=False)

file_id = "1R_dRzF-X1R4dZm2u5cSfza6KiootRz-1"
gdown.download(f"https://drive.google.com/uc?id={file_id}", "frisbee_dotmaps_cnn_resnet18.pth", quiet=False)
```

The weights were calculated using the same training process listed in [FrisbeeClassification.ipynb](notebooks/FrisbeeClassfication.ipynb), and were saved by mounting Google Drive and saving the weights to the specified folder.
