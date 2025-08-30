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

**TF Formula:**

$$
TF(t, d) = \frac{\text{Number of times term t appears in document d}}{\text{Total number of terms in document d}}
$$

**IDF Formula:**

$$
IDF(t, D) = \log \left( \frac{\text{Total number of documents}}{\text{Number of documents containing term t}} \right)
$$


**Example:**  
- Word = "money" → rare in corpus → high weight  
- Word = "the" → very common → low weight  

This emphasizes *important* words and down-weights common fillers.

**Example**
  -Doc1: "The cat sat on the mat"
  -Doc2: "The dog played in the park"
  -Doc3: "Cats and dogs are great pets"

**TF for term "cat":**

- Doc1: "the cat sat on the mat" → 6 words  
  - "cat" appears 1 time → TF = 1/6 ≈ 0.167  

- Doc2: "the dog barked loudly" → 4 words  
  - "cat" appears 0 times → TF = 0  

- Doc3: "a cat and a dog" → 6 words  
  - "cat" appears 1 time → TF = 1/6 ≈ 0.167
 
    

**IDF for term "cat":**

- "cat" appears in **Doc1** and **Doc3** → 2 out of 3 documents  
- IDF("cat") = log(3 / 2) ≈ 0.176



**Scores for "cat":**

- Doc1: 0.167 × 0.176 ≈ 0.029  
- Doc2: 0 × 0.176 = 0  
- Doc3: 0.167 × 0.176 ≈ 0.029


- Why does "cat" get the same TF-IDF score in Doc1 and Doc3,  
  even though Doc3 might use a variant like **"cats"**?  
---

---

## 4. Naïve Bayes for Text (10 min)

**Why it works well:**  
- Words are treated as independent features (Bag of Words assumption).  
- Text datasets are often high-dimensional → Naïve Bayes handles this efficiently.  
- Works surprisingly well as a baseline model.

**Formulation in text context:**  
We want to compute:

P(Class | Words) ∝ P(Class) * P(word1|Class) * P(word2|Class) * ...


- **Prior:** Probability of each class (e.g., spam vs not spam).  
- **Likelihood:** Estimated from word frequencies (using Count/TF-IDF vectors).  

---

## 5. Practical Implementation Notes (5 min)

In scikit-learn:
- `CountVectorizer` → converts text to Bag of Words  
- `TfidfVectorizer` → converts text to TF-IDF  
- Naïve Bayes classifiers:  
  - `MultinomialNB` → works well for counts and TF-IDF  
  - `BernoulliNB` → good for binary presence/absence of words  

**Workflow:**
1. Collect documents and labels  
2. Preprocess text (lowercase, remove punctuation, stopwords, etc.)  
3. Vectorize using CountVectorizer or TfidfVectorizer  
4. Train Naïve Bayes model (`MultinomialNB`)  
5. Predict class of new text  

---

## 6. Example Code Snippet (Python)

```python
from sklearn.feature_extraction.text import CountVectorizer, TfidfVectorizer
from sklearn.naive_bayes import MultinomialNB
from sklearn.pipeline import make_pipeline

# Sample data
docs = ["Win money now", "Hello friend", "Claim your prize", "Hello again"]
labels = ["spam", "ham", "spam", "ham"]

# Pipeline with TF-IDF + Naïve Bayes
model = make_pipeline(TfidfVectorizer(), MultinomialNB())
model.fit(docs, labels)

# Test prediction
print(model.predict(["Win a prize now!"]))

