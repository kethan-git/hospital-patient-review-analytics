# Hospital Patient Review Analytics

A multi-method text and web analytics study of 3,110 Google Reviews across two branches of Sri Sathya Sai Institute of Higher Medical Sciences (SSSIHMS) - Whitefield, Bengaluru and Prasanthigram, Andhra Pradesh - covering reviews published between 2013 and 2026.

Built as a capstone project for an MBA Text & Web Analytics course.

---

## Overview

SSSIHMS is one of India's most distinctive healthcare institutions, providing completely free, world-class medical care to all patients regardless of economic background. This project analyses patient reviews to identify what is working, what isn't, how experiences have evolved over time, and what the administration should prioritise fixing - separately for each branch.

---

## Pipeline

| Phase | Method | Purpose |
|---|---|---|
| 1 | Exploratory Data Analysis | Baseline metrics, temporal trends, engagement patterns |
| 2 | Text Preprocessing | Cleaning, tokenisation, lemmatisation |
| 3 | Word Frequency & Clouds | Visual overview of dominant vocabulary |
| 4 | VADER Sentiment Analysis | Rule-based baseline sentiment scoring |
| 5 | ML Sentiment Classification | Supervised binary classifier (Logistic Regression) |
| 6 | LDA Topic Modelling | Unsupervised theme discovery per branch |
| 7 | Aspect-Based Sentiment Analysis | Granular sentiment across 8 hospital aspects |
| 8 | Named Entity Recognition | Department and location-level sentiment |

---

## Key Findings

**Branch 1 - Whitefield**
- 81.5% positive sentiment across 2,000 reviews
- Waiting Time (57.1% negative) and Appointments (50.6% negative) are critical pain points
- Every patient entry touchpoint - entrance, reception, main gate, security, counter - registers majority-negative sentiment
- Eye department (87.5% negative) and Emergency department (81.8% negative) require immediate attention
- Cleanliness is the standout strength at 94.1% positive

**Branch 2 - Prasanthigram**
- 87.9% positive sentiment across 1,110 reviews
- Cardiology, ophthalmology, and orthopaedics all at 100% positive
- Owner response rate of just 1.4% - critically low engagement with patient feedback
- Staff behaviour and waiting time are the primary concerns

**Cross-branch**
- Staff behaviour emerges as a distinct negative topic in both branches, confirmed independently by LDA, ABSA, and NER
- Unified Logistic Regression sentiment classifier achieves Macro F1 of 0.902

---

## Tech Stack

| Task | Library |
|---|---|
| Data wrangling | `pandas`, `numpy` |
| Visualisation | `matplotlib`, `seaborn`, `plotly` |
| Text preprocessing | `nltk`, `spacy` |
| Sentiment (rule-based) | `nltk` VADER |
| Sentiment (ML) | `scikit-learn` |
| Topic modelling | `scikit-learn` LDA |
| Topic selection | `gensim` coherence scoring |
| Word clouds | `wordcloud` |
| NER | `spacy` |
| Data collection | Apify Google Maps Reviews Scraper |

---

## Data

Reviews were collected via Apify's Google Maps Reviews Scraper in March 2026. Two CSV files are used:

- `sssihms_blr.csv` - Branch 1, Whitefield (2,000 reviews)
- `sssihms_ptp.csv` - Branch 2, Prasanthigram (1,110 reviews)

Raw data files are not included in this repository. To replicate the data collection, use the [Apify Google Maps Reviews Scraper](https://apify.com/compass/google-maps-reviews-scraper) with the respective Google Maps URLs for each branch.

---

## Notebook Structure

The notebook `TWA_SSSIHMS_.ipynb` is organised into the following sections:

1. Setup & Data Loading
2. Data Preparation & EDA
3. Text Preprocessing
4. Word Frequency & Cloud Analysis
5. VADER Sentiment Analysis
6. ML Sentiment Classification
7. LDA Topic Modelling
8. Aspect-Based Sentiment Analysis
9. Named Entity Recognition
10. Branch Comparison

---

## Methodological Notes

- **Sentiment labelling:** Binary scheme - reviews with 1–3 stars labelled negative, 4–5 stars labelled positive. Three-star reviews (3.1% of dataset) were conservatively assigned to the negative class after qualitative inspection revealed a recurring mixed-sentiment pattern.
- **Data leakage correction:** An 80.9% overlap between Branch 2 reviews and the combined training set was identified and corrected by splitting each branch into train/test sets before combining for training.
- **LDA topic selection:** Standard metrics (perplexity, coherence) produced inconclusive results on the small corpus. Five topics per branch was selected based on dataset size constraints and domain knowledge, with bigram frequency analysis used to inform topic labelling.
- **Clustering:** K-Means clustering on TF-IDF vectors yielded consistently low silhouette scores (0.009–0.026), confirming that patient reviews do not form well-separated natural clusters - validating LDA's mixed-membership approach as the appropriate model.

---

## SDG Alignment

This project aligns with:
- **SDG 3** - Good Health and Well-Being: surfacing barriers to quality healthcare delivery
- **SDG 10** - Reduced Inequalities: identifying and documenting staff classism directed at economically disadvantaged patients
- **SDG 17** - Partnerships for the Goals: demonstrating how publicly available data can serve as an accountability mechanism for social institutions

---

## Requirements 

pandas
numpy
matplotlib
seaborn
plotly
nltk
spacy
scikit-learn
gensim
wordcloud
tqdm

--- 

Install with:
```bash
pip install pandas numpy matplotlib seaborn plotly nltk spacy scikit-learn gensim wordcloud tqdm pyLDAvis
python -m spacy download en_core_web_sm
```

---

## Academic Context

MBA Capstone Project - Text & Web Analytics
April 2026
