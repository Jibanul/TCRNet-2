# TCRNet Project

This repository contains scripts and instructions to preprocess data, train models, and test TCRNet and TCRNet-2 booster models. Below is a detailed guide to understanding and running the scripts and using the data files.

## Table of Contents
- [Scripts](#scripts)
- [Script Descriptions and Sequence](#script-descriptions-and-sequence)
- [Supporting Scripts](#supporting-scripts)
- [Folders and Files](#folders-and-files)
- [Train](#train)
- [Test](#test)
- [Dependencies](#dependencies)

---

## Scripts

### Script Descriptions and Sequence
Run the scripts in the following sequence for proper execution:

1. **`extract_chip.py`**  
   - Creates 40x80 chips to train the networks.

2. **`center_crop_chip.py`**  
   - Crops 40x80 chips to 20x40 to generate the QCF filters for the first layer.

3. **`hard_clutter_tcrnet2_chip.py`**  
   - Creates hard clutter for the booster TCRNet-2.

4. **`qcf_basis.py`**  
   - Generates the QCF filters.

5. **`train_tcr2.py`**  
   - Trains both TCRNet-2 and TCRNet-2 booster models.

6. **`test_tcr2.py`**  
   - Tests the TCRNet model.

7. **`roc_multiple_TCRNets.py`**  
   - Plots the ROC curves.

---

### Supporting Scripts
The following scripts are called within the above scripts:
- **`tcr_cnn_2streams.py`**  
  - Contains the model architecture.
  
- **`imresize.py`**  
  - Scales images to a 2500m range.
  
- **`crop.py`**  
  - Crops images.

---

## Folders and Files

- **`weights_filters/`**  
  - Contains trained models and filters.

- **`data/`**  
  - Contains JSON files with test image information for various ranges (2.5 km, 3.0 km, and 3.5 km). It also includes training and testing datasets.
    - **`test_25to35all.json`**: Both day and night images.
    - **`test_25to35day.json`**: Day images.
    - **`test_25to35night.json`**: Night images.

- **`requirements.txt`**  
  - Lists all Python libraries required for this project.

---

## Train

To train the TCRNet-2 and TCRNet-2 booster models:

1. Ensure the required datasets are available in the `data/` directory.
2. Generate QCF filters by running:  
```
   python qcf_basis.py
```
3. Train the models using:  
```
   python train_tcr2.py
```
4. During the training process, the trained weights and filters will be saved in the `weights_filters/` directory.

---

## Test

To test the trained TCRNet models:

1. Ensure that the trained model weights and filters are available in the `weights_filters/` directory.
2. Run the testing script:  
```
   python test_tcr2.py
```
3. To visualize the performance of multiple TCRNets, generate ROC curves using:  
```
   python roc_multiple_TCRNets.py
```

---

## Dependencies

To set up the environment, install the required dependencies by running:  
```
pip install -r requirements.txt
```

---

## Notes
Ensure that the data and required files are correctly placed in the respective directories before running the scripts. Follow the sequence mentioned above for the smooth execution of the project pipeline.
