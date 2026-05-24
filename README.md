# ESG Greenwashing Detection — NLP Analysis of S&P 500 Sustainability Reports

`Python` `FinBERT` `pdfplumber` `Plotly` `NLTK`

---

## Question

Does the language used in corporate sustainability reports reflect actual ESG 
performance, or is it strategically optimistic regardless of real-world impact?

---

## What I Did

Built an end-to-end NLP pipeline to test whether FinBERT sentiment scores 
extracted from 17 S&P 500 sustainability reports correlate with real ESG risk 
ratings from Sustainalytics.

**Sample:** 17 companies selected via stratified distribution across ESG risk 
tiers (Negligible → Severe), based on S&P 500 ESG Risk Ratings dataset (Kaggle)

**Pipeline:**
1. PDF text extraction — pdfplumber
2. Text cleaning — NLTK stopword removal and normalization  
3. Sentiment analysis — FinBERT with keyword-based stratified chunk sampling
4. Statistical comparison — Pearson correlation vs real ESG risk scores

---

## Results

| Metric | r | p-value | Significant |
|--------|---|---------|-------------|
| ESG Risk vs Positive Sentiment | 0.176 | 0.499 | No |
| ESG Risk vs Negative Sentiment | 0.008 | 0.976 | No |

Average neutral sentiment across all reports: **0.83**

**Key outliers:**
- General Electric (Severe) → negative: 0.215 — consistent with public controversies
- Occidental Petroleum (Severe) → positive: 0.149 — diverges from ESG rating
- Hasbro (Negligible) → negative: 0.157 — conservative, transparent language

---

## Interpretation

No significant correlation was found. S&P 500 companies operate under 
constant ESG scrutiny — institutional investors, rating agencies, regulators. 
The result is homogenized report language: technically neutral regardless of 
underlying performance. Greenwashing, if present at scale, may be more visible 
in less scrutinized companies outside mainstream ESG coverage.

---

## Limitations and Future Work

- n = 17 limits statistical power
- FinBERT does not capture strategic ambiguity or technical obfuscation
- Next: same pipeline on large-cap companies with lower ESG media exposure

---

## Tech Stack

| Tool | Purpose |
|------|---------|
| pdfplumber | PDF text extraction |
| NLTK | Text cleaning |
| FinBERT (ProsusAI) | Financial sentiment analysis |
| pandas | Data manipulation |
| Plotly | Interactive visualizations |
| scipy | Pearson correlation |