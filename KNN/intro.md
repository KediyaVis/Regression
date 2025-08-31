# K-Nearest Neighbors (KNN) Classifier

## What is KNN?
- **K-Nearest Neighbors (KNN)** is a **supervised machine learning algorithm** used for **classification** (and regression).
- It works by:
  1. Storing all training data.
  2. When a new data point comes in, finding the **K closest training samples** (neighbors).
  3. Predicting the label based on the **majority vote** (classification) or average (regression).
<img width="1390" height="790" alt="image" src="https://github.com/user-attachments/assets/148738b7-7dd0-40fd-8dfd-7f9eafc3a182" />

---

## How it Works (Classification)
1. Choose a value for **K** (e.g., 3 or 5).
2. Measure the **distance** (usually Euclidean) between the new data point and all training samples.
3. Select the **K nearest neighbors**.
4. Assign the class label that is most common among these neighbors.

---

## Example
Suppose K = 3 and we want to classify a new point:
- 2 nearest neighbors are **Class A**
- 1 nearest neighbor is **Class B**

The model predicts **Class A**.

---

## Key Hyperparameters

- **n_neighbors (K):** Number of neighbors to consider.  
  - Small K → more flexible, can overfit.  
  - Large K → smoother decision boundary, may underfit.  
  - Common heuristic: `K ≈ sqrt(N)` where `N` is the number of samples.  

- **weights:** Determines how neighbors contribute to the vote.  
  - `"uniform"`: all neighbors are equally weighted.  
  - `"distance"`: closer neighbors have more influence.  
  - Custom function can also be defined.  

- **metric:** Distance metric used to measure closeness.  
  - `"minkowski"` (default, with `p=2` → Euclidean distance).  
  - `"manhattan"` (`p=1`).  
  - `"chebyshev"`, `"cosine"`, or other supported metrics.  

- **p:** Power parameter for Minkowski distance.  
  - `p=1`: Manhattan distance.  
  - `p=2`: Euclidean distance.  

- **algorithm:** Method used to compute neighbors.  
  - `"auto"`: chooses the best method.  
  - `"ball_tree"`, `"kd_tree"`, `"brute"`.  

- **leaf_size:** Affects speed of `kd_tree` and `ball_tree`. Does not affect accuracy.  

- **n_jobs:** Number of CPU cores to use. `-1` means all cores.

---

## Advantages
- Simple and intuitive.  
- Works well with smaller datasets.  
- Non-parametric (makes no assumptions about data distribution).  

---

## Disadvantages
- Computationally expensive for large datasets (requires distance calculation for all points).  
- Sensitive to noisy data and irrelevant features.  
- Performance depends heavily on the choice of **K** and feature scaling.  

---

## Python Example (Scikit-learn)
```python
from sklearn.datasets import load_iris
from sklearn.model_selection import train_test_split
from sklearn.neighbors import KNeighborsClassifier
from sklearn.metrics import classification_report

# Load dataset
X, y = load_iris(return_X_y=True)
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

# Create KNN model with hyperparameters
knn = KNeighborsClassifier(
    n_neighbors=5,       # number of neighbors
    weights="distance",  # closer neighbors have more influence
    metric="minkowski",  # distance metric
    p=2,                 # Euclidean distance
    n_jobs=-1            # use all CPU cores
)

# Train model
knn.fit(X_train, y_train)

# Predictions
y_pred = knn.predict(X_test)

# Evaluation
print(classification_report(y_test, y_pred))
