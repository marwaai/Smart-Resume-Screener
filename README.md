
# 🚀 Smart Resume Screener – Semantic AI Career Matcher

An end-to-end AI-powered resume screening system that goes beyond naive keyword matching.
In this project, I built a semantic resume–job matching engine using modern NLP techniques to fairly and accurately evaluate candidates while eliminating common industry biases.

---

## 📌 Problem Statement

Traditional resume screening systems suffer from several critical issues:

❌ Heavy dependence on keyword matching, ignoring semantic meaning
❌ Length bias, where long resumes dilute relevant skill signals
❌ Uninterpretable similarity scores that confuse recruiters
❌ Binary accept/reject logic that ignores candidate versatility

My goal was to design a system that **ranks candidates semantically**, not superficially.

---

## ✨ Key Technical Innovations

### 1️⃣ Sliding Window Chunking — Solving Length Bias

**Problem**
Long resumes reduce cosine similarity because embeddings average irrelevant content.

**Solution**
I split each resume into overlapping chunks (250–400 characters), embed each chunk independently, and apply **global max pooling** across all chunk–job similarities.

**Why this works**
Even if a candidate’s strongest experience appears deep inside a long resume, the model still captures the highest-relevance segment.

---

### 2️⃣ Square-Root Score Boosting — Human-Centered UX

**Problem**
Raw cosine similarity values (e.g., 0.54) appear misleadingly low to non-technical users.

**Solution**
I apply a monotonic square-root scaling function:

```
final_score = sqrt(cosine_similarity) × 100
```

**Result**

* Preserves ranking order
* Produces intuitive 0–100% confidence scores
* Never inflates similarity beyond logical bounds

This improves user trust without compromising mathematical correctness.

---

## 🧪 Validation & Stress Testing

To ensure the model truly understands professional relevance, I implemented a **Random Baseline validation strategy**.

### 🔬 Dataset

Hugging Face Resume Screening Dataset

### 🧠 Experiment

I deliberately mismatched resumes with unrelated job descriptions
(e.g., Nurse resume ↔ DevOps job)

### 📊 Results

| Scenario        | Mean Similarity |
| --------------- | --------------- |
| Correct Matches | ~54.23%         |
| Random Pairs    | ~39.62%         |

✅ The ~15% gap demonstrates that the model captures **semantic professional context**, not just shared English vocabulary.

---

## 🛠️ Tech Stack

### Core AI

* Sentence-Transformers (`all-MiniLM-L6-v2`)
* High-speed semantic embeddings

### NLP & NER

* spaCy (`en_core_web_sm`)
* Name and organization extraction

### Backend

* Flask
* REST-based request handling

### Preprocessing

* pdfplumber (PDF parsing)
* python-docx (DOCX parsing)

### Data Science & ML

* PyTorch
* Pandas, NumPy
* Scikit-learn

---

## 🧠 Key Takeaways

✅ Eliminates resume length bias
✅ Semantic-first ranking instead of keyword hacks
✅ Interpretable, human-friendly scores
✅ Validated against random baselines

---

## 📌 Future Improvements

* Resume section weighting (Experience > Skills > Education)
* Skill-level and proficiency extraction
* Multilingual resume support
* Recruiter dashboard analytics
