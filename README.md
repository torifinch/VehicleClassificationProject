# Vehicle Classification Project

This project explores both **unsupervised** and **supervised machine learning** approaches to classify vehicles into categories: **car, bus, and van**, based on geometric shape and size metrics. The clear winner of the project was the supervised learning approach using the Random Forest Classifier, which achieved an impressive 95% accuracy in correctly classifying vehicles as cars, buses, or vans.

## Author

Victoria Finch 2025

---

## Project Goals

- Cluster vehicles based on size metrics using **K-Means** and **DBSCAN**
- Classify vehicle types using **Random Forest Classifier**
- Perform **dimensionality reduction with PCA**
- Conduct robust **EDA (Exploratory Data Analysis)**
- Evaluate models using appropriate metrics like **Silhouette Score**, **Accuracy**, and **Classification Report**

---

## Dataset

The dataset contains shape-based numerical features for different vehicle images.  
**Target Variable**: `class` (car, bus, van)

### ✅ Features:

| Feature | Description |
|--------|-------------|
| compactness | Shape compactness |
| circularity | Closeness to a circle |
| distance_circularity | Distance-based circularity |
| radius_ratio | Ratio of radii |
| pr.axis_aspect_ratio | Aspect ratio of principal axis |
| max.length_aspect_ratio | Maximum length-based aspect ratio |
| scatter_ratio | Measure of spread |
| elongatedness | Degree to which object is elongated |
| pr.axis_rectangularity | Principal axis rectangularity |
| max.length_rectangularity | Max length rectangularity |
| scaled_variance / .1 | Scaled variances of pixel intensities |
| scaled_radius_of_gyration / .1 | Radius of gyration (moment of inertia) |
| skewness_about / .1 / .2 | Skewness (shape asymmetry) |
| hollows_ratio | Ratio of hollow areas |

---

##  Exploratory Data Analysis (EDA)

- **Correlation Heatmap** to understand feature relationships
- **Boxplots** to detect outliers
- **Pairplots** by vehicle class
- **Class balance check** using countplots

---

##  Feature Engineering & Selection

- Removed or combined redundant features based on correlation
- **Standardized** all features using `StandardScaler`
- Reduced dimensionality with **PCA** for clustering visualization and noise reduction

---

##  Unsupervised Learning

### ✅ K-Means Clustering

Tested multiple values of K:
- **K=2 → Silhouette Score: 0.525** (best separation)
- **K=3 → Silhouette Score: 0.464** (aligns with 3 vehicle types)

**Cluster-label cross tabulation** showed strong alignment with true classes.

### ✅ DBSCAN

Final parameters:
- `eps = 2.2`
- `min_samples = 25`

**Result:**
- **Silhouette Score: 0.052** → Weak clustering
- High number of noise points
- Poor match with true vehicle labels

**Conclusion:** DBSCAN is not effective for this dataset.

---

##  Supervised Learning

### ✅ Random Forest Classifier

- Trained on original features and PCA components
- 80/20 train-test split with stratification
- Used Grid Search to tune `max_depth`

**Final Performance:**
Accuracy: 0.95
Precision / Recall / F1-Score:

Bus: 0.95 / 0.95 / 0.95

Car: 0.96 / 0.93 / 0.95

Van: 0.91 / 0.97 / 0.94


---

## 📈 Evaluation Metrics Explained

| Metric | Description |
|--------|-------------|
| Accuracy | Overall correct predictions |
| Precision | Correct positive predictions out of predicted positives |
| Recall | Correct positive predictions out of actual positives |
| F1-Score | Harmonic mean of precision and recall |
| Silhouette Score | Used in clustering; measures how similar an object is to its own cluster vs. others |

---

##  Outlier Handling

- Outliers detected using boxplots and Z-score method
- PCA helped mitigate influence of outliers
- Extreme values filtered prior to DBSCAN for improved clustering

---

##  Dimensionality Reduction with PCA

- PCA applied before clustering
- Retained **91% of variance with 5 components**
- Helped improve **K-Means silhouette score** from 0.28 → 0.46+

---

## ✅ Conclusion

- **K-Means with K=2 or 3 was the most effective clustering approach**
- **Best Result: Random Forest classifier achieved 95% accuracy** in classifying vehicles
- **DBSCAN was less effective due to noise sensitivity**
- PCA improved cluster separation and model performance

---

## 📌 Tech Stack

- Python 3
- Pandas, NumPy, Scikit-Learn, Matplotlib, Seaborn
- Jupyter Notebook
