# Part 1: Introduction & Intuition (30 min)

---

## 1. Warm-up Discussion (5 min)

- How do we decide if an email is *spam* or *not spam*?  
- What clues (words, sender, subject line) do we usually look for?  


---

## 2. What is Naïve Bayes? (10 min)

- **Naïve Bayes** is a **probabilistic classifier**.  
- It is based on **Bayes’ Theorem** (probability of an event given prior knowledge).  
- Called **“Naïve”** because it assumes that all features are **independent** of each other.  

**Analogy:**  
- Imagine diagnosing a disease based on symptoms.  
- Naïve Bayes assumes each symptom contributes **independently** to the probability of the disease, even if in reality some symptoms are related.  

---

## 3. Real-world Applications (5 min)

-  **Spam Detection**: Identify spam emails.  
-  **Sentiment Analysis**: Predict if a review is positive or negative.  
-  **Medical Diagnosis**: Predict a disease given symptoms.  
-  **Document Classification**: Classify news articles, emails, etc.  

 **Class Activity:**  
- *Which of these applications do you encounter daily?*  

---

## 4. Intuition with a Simple Example (7 min)

**Sentence:**  
*"Win money now"*  

- If the email contains **“Win”**, probability of spam increases.  
- If it contains **“Hello”**, probability of spam decreases.  

**Table Example:**  

| Word   | P(word | spam) | P(word | not spam) |
|--------|---------|-----------------|
| Win    | 0.8     | 0.1             |
| Money  | 0.7     | 0.2             |
| Hello  | 0.2     | 0.7             |

- For *"Win money now"*, Naïve Bayes combines these probabilities.  
- Each word contributes **independently** to the final decision.  

 **Mini Exercise:**  
- *If you saw the word “Free” in an email, would you consider it spammy? Why?*  

---

## 5. Transition to Next Section (3 min)

- So far, we’ve seen **intuition and examples**.  
- But how does Naïve Bayes actually **calculate probabilities**?  
- Next, we’ll dive into the **mathematics** behind it.  

---
