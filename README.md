# ESG Greenwashing Detection — NLP Analysis

> Do companies with better ESG scores actually write differently in their sustainability reports?

![Python](https://img.shields.io/badge/Python-3.14-blue) ![FinBERT](https://img.shields.io/badge/NLP-FinBERT-green) ![ESG](https://img.shields.io/badge/ESG-Sustainalytics-orange)

---

## Origin

It all started two days ago, on a volleyball court. During an amateur tournament, while waiting for my game, I noticed something: players call their own fouls very differently depending on the context. Without a proper referee or cameras, it's just easier to stay quiet and take the point.

I study at ISEG. I'm not the kind of student who spends their life in the library or buried in books — but apparently I've absorbed enough to connect a volleyball foul to corporate sustainability reporting. The parallel was immediate: *is the same true for companies?* Do firms with poor ESG performance use more positive language in their sustainability reports to compensate — or does the language actually reflect reality?

I wanted to build the model first, find the answer myself, and only then compare it to what the academic literature had already figured out.

---

## What I built

### Dataset
S&P 500 ESG Risk Ratings from Kaggle (Sustainalytics, 2023), covering 503 companies. From these, 17 were selected via stratified sampling across the full ESG risk spectrum — from Negligible to Severe.

### Pipeline

```
PDF download → pdfplumber → NLTK cleaning → keyword sampling → FinBERT → Pearson correlation
```

Sustainability reports were extracted, cleaned, and chunked. ESG-relevant chunks were selected via keyword-based stratified sampling and passed through FinBERT for sentiment scoring. Positive sentiment scores were then correlated against Sustainalytics ESG risk ratings.

---

## Results

| Metric | Value |
|---|---|
| Companies analysed | 17 |
| Pearson r | 0.176 |
| p-value | 0.499 |
| Avg neutral score | 0.83 |

**Main finding:** No statistically significant correlation between positive sentiment in sustainability reports and ESG risk score (r = 0.176, p = 0.499). Across all 17 companies — from Negligible to Severe ESG risk — the language remains uniformly neutral, averaging a sentiment score of 0.83. The language does not reflect the underlying performance.

### Notable outliers

| Company | ESG Risk | Sentiment | Note |
|---|---|---|---|
| General Electric | Severe | negative 0.215 | High ESG risk, unusually negative tone |
| Occidental Petroleum | Severe | positive 0.149 | High risk, positive framing — classic greenwashing signal |
| Hasbro | Negligible | negative 0.157 | Low risk, unexpectedly negative tone |

---

## Interpretation

The absence of correlation is itself the finding. In a world where greenwashing were widespread and detectable via sentiment, we would expect companies with poor ESG scores to write more positively — inflating their narrative. Instead, language is flat across the board.

One hypothesis: S&P 500 companies operate under intense external scrutiny — analyst coverage, ESG ETF inclusion, regulatory pressure, media attention. This scrutiny acts as a disciplining force that homogenises language regardless of underlying performance. Companies don't write well because they perform well. They write carefully because they are watched carefully.

---

## What the literature says

Having reached a conclusion independently, I then looked at what existing research had found — and the convergence was striking.

**Zhu et al. (2025) — "The Disclosure Fog", International Journal of Finance & Economics**
Using data from Chinese heavily polluting firms (2012–2021), finds that institutional investors encourage publishing sustainability reports but simultaneously discourage the use of sustainability-related language within them. Scrutiny shapes tone, not virtue — directly consistent with the finding here.

**Lagasio (2024) — NLP-based ESG-washing severity index**
Proposes an automated severity index to quantify ESG-washing in sustainability reports using NLP. Demonstrates that textual analysis can support regulatory supervision — a more sophisticated version of the pipeline built here, arriving at similar conclusions.

**CEE Greenwashing Study (MDPI, 2026) — 204 firms, Central & Eastern Europe**
Constructs a Greenwashing Severity Index comparing corporate ESG self-representation with external media narratives. Finds moderate but widespread greenwashing, with substantial heterogeneity linked to differences in regulatory maturity — exactly the cross-scrutiny comparison this project could not test.

**ScienceDirect (2025) — Negative media coverage and ESG rating divergence**
Shows that media pressure induces information disclosure manipulation, with the effect more pronounced in firms with low institutional investor presence. Where scrutiny is absent, divergence grows.

---

## The open question

*In amateur volleyball, players call their own fouls. Without referees, cameras, or scoreboards, the temptation to stay silent and take the point is real — and often acted on. In professional matches, the system of control makes that choice irrelevant: the foul is called regardless.*

*S&P 500 companies are the professional athletes. Their language is disciplined not by ethics, but by the infrastructure watching them — analysts, ESG ratings agencies, ETF inclusion criteria, regulatory scrutiny. The language is flat because the referees are always on the court.*

*The question this project cannot answer — but that the literature begins to address — is what happens on the amateur courts: the mid-cap firms, the emerging market conglomerates, the companies outside the cone of institutional visibility. Do they write more honestly, or more recklessly? Does the absence of scrutiny reveal virtue or expose it?*

That is a question for a dataset that doesn't yet exist in clean, accessible form — and for a future iteration of this project.

Oh — and we won the tournament.

---

## Tech stack

`Python 3.14` `pdfplumber` `NLTK` `FinBERT` `pandas` `scikit-learn` `plotly` `transformers` `torch`

---

*Dataset: S&P 500 ESG Risk Ratings — Kaggle (Sustainalytics, 2023) · Sample: 17 companies · Reports: 2021–2022 sustainability PDFs*
