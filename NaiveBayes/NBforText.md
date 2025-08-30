# Naïve Bayes for Text Classification

---

## 1. Motivation (5 min)

- Text is unstructured → algorithms need numbers.  
- Example: "Win money now!" → we can’t directly feed words into Naïve Bayes.  
- Solution → **Vectorization techniques** (Count Vectorization, TF-IDF).  

**Question to students:**  
How can we turn text into numbers so that a model like Naïve Bayes can use it?

---

## 2. Bag of Words & Count Vectorization (10 min)

**Idea:** Represent each document by word counts.  
- Build a vocabulary (all unique words).  
- Each document = vector of word frequencies.  

**Example:**  
Corpus = ["Win money now", "Hello friend hello"]

Vocabulary = {Win, money, now, Hello, friend}

| Document | Win | money | now | Hello | friend |
|----------|-----|-------|-----|-------|--------|
| Doc1     | 1   | 1     | 1   | 0     | 0      |
| Doc2     | 0   | 0     | 0   | 2     | 1      |

**Notes:**  
- Easy and fast  
- Ignores word order (bag = unordered)  
- Leads to sparse vectors if vocabulary is large  

---

## 3. TF-IDF Representation (10 min)

**Problem with raw counts:**  
- Common words like "the", "is", "and" dominate.  

**Solution:** Term Frequency – Inverse Document Frequency (TF-IDF).  

- **Term Frequency (TF):** How often a word appears in a document.  
- **Inverse Document Frequency (IDF):** How unique a word is across all documents.  

Final Weight = `TF * IDF`  

**Example:**  
- Word = "money" → rare in corpus → high weight  
- Word = "the" → very common → low weight  

This emphasizes *important* words and down-weights common fillers.

---

## 4. Naïve Bayes for Text (10 min)

**Why it works well:**  
- Words are treated as independent features (Bag of Words assumption).  
- Text datasets are often high-dimensional → Naïve Bayes handles this efficiently.  
- Works surprisingly well as a baseline model.

**Formulation in text context:**  
We want to compute:

