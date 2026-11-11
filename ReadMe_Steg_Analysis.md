# AI Lab Background: Detecting Hidden Messages in Images (Steganography)

---

## The Problem

In the world of digital forensics, criminals often use a technique called *steganography* to hide secret messages inside innocent-looking image files. These messages are invisible to the human eye and can bypass traditional detection methods.

**Forensic examiners are now faced with a modern challenge:**

> Given an image, can we determine/detect if a message has been embedded?

The difficulty lies in the fact that visually, **stego images** (those with embedded content) appear identical to normal **cover images**. Without the right tools, it's nearly impossible to know whether an image contains concealed data.

<img width="443" alt="image" src="https://github.com/user-attachments/assets/5928d141-733a-4989-b47f-731b23f0d05f" /> and <img width="407" alt="image" src="https://github.com/user-attachments/assets/68a0f921-83ab-4823-884d-894cd35e2915" />

---

## Objective of the Lab

In this lab, you will train an AI model to help forensic investigators:

1. Detect whether a given image is a **steg image** (contains a hidden message).
2. Distinguish it from a **cover image** (a clean image with no hidden content).

---

## Why Use AI?

Traditional detection methods rely on manual analysis or statistical tools that may fail when sophisticated embedding techniques like **LSB (Least Significant Bit) matching** are used.

Artificial Intelligence, particularly Machine Learning, offers a powerful solution:

- By extracting and analyzing statistical patterns from image features,
- AI models can *learn* the subtle differences between cover and stego images,
- And predict whether an unseen image contains a hidden message.

---

## Outcome

By the end of this lab, you will have built an **AI-powered tool** capable of flagging images that may contain steganographic content — a valuable aid for digital forensic investigations.

---

## Goal

The goal of this lab is to:

- Understand how hidden messages can be embedded into images using a technique called **steganography**.
- Explore the challenges digital forensic investigators face in detecting **LSB-based stego images**.
- Train a machine learning model to classify images as either:
  - **Cover images** (no hidden message), or
  - **Stego images** (contain hidden message).
- Extract both simple and advanced features from grayscale images (e.g., pixel statistics, edge features, correlation).
- Use AI techniques such as **Random Forest** and **PCA** to build an effective detection pipeline.
- Evaluate the trained model on held-out data using metrics such as **accuracy**, **precision / recall** and a **confusion matrix**.
- Test the model with custom grayscale images to determine whether a hidden message exists.

By the end of this lab, you will have developed an **AI-powered steganography detection system** capable of assisting forensic analysts in uncovering hidden communications in images.

---

## Dataset

### Source

The dataset used in this lab is sourced from the **Steganalysis Project Repository** on GitHub:

