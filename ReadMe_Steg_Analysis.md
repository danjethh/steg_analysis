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
- Evaluate the trained model using metrics such as **accuracy** and **F1-score**.
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
- The dataset is split: **70% for training**, **30% for testing**
- The training loop:
  - Fits the model on training features and labels
  - Evaluates the model on training data to compute:
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

### ⚙️ Setup

#### 1. Install Dependencies
Use the following command to install all required Python packages:

```bash
pip install torch torchvision matplotlib opencv-python pycocotools py7zr requests PyWavelets
```

#### 2. Download and Extract the Dataset

```bash
# No compressed dataset used in this lab
# Instead, all data is sourced from:
# https://github.com/Sourish1997/steganalysis/tree/master/Datasets
```

---

### Running the Lab

1. **Run each cell** in the notebook **sequentially**:
   - Train the model using extracted features.
   - Save the trained model.
   - Use the prediction function to test the model on new images.

2. **To test a custom image**:
   - Make sure the image is **512x512 grayscale (.pgm format)**.
   - Use the `run_prediction(scaler, pca, clf)` function and **provide the image URL** when prompted.

---

### Expected Outputs

#### Training Logs

```text
Training Accuracy: 0.9876

Classification Report:
              precision    recall  f1-score   support
       Cover       0.99      0.98      0.98      1500
       Stego       0.98      0.99      0.98      1500
    accuracy                           0.98      3000
```

#### Prediction Result

```text
Prediction Result: Steg Image (LSB Matching Detected)
```

#### Custom Image Output

- The system will print the predicted label based on the trained model:
  - `Steg Image (LSB Matching Detected)`  
  - `Cover Image (No LSB Matching)`

---

### Conclusion

This lab demonstrates how to build a steganography detection system using machine learning. By analyzing subtle statistical patterns from image features, the AI model can accurately detect whether a message is hidden inside an image. This is a powerful tool for digital forensics, helping investigators uncover hidden evidence within seemingly harmless images.

Feel free to experiment with other `.pgm` images and observe the model's predictions!
```
