# Introduction & Intuition

---

## 1. Warm-up Discussion 

- How do we decide if an email is *spam* or *not spam*?  
- What clues (words, sender, subject line) do we usually look for?  


---

## 2. What is Naïve Bayes? 

- **Naïve Bayes** is a **probabilistic classifier**.  
- It is based on **Bayes’ Theorem** (probability of an event given prior knowledge).  
- Called **“Naïve”** because it assumes that all features are **independent** of each other.  

**Analogy:**  
- Imagine diagnosing a disease based on symptoms.  
- Naïve Bayes assumes each symptom contributes **independently** to the probability of the disease, even if in reality some symptoms are related.  

---

## 3. Real-world Applications 

-  **Spam Detection**: Identify spam emails.  
-  **Sentiment Analysis**: Predict if a review is positive or negative.  
-  **Medical Diagnosis**: Predict a disease given symptoms.  
-  **Document Classification**: Classify news articles, emails, etc.  

 **Class Activity:**  
- *Which of these applications do you encounter daily?*  

---

## 4. Intuition with a Simple Example 

**Sentence:**  
*"Win money now"*  

- If the email contains **“Win”**, probability of spam increases.  
- If it contains **“Hello”**, probability of spam decreases.  

**Table Example:**  

| Word   | P(word \| spam) | P(word \| not spam) |
|--------|----------------|-------------------|
| Win    | 0.8            | 0.1               |
| Money  | 0.7            | 0.2               |
| Hello  | 0.2            | 0.7               |

- For *"Win money now"*, Naïve Bayes combines these probabilities.  
- Each word contributes **independently** to the final decision.  

 **Mini Exercise:**  
- *If you saw the word “Free” in an email, would you consider it spammy? Why?*  
- *Congratulations, you won a prize!* — Spam or Not Spam?
- Similarily, what do you think about
   - “Free vacation now”
   - “Meeting tomorrow at 10am”
   - “Claim your prize”
   - “Project update attached”

## Visual Intuition: Probability Tree

Let’s build a simple example with a **tiny dataset** of emails:

- 10 spam emails, 8 contain "Win", 2 contain "Hello"  
- 10 not-spam emails, 1 contains "Win", 7 contain "Hello"  

So:  
- P(Spam) = 10 / 20 = 0.5  
- P(Not Spam) = 10 / 20 = 0.5  

Conditional probabilities:  
- P("Win" | Spam) = 8 / 10 = 0.8  
- P("Hello" | Spam) = 2 / 10 = 0.2  
- P("Win" | Not Spam) = 1 / 10 = 0.1  
- P("Hello" | Not Spam) = 7 / 10 = 0.7

```mermaid
flowchart TD
  E[Email]
  E --> S[Spam (0.5)]
  E --> N[Not Spam (0.5)]
  S --> SW["Win (0.8)"]
  S --> SH["Hello (0.2)"]
  N --> NW["Win (0.1)"]
  N --> NH["Hello (0.7)"]
```


```text
[Email]
├─ Spam (0.5)
│  ├─ "Win"    0.8
│  └─ "Hello"  0.2
└─ Not Spam (0.5)
   ├─ "Win"    0.1
   └─ "Hello"  0.7
```

---

### Probability Tree

---

## 5. Transition to Next Section 

- So far, we’ve seen **intuition and examples**.  
- But how does Naïve Bayes actually **calculate probabilities**?  
- Next, we’ll dive into the **mathematics** behind it.  

---