- Original Cover Image Features:  
  [https://github.com/Sourish1997/steganalysis/blob/master/Datasets/steg_features.csv](https://github.com/Sourish1997/steganalysis/blob/master/Datasets/steg_features.csv)

- Stego Image Features (LSB Embedded):  
  [https://github.com/Sourish1997/steganalysis/blob/master/Datasets/steg_lsb_features.csv](https://github.com/Sourish1997/steganalysis/blob/master/Datasets/steg_lsb_features.csv)

These files contain extracted statistical features from grayscale images — both clean (cover) and tampered (stego) — and serve as the input to train our AI classifier.

---

### Structure

The dataset contains **two CSV files**:

- `steg_features.csv`:  
  - Contains 10,000 rows of feature vectors extracted from **clean cover images**.
  - Each row has 41 numerical values (features) representing image characteristics.

- `steg_lsb_features.csv`:  
  - Contains 10,000 rows of feature vectors extracted from **stego images** that have hidden messages embedded using the **LSB (Least Significant Bit)** technique.
  - Each row also contains 41 numerical features.

After loading, both datasets are labeled (`0` for cover, `1` for stego) and merged into a single dataset for supervised machine learning.

---
## Preprocessing & AI Background

### Preprocessing the Dataset

Before feeding the data into a machine learning model, we perform the following steps:

1. **Labeling**:
   - Clean (cover) image feature vectors are labeled as `0`.
   - Stego (LSB-embedded) image feature vectors are labeled as `1`.

2. **Combining Datasets**:
   - Both datasets are merged into a single DataFrame containing 20,000 samples (10,000 cover + 10,000 stego).

3. **Data Cleaning**:
   - Rows containing invalid or `NaN` values are removed. These often result from uniform image regions or calculation errors.

4. **Normalization**:
   - Feature values are standardized using `StandardScaler` to ensure all features have a mean of 0 and standard deviation of 1. This improves model learning performance.

5. **Dimensionality Reduction (PCA)**:
   - Principal Component Analysis (PCA) is used to reduce the 41 extracted features to 10 key components while preserving most of the variance.
   - This helps in reducing computational load and removing noise from the dataset.

---

### Random Forest Classifier

We train a **Random Forest Classifier**, a powerful ensemble learning method that works by building multiple decision trees and combining their results for better accuracy.

- Works well with tabular data like our extracted features.
- Handles noise and overfitting better than a single decision tree.
- Fast to train and easy to interpret.

---

### Why Use AI for Steganalysis?

- **Precision**: AI can pick up on subtle feature deviations between cover and stego images that humans or traditional tools can't detect.
- **Scalability**: Can scan thousands of images quickly to identify potentially suspicious ones.
- **Adaptability**: The model can be retrained as newer, more complex steganography techniques emerge.

---

##  Training & Evaluation Process

### Steps

#### 1. Load and Prepare the Dataset
- The dataset consists of **two sets of feature vectors**:
  - `Cover` images (clean): Labeled as `0`.
  - `Stego` images (with hidden message using LSB matching): Labeled as `1`.
- The datasets are combined and preprocessed using:
  - **Normalization** with `StandardScaler`
  - **Dimensionality Reduction** with `PCA` (reducing 41 features to 10)

#### 2. Model Initialization
- A **Random Forest Classifier** is initialized using:
  - `n_estimators=100` (100 trees)
  - `max_depth=10` for better control over overfitting
- The classifier is trained to distinguish between cover and stego images using their extracted and reduced feature vectors.

#### 3. Model Training Loop
- The dataset is split: **70% for training**, **30% for testing** (before scaling and PCA, so the test set stays unseen)
- The training step:
  - Fits the model on training features and labels
  - Evaluates the model on both the training data and the held-out test data to compute:
    - **Accuracy**
    - **Classification Report** (Precision, Recall, F1-Score)

```python
# Training the classifier
clf = RandomForestClassifier(n_estimators=100, max_depth=10, random_state=42)
clf.fit(X_train, y_train)
```

---

### Testing and Evaluation Process

#### 1. Image Inference
- A **custom image** is supplied via URL by the user (must be 512x512 grayscale).
- The image is processed and passed through the following steps:
  - **41 CF features** are extracted.
  - The features are **normalized** and reduced to **10 PCA components**.
  - The classifier predicts the class: `Cover` or `Stego`.

```python
# Predict using trained classifier
features = extract_cf_features(image, scaler, pca)
prediction = clf.predict(features)
```

#### 2. Output
- The result is printed for the user:
  - **Cover Image (No Hidden Content)**
  - **Steg Image (Message Detected)**

#### 3. Evaluation Metrics
- The model’s performance is measured using:
  - **Accuracy**
  - **Precision**
  - **Recall**
  - **F1-score**
- These metrics help understand how well the AI detects hidden messages.

---
## 🛠️ Usage Instructions

### Notebooks

| Notebook | Purpose |
|---|---|
| `how_steg_works.ipynb` | Hands-on theory: pixels, bits, hide a message with LSB, recover it, compare cover and stego |
| `AI_steg_predict.ipynb` | Supervised learning: train a Random Forest to detect stego images, then test images |

Run `how_steg_works.ipynb` first, then `AI_steg_predict.ipynb`.

### Running the labs (no installation on your own computer)

1. Open the notebook in your hosted Jupyter environment (or click the *Open in Colab* badge at the top of the notebook).
2. Run all cells from top to bottom (Jupyter: *Kernel, Restart & Run All*; Colab: *Runtime, Run all*).
3. The first cell installs any missing library **inside the hosted session**, and the notebooks download their own data and sample images. Nothing has to be uploaded, downloaded or typed in while the notebook runs.

### Testing your own image

In `AI_steg_predict.ipynb`, Part B, Step 4: set `MY_IMAGE` to the URL (or path) of a **512x512 grayscale `.pgm`** image and run the cell. JPEG images are a poor fit because compression destroys the least-significant-bit patterns the model uses.

---

### Expected Outputs

These numbers are what the notebook produces (the random seed is fixed, so you should see the same values):

```text
Combined Dataset Shape: (20000, 42)
Dataset shape after removing NaNs: (19358, 41)   (removed 642 rows)
Training rows: 13550   Test rows: 5808
Total variance kept by PCA: 96.6%

TRAINING accuracy: 0.7825
TEST accuracy:     0.6985      <- the number that matters (images the model has never seen)
```

On the held-out test set the model is right about 7 times in 10: much better than guessing (50 %), but far from perfect. LSB *matching* is designed to be hard to detect, so this is a realistic result. A stego verdict from this model is a lead, not proof.

#### Prediction example (sample pair no. 1)

```text
Cover image  -> Cover Image (No LSB Matching)               (probability of stego = 0.02)
Stego image  -> Steg Image (LSB Matching Detected)          (probability of stego = 0.81)
```

---

### Conclusion

This lab demonstrates how to build a steganography detection system using machine learning, and, just as importantly, how to measure it honestly: accuracy on unseen data, a confusion matrix, and a clear statement of limitations. Feel free to experiment with other `.pgm` images from the BOSSbase sample collection (numbers 1 to 25).
