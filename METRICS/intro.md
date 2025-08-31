# Evaluation Metrics for Classification

When evaluating classifiers (like Naïve Bayes), accuracy alone may not be enough.  
We use additional metrics to capture different aspects of performance.  

---

## 1. Precision-Recall AUC (PR-AUC)

- **Precision**: Of all predicted positives, how many are actually positive?
- **Recall**: Of all actual positives, how many did we predict correctly?
- **PR Curve**: Plots Precision vs. Recall at different thresholds.
- **PR-AUC**: The area under the PR curve. Higher is better.

### Why use PR-AUC?
- Useful when classes are **imbalanced**.
- AUC closer to 1 means better separation of positive vs. negative classes.

**Formula:**
Precision = TP / (TP + FP)
Recall = TP / (TP + FN)

yaml
Copy code

---

## 2. Log Loss (Cross-Entropy Loss)

- Measures how close predicted probabilities are to true labels.
- Penalizes wrong predictions with **high confidence** more heavily.

**Formula:**
LogLoss = - (1/N) * Σ [ y*log(p) + (1-y)*log(1-p) ]

yaml
Copy code

- `y` = true label (0 or 1)  
- `p` = predicted probability for class 1  
- Lower Log Loss = better calibrated probabilities  

---

## 3. Matthews Correlation Coefficient (MCC)

- A **balanced measure** even for imbalanced datasets.
- Takes into account **TP, TN, FP, FN**.

**Formula:**
MCC = (TPTN - FPFN) / sqrt((TP+FP)(TP+FN)(TN+FP)(TN+FN))

yaml
Copy code

- Range: -1 to +1
  - +1 = perfect prediction
  - 0 = random prediction
  - -1 = total disagreement

---

## 4. Cohen’s Kappa

- Measures agreement between predictions and true labels, correcting for chance.

**Formula:**
Kappa = (p_o - p_e) / (1 - p_e)

markdown
Copy code

- `p_o`: observed agreement = accuracy
- `p_e`: expected agreement by chance

- Range: -1 to 1
  - 1 = perfect agreement
  - 0 = agreement no better than chance
  - <0 = worse than random

---

## 5. Balanced Accuracy

- Average of recall across classes.
- Adjusts for **imbalanced classes**.

**Formula:**
Balanced Accuracy = (Recall_class1 + Recall_class2 + ... + Recall_classN) / N

python
Copy code

- Ensures minority class performance is not ignored.

---

## Example: Computing Metrics in Python

```python
from sklearn.metrics import (
    precision_recall_curve, average_precision_score,
    log_loss, matthews_corrcoef, cohen_kappa_score,
    balanced_accuracy_score
)


print("MCC:", mcc)
print("Cohen's Kappa:", kappa)
print("Balanced Accuracy:", bal_acc)
