# Finding Similar Items — NYT Comments 2020

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/YOUR_USERNAME/YOUR_REPO/blob/main/Finding_Similar_Items.ipynb)

This project is made for the exam of **Algorithms for Massive Datasets** — MSc Computer Science, Università degli Studi di Milano, 2025–26.

**Author:** Aliza Aziz — 82838A  
**Instructor:** Prof. Dario Malchiodi

---

## About

The goal is to find similar and near-duplicate reader comments from the New York Times 2020 dataset using **MinHashing** and **Locality Sensitive Hashing (LSH)**, following Chapter 3 of *Mining of Massive Datasets* (Leskovec, Rajaraman, Ullman).

With ~19.9 million comments, there are around 450 million possible pairs to compare. Doing it naively is completely infeasible. LSH brings this down to a tiny fraction of comparisons while still finding the similar ones.

Everything is implemented from scratch in Python. No sklearn, no datasketch, just pandas, numpy, and matplotlib for the basics.

---

## Dataset

**New York Times Articles & Comments 2020**  
→ [Kaggle link](https://www.kaggle.com/datasets/benjaminawd/new-york-times-articles-comments-2020)

About 2 GB compressed, ~19.9M comments across 10 part files. The dataset is downloaded automatically at runtime. It is not included in this repo.

---

## How to run

### Google Colab (easiest)

Click the badge above, then add your Kaggle credentials in Cell 2:

```python
os.environ['KAGGLE_USERNAME'] = "your_username"
os.environ['KAGGLE_KEY']      = "your_key"
```

Then run all cells. Takes about 2 minutes on a free Colab CPU.


---

## Pipeline

```
Comments → Shingling → MinHashing → LSH → Similar Pairs
```

- **Shingling** — each comment becomes a set of hashed 5-character windows
- **MinHashing** — each shingle set is compressed into a 128-integer signature
- **LSH** — signatures are split into 32 bands; comments matching in any band become candidates
- **Verification** — candidates are scored and filtered by Jaccard similarity ≥ 0.5

---

## Parameters

Set in Cell 1. Defaults are tuned for a fast run:

| Variable | Default | Description |
|----------|---------|-------------|
| `MAX_COMMENTS` | 30000 | How many comments to load |
| `K_SHINGLE` | 5 | Shingle window size |
| `N_HASH` | 128 | Signature length |
| `N_BANDS` | 32 | LSH bands |
| `SIMILARITY_THRESHOLD` | 0.5 | Minimum Jaccard to report |
| `SUBSAMPLE` | True | Set False for full data |

---

## Results

For each similar pair found, the notebook shows the comment text, article ID, similarity score, and whether both comments are from the same article. A histogram of similarity scores is also generated.

---


## Declaration

> *"I declare that this material, which I now submit for assessment, is entirely my own work and has not been taken from the work of others, save and to the extent that such work has been cited and acknowledged within the text of my work."*
