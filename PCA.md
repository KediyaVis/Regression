# 📊 Principal Component Analysis (PCA) – Math & Intuition

## 1. Setup
We have a dataset with `n` samples and `d` features:
\[
X \in \mathbb{R}^{n \times d}
\]

👉 First, center the data (subtract mean from each feature):
\[
X_{centered} = X - \mu
\]

---

## 2. Goal of PCA
Find directions (vectors) that capture **maximum variance** in the data.

Optimization problem:
\[
\max_{w} \ \text{Var}(Xw) \quad \text{s.t. } \|w\|=1
\]

---

## 3. Variance and Covariance
Variance of projection on \( w \):
\[
\text{Var}(Xw) = \frac{1}{n} \|Xw\|^2 = w^T \Sigma w
\]

where covariance matrix is:
\[
\Sigma = \frac{1}{n} X^T X
\]

---

## 4. Eigenvalue Problem
The optimization reduces to solving:
\[
\Sigma w = \lambda w
\]

- \( w \): **eigenvector** (direction of maximum variance)  
- \( \lambda \): **eigenvalue** (amount of variance along that direction)

---

## 5. Geometric Meaning
- **Eigenvector** = direction (principal component axis)  
- **Eigenvalue** = variance (spread) along that direction  

📌 In 2D: If you draw an ellipse around the data cloud,  
- The **axes of the ellipse** = eigenvectors  
- The **lengths of the ellipse’s semi-axes** = \(\sqrt{\lambda_1}, \sqrt{\lambda_2}\)

---

## 6. Dimensionality Reduction
To reduce to `k` dimensions:
- Take top `k` eigenvectors (those with largest eigenvalues)  
- Project data:
\[
Z = X W_k
\]

where \( W_k \) is the matrix of top `k` eigenvectors.

---

## 7. PCA via SVD
In practice, PCA is often computed using **Singular Value Decomposition (SVD):**
\[
X = U \Sigma V^T
\]

- Columns of \(V\) = principal components (eigenvectors)  
- Squared singular values = eigenvalues  

---

## 8. Explained Variance
If eigenvalues are \(\lambda_1, \lambda_2, \dots, \lambda_d\):
\[
\text{Explained Variance Ratio}_i = \frac{\lambda_i}{\sum_{j=1}^d \lambda_j}
\]

This helps decide **how many components to keep**.

---

# ✅ Summary
1. Center data  
2. Compute covariance matrix  
3. Find eigenvectors & eigenvalues  
4. Eigenvectors = directions of max variance  
5. Eigenvalues = variance along those directions  
6. Keep top-k components → reduced representation
