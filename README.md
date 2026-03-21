# **BRAT** (Bread + Cat)

## **Project overview**
This project tackles the binary image classification task of distinguishing between images of cats and cats in the "loaf" position (paws tucked underneath the body, resembling a loaf shape) using the [CatLoaf](https://www.kaggle.com/datasets/erogluegemen/cat-catloaf-classification) dataset.

---

## **Setup Instructions**
The dataset is sourced from [CatLoaf](https://www.kaggle.com/datasets/erogluegemen/cat-catloaf-classification) and contains two classes: loaf (cats in the loaf position) and cat (cats not in the loaf position). Download the dataset from Kaggle and place the images into images/loaf/ and images/cat/ before training.

---

## Project Structure

```
BRAT/
├── brat_mlp.ipynb        <- MLP baseline model
├── brat_project.ipynb    <- EfficientNet-B0 CNN with 5-fold CV
├── images/
│   ├── cat/              <- non-loaf cat images (label = 0)
│   └── loaf/             <- cat loaf images (label = 1)
└── results/              <- auto-created during training
    ├── fold_1_best.pt
    ├── fold_2_best.pt
    ├── fold_3_best.pt
    ├── fold_4_best.pt
    ├── fold_5_best.pt
    ├── cv_summary.json
    ├── confusion_matrix.png
    ├── roc_curve.png
    └── training_curves.png
```

---

## Required Dependencies

**Python 3.10+**

For the MLP notebook:
```bash
pip install torch torchvision scikit-learn matplotlib seaborn numpy pillow tqdm
```

For the CNN notebook:
```bash
pip install torch torchvision scikit-learn matplotlib pillow
```

---

## Dataset

The dataset is sourced from [this Kaggle page](https://www.kaggle.com/datasets/erogluegemen/cat-catloaf-classification) and contains two classes: `loaf` (cats in the loaf position) and `cat` (cats not in the loaf position). Download the dataset from Kaggle and place the images into `images/loaf/` and `images/cat/` before running either notebook.

The dataset contains 646 images total, with 323 images per class.

---

## How to Train

### MLP Baseline — `brat_mlp.ipynb`

1. Make sure the dataset is in `images/cat/` and `images/loaf/`
2. Open `brat_mlp.ipynb` and run all cells top to bottom
3. The notebook loads the data, trains the MLP for 30 epochs, and prints final train and test loss and accuracy

### EfficientNet-B0 CNN — `brat_project.ipynb`

1. Make sure the dataset is in `images/cat/` and `images/loaf/`
2. Open `brat_project.ipynb` and run all cells top to bottom
3. The notebook will:
   - Load and preview the dataset
   - Train EfficientNet-B0 using 5-fold stratified cross-validation (20 epochs per fold)
   - Save the best checkpoint per fold to `results/`
   - Evaluate all fold checkpoints and print a classification report
   - Save a confusion matrix, ROC curve, and training curves to `results/`

---

## Expected Outputs

### MLP
```
Final Epoch Train: {'loss': 0.6292, 'acc': 0.6415}
Test: {'loss': 0.6433, 'acc': 0.6077}
```

### EfficientNet-B0 CNN
```
5-FOLD CV COMPLETE
Per-fold F1 : [0.9173, 0.9846, 0.9385, 0.9764, 0.9302]
Mean F1     : 0.9494 +/- 0.0264

AGGREGATE RESULTS — EfficientNet-B0 (5-fold CV)

              precision    recall  f1-score   support

         cat       0.95      0.94      0.95       323
        loaf       0.94      0.95      0.95       323

    accuracy                           0.95       646
   macro avg       0.95      0.95      0.95       646
weighted avg       0.95      0.95      0.95       646

Mean F1      : 0.9494 +/- 0.0264
Mean AUC-ROC : 0.9835 +/- 0.0080
```

Three plots are saved to `results/`: a confusion matrix, ROC curve, and per-fold training curves.

---

## Reproducing Results

All random seeds are fixed (seed=0 for MLP, seed=42 for CNN). To reproduce:

1. Download the dataset from [Kaggle](https://www.kaggle.com/datasets/erogluegemen/cat-catloaf-classification) and place images in `images/cat/` and `images/loaf/`
2. Install dependencies
3. Run `brat_mlp.ipynb` top to bottom
4. Run `brat_project.ipynb` top to bottom

Note: the CNN was run on CPU. Training takes approximately 50 seconds per epoch per fold (~50 minutes total). A GPU will be significantly faster.
