# Bayes’ Theorem in Classification (20 min)

---

## 1. Recap & Motivation (2 min)

👉 Last time we saw that Naïve Bayes uses **Bayes’ Theorem**.  
Now let’s dig deeper: **How does Bayes’ Theorem help in classification?**

**Reminder:**  
- We want to classify an email into **Spam** or **Not Spam**.  
- We observe evidence (e.g., words like “Win”, “Hello”).  
- Bayes’ Theorem lets us flip the problem: from **P(Class | Evidence)** to **P(Evidence | Class).**

---

## 2. Bayes’ Theorem Refresher (5 min)

$$
P(A|B) = \frac{P(B|A) \cdot P(A)}{P(B)}
$$

- **Posterior**: \( P(A|B) \) → probability of hypothesis after seeing evidence.  
- **Prior**: \( P(A) \) → initial belief before evidence.  
- **Likelihood**: \( P(B|A) \) → probability of seeing evidence if hypothesis is true.  
- **Evidence**: \( P(B) \) → total probability of evidence.  

👉 **Analogy:**  
- Hypothesis: *The email is Spam.*  
- Evidence: *The word "Win" appears.*  
- Bayes’ theorem tells us: *Given "Win," how likely is Spam?*

---

## 3. Bayes’ Theorem in Classification (5 min)

General formula for a class \(C\) and features \(x_1, x_2, \dots, x_n\):

$$
P(C | x_1, x_2, \dots, x_n) = \frac{P(C) \cdot P(x_1, x_2, \dots, x_n | C)}{P(x_1, x_2, \dots, x_n)}
$$

- Numerator = Prior × Likelihood  
- Denominator = Evidence (normalizes across classes)  

Since Evidence is constant across classes, we can compare:

$$
P(C | x_1, x_2, \dots, x_n) \propto P(C) \prod_{i=1}^{n} P(x_i|C)
$$

👉 This is the heart of **Naïve Bayes classification**.

---

## 4. Worked Example (7 min)

Suppose we have the following dataset:

- **P(Spam) = 0.5**, **P(Not Spam) = 0.5**  
- P("Win" | Spam) = 0.8, P("Win" | Not Spam) = 0.1  
- P("Hello" | Spam) = 0.2, P("Hello" | Not Spam) = 0.7  

---

### Case: New email → "Win Hello"

- For Spam:  
$$
P(Spam | Win, Hello) \propto P(Spam) \cdot P(Win|Spam) \cdot P(Hello|Spam)
$$  
$$
= 0.5 \times 0.8 \times 0.2 = 0.08
$$

- For Not Spam:  
$$
P(NotSpam | Win, Hello) \propto P(NotSpam) \cdot P(Win|NotSpam) \cdot P(Hello|NotSpam)
$$ 
$$
= 0.5 \times 0.1 \times 0.7 = 0.035
$$

 Since **0.08 > 0.035**, classify as **Spam**.

---

## 5. Quick Student Activity (3 min)

- Present 2 short subject lines:  
  1. "Hello Friend"  
  2. "Win a Prize"  

Ask students to compute which class is more likely (Spam vs Not Spam) given the same probabilities.  

**Discussion Prompt:**  
- What happens if both classes give *very small probabilities*?  
- How does Laplace smoothing help in such cases? (tease for later)

---

## 6. Transition (1–2 min)

- We now understand **how Bayes’ Theorem is applied in classification.**  
- Next, we’ll move into **implementation examples** (with datasets and scikit-learn).
