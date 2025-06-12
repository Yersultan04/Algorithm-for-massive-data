Algorithms for Massive Data 

## Overview
This repository contains a reproducible pipeline that flags duplicated and near-duplicated reviews in the Amazon Books dataset. Link to Google Colab: https://colab.research.google.com/drive/1OPGhnIimioF4E8i_EzXM9crrc3aju8zH?usp=sharing
Technique summary:

* MinHash + LSH – narrows candidates by Jaccard similarity.  
* TF-IDF + approximate k-NN – confirms candidates by cosine similarity.

## Repository Layout
| Path | Purpose |
|------|---------|
| Data Project.ipynb | End-to-end notebook: data load, preprocessing, MinHash/LSH, TF-IDF k-NN, evaluation. |
| Report_for_Massive_Data_Project.pdf | Report describing the method and results. |

## Method in Brief

1. **Pre-process** reviews (language filter, tokenise, lower-case, stop words).
2. Build **128-perm MinHash** signatures and apply **banded LSH**.
3. Verify candidates with **exact Jaccard** and **cosine TF-IDF** tests.

## License

MIT – see `LICENSE`.
