# **BRAT** (Bread + Cat)

## **Project overview**
This project tackles the binary image classification task of distinguishing between images of cats and cats in the "loaf" position (paws tucked underneath the body, resembling a loaf shape) using the [CatLoaf](https://www.kaggle.com/datasets/erogluegemen/cat-catloaf-classification) dataset.

---

## **Setup Instructions**
The dataset is sourced from [CatLoaf](https://www.kaggle.com/datasets/erogluegemen/cat-catloaf-classification) and contains two classes: loaf (cats in the loaf position) and cat (cats not in the loaf position). Download the dataset from Kaggle and place the images into images/loaf/ and images/cat/ before training.

**Requires Python 3.10+**

---

## Required dependencies
- torch 
- torchvision 
- scikit-learn 
- matplotlib 
- seaborn 
- numpy 
- pillow
- tqdm


## How to train the model

```bash
python cat_loaf_classifier.py --mode train --data_dir data
```

## How to evaluate the model

## Expected outputs
