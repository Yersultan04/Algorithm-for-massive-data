````markdown
# Duplicate-Review Detection in the Amazon Books Dataset

Algorithms for Massive Data – Project 1  
Bachelor / Master **Data Science for Economics**, University of Milan  
*June 2025*

---

## 🚀 Overview
This repository contains a fully-reproducible pipeline for **finding duplicated and near-duplicated book reviews** in the 3 M-review Amazon Books dataset. The notebook combines:

* **MinHash + LSH** to shortlist candidate pairs by Jaccard similarity.  
* **TF-IDF + Approximate k-NN** to verify candidates with cosine similarity. :contentReference[oaicite:0]{index=0}

On a 10 000-review subset the end-to-end run time is **\<10 min / \<3 GB RAM**, detecting 214 high-similarity pairs with **96 % precision, 84 % recall**. :contentReference[oaicite:1]{index=1}

---

## 📁 Repository Contents

| Path | Description |
|------|-------------|
| `Untitled2.ipynb` | Main Jupyter notebook: data ingestion, preprocessing, MinHash/LSH, TF-IDF k-NN, evaluation & visualisations. |
| `Report_for_Massive_Data_Project.pdf` | 8-page project report detailing methodology, experiments and discussion (source for this README). |
| `requirements.txt` | Exact Python package versions (tested on Python 3.10, Google Colab). |
| `data/` | Empty placeholder; the Kaggle-hosted raw CSV (≈2.9 GB) is downloaded automatically at first run. |

---

## ⚡ Quick Start

```bash
# 1. Clone and install
git clone https://github.com/<your-org>/duplicate-review-detection.git
cd duplicate-review-detection
pip install -r requirements.txt          # or !pip install -r requirements.txt in Colab

# 2. Open the notebook
jupyter lab Untitled2.ipynb              # or click the Colab badge at the top of the notebook

# 3. Choose a run mode
#    sample=True  – default 10 k reviews for fast experimentation
#    sample=False – full 3 M reviews (needs >16 GB RAM)
````

All random seeds are fixed for determinism; change the YAML block at the top of the notebook to tweak thresholds, sample size or MinHash parameters.

---

## 🔍 Methods in Brief

| Stage               | Key Steps                                                                                |
| ------------------- | ---------------------------------------------------------------------------------------- |
| **Pre-processing**  | Language filter → lower-casing → HTML & non-ASCII strip → tokenisation → stop-word drop. |
| **Jaccard path**    | 128-perm MinHash signatures → banded LSH → exact Jaccard verification (≥0.80).           |
| **Cosine path**     | TF-IDF matrix (sk-learn) → cosine k-NN (k=5) → threshold ≥0.85.                          |
| **Merge & Cluster** | Union of verified pairs → optional NetworkX graph to group duplicates.                   |

For an architecture diagram and full formulae refer to § 4 of the PDF report.&#x20;

---

## 📊 Sample Results

| Metric (10 k sample)    | Value              |
| ----------------------- | ------------------ |
| Duplicate pairs found   | **214**            |
| Unique reviews involved | 158                |
| Precision / Recall / F1 | 0.96 / 0.84 / 0.90 |

A histogram of cosine similarities and example duplicate clusters are generated automatically in the notebook.&#x20;

---

## 🖇️ Extending This Work

* Swap TF-IDF for **Sentence-BERT embeddings** to capture deeper paraphrases.
* Push to **100 k+ reviews** using FAISS or Milvus for vector search scalability.
* Add reviewer-behaviour features to flag coordinated spam campaigns.

---

## 📖 Citation

If you use this code, please cite the accompanying report:

```
[Student Name]. “Finding Similar Items in the Amazon Books Reviews Dataset.”
Algorithms for Massive Data – Project 1 Report. University of Milan, June 2025.
```

---

## 📝 License

MIT – see `LICENSE` file for details.

---

*Last updated: 12 Jun 2025*

```
```
