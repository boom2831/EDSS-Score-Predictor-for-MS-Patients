
# 🧠 EDSS Prediction Using Hybrid Deep Learning on Brain MRI

## 📌 Title:
**A Deep Learning Hybrid Approach for EDSS Prediction Using Brain MRI and Lesion Segmentation**

---

## 👥 Authors:
- Bhumika G  
- Aniketh Chakravarthy S  
- Bhuvana S  
- Sujay S Veershette  
**Department of Computer Science, RV University**

---

## 🧾 Abstract:

We propose a hybrid deep learning model combining convolutional neural networks (CNNs) and ensemble learning techniques for predicting Expanded Disability Status Scale (EDSS) in Multiple Sclerosis (MS) patients using multimodal MRI and lesion segmentation.

---

## 📂 Dataset Overview:

Each patient has:
- **MRI Scans**:
  - T1-weighted
  - T2-weighted
  - FLAIR
- **Lesion Masks** (performed binary segmentation)
- **Clinical Data** (CSV)

---

> Each slice is 2D axial and aligned to RAS orientation.

---

## ⚙️ Preprocessing Pipeline:

1. Load NIfTI images using `nibabel`
2. Extract center 2D axial slices
3. Resize to 224×224
4. Normalize intensities [0, 1]
5. Align lesion masks to all modalities

---

## 🧬 Feature Engineering:

| Feature                    | Description                          |
|---------------------------|--------------------------------------|
| LesionVolume_mm3          | Total lesion size                    |
| LesionCount               | Number of unique lesion areas       |
| FLAIR/T2 Contrast Ratio   | Differentiates chronic vs active    |
| BrainVolume (mm3)         | Total brain size (from T1 scan)     |
| MeanLesionSize            | Average size of lesions             |
| Modality-specific Lesion Load | FLAIR, T1, T2                      |


---

## 🧠 CNN Architecture:

- 2 Convolutional layers with ReLU + MaxPool
- Flatten to 224-D embedding
- Regressed against EDSS score

> **Input Channels**: Stacked T1, T2, and FLAIR images

---

## 🔁 Cross-Validation:

- **Leave-One-Out Cross Validation (LOOCV)** used
- 1 patient left out, 59 used for training in each fold
- Models: Ridge, Lasso, SVR, Random Forest, XGBoost, MLP

---

## 📊 Model Evaluation:

| Model            | MSE    | R² Score |
|------------------|--------|----------|
| **SVR**          | 1.134  | 0.187    |
| Ridge Regression | 1.721  | 0.313    |
| Lasso Regression | 2.258  | -0.034   |
| Random Forest    | 2.334  | 0.064    |

> CNN embeddings significantly enhanced performance.

---

## 🧪 Requirements:

```bash
pip install numpy pandas nibabel scikit-learn xgboost matplotlib
```

---

## 🎯 Key Takeaways:

- SVR with CNN + radiomics gave best results
- Hybrid modeling captures clinical, image annotations & imaging correlations
- FLAIR and lesion segmentation critical for prediction

---

## 📚 References:

- He et al., 2016 – ResNet
- Eshaghi et al., 2021 – MS Clustering
- Danelakis et al., 2020 – Lesion-based EDSS prediction

(*Full list in report*)

---

## 🙏 Acknowledgements:

We thank **Prof. Shoeb Ahmad** and RV University for providing guidance and mentorship.
