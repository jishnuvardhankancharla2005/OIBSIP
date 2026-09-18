<div align="center">

  <!-- Animated Header Banner -->
  <img src="assets/banner.svg" alt="Sentiment Analysis & NLP Intelligence Lab Banner" width="100%" />

  <br/><br/>

  <!-- Dynamic Badges -->
  [![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/)
  [![Scikit-Learn](https://img.shields.io/badge/scikit--learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)](https://scikit-learn.org/)
  [![Pandas](https://img.shields.io/badge/pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)](https://pandas.pydata.org/)
  [![NLTK](https://img.shields.io/badge/NLTK-NLP%20Pipeline-339933?style=for-the-badge)](https://www.nltk.org/)
  [![Chart.js](https://img.shields.io/badge/Chart.js-v4.4.4-FF6384?style=for-the-badge&logo=chartdotjs&logoColor=white)](https://www.chartjs.org/)
  [![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?style=for-the-badge&logo=jupyter&logoColor=white)](https://jupyter.org/)
  [![Oasis Infobyte](https://img.shields.io/badge/Oasis%20Infobyte-Level%201%20Task%204-8B5CF6?style=for-the-badge)](https://oasisinfobyte.com/)

  <p align="center">
    <strong>An end-to-end Machine Learning and Natural Language Processing suite for multi-class customer sentiment classification, feature interpretability, and interactive visual analytics.</strong>
  </p>

  <p align="center">
    <a href="#-project-overview">Overview</a> •
    <a href="#-system-architecture">Architecture</a> •
    <a href="#-key-results--benchmarks">Benchmarks</a> •
    <a href="#-linguistic-insights">Linguistic Insights</a> •
    <a href="#-interactive-dashboard">Dashboard</a> •
    <a href="#-getting-started">Getting Started</a>
  </p>

</div>

---

## 🌟 Project Overview

Customer reviews are vital indicators of user experience and brand health. However, in large-scale eCommerce datasets like the **Amazon Fine Food Reviews (568,454 reviews)**, real-world data is heavily skewed toward positive ratings (~78% 5-star ratings). A naive classifier could predict "Positive" for every sample and falsely appear accurate without learning true sentiment signals.

This project delivers a **rigorous 3-class sentiment intelligence pipeline** by:
1. **Curating an 18,000-review class-balanced sample** (6,000 Negative, 6,000 Neutral, 6,000 Positive) to eliminate majority-class bias.
2. **Transforming raw unstructured text** with custom NLP tokenization, regex cleaning, and **TF-IDF N-Gram vectorization (5,000 features)**.
3. **Training & benchmarking statistical classifiers**: **Multinomial Naive Bayes** and **L2-Regularized Logistic Regression**.
4. **Deploying a zero-dependency standalone BI Intelligence Dashboard (`dashboard.html`)** offering confusion matrix heatmaps, feature coefficient inspection, review length boxplots, and a live sample prediction explorer.

---

## 🏗️ System Architecture

<div align="center">
  <img src="assets/architecture.svg" alt="NLP and ML Pipeline Architecture Diagram" width="100%" />
</div>

<br/>

### 🔄 End-to-End Pipeline Stages

| Stage | Component | Operations & Transformations | Artifacts / Output |
| :---: | :--- | :--- | :--- |
| **01** | **Raw Ingestion** | Ingestion of 568,454 Amazon Fine Food reviews | Raw text & 5-star ratings |
| **02** | **Sentiment Mapping** | Polarities mapped: 1–2★ (Negative), 3★ (Neutral), 4–5★ (Positive) | Discrete ternary labels |
| **03** | **Stratified Sampling** | Class-balanced subsetting (6,000 samples per class) | 18,000 balanced rows (`sampled_reviews.csv`) |
| **04** | **NLP Preprocessing** | Lowercasing, HTML/URL stripping, punctuation & contractions removal | Cleaned token sequences |
| **05** | **TF-IDF Vectorization** | Sublinear term frequency, unigram + bigram n-grams, top 5,000 features | Sparse feature matrix $\mathbf{X} \in \mathbb{R}^{18000 \times 5000}$ |
| **06** | **Model Training** | Multinomial Naive Bayes ($\alpha=1.0$) vs. Logistic Regression ($C=1.0$, L2) | Trained classifier weights & log-probs |
| **07** | **Evaluation & Audit** | 80/20 train-test split, per-class Precision/Recall/F1, Confusion Matrix | Classification reports & validation curves |
| **08** | **BI Dashboard** | Offline-capable reactive dashboard with Chart.js & dynamic test explorer | `dashboard.html` + standalone assets |

---

## 📊 Key Results & Benchmarks

Both models were evaluated on an **unseen 20% test partition (3,600 reviews)** across a balanced 3-class distribution (1,200 Negative, 1,200 Neutral, 1,200 Positive).

### 🏆 Model Comparison Matrix

| Model | Accuracy | Precision (Macro) | Recall (Macro) | F1-Score (Macro) | Strengths / Trade-offs |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Logistic Regression (L2)** | **68.44%** | **0.6840** | **0.6844** | **0.6842** | 🥇 **Best overall performer**; highly interpretable linear weights; superior handling of subtle positive/negative boundaries. |
| **Multinomial Naive Bayes** | **68.39%** | **0.6840** | **0.6839** | **0.6839** | ⚡ Extremely fast training & inference; strong baseline for bag-of-words text classification. |
| *Random Baseline* | *33.33%* | *0.3333* | *0.3333* | *0.3333* | *Theoretical baseline on a balanced 3-class dataset.* |

<br/>

### 🎯 Per-Class Performance Breakdown & Error Analysis

<div align="center">
  <img src="assets/confusion_matrix.svg" alt="Animated Confusion Matrix & Class Performance Heatmap" width="100%" />
</div>

<br/>

```
  Sentiment Class      Precision      Recall      F1-Score     Performance Gauge
  ───────────────────────────────────────────────────────────────────────────────
  Positive  (4–5★)       0.747         0.759       0.753       ███████████████░░  (75.3%)
  Negative  (1–2★)       0.696         0.690       0.693       ██████████████░░░  (69.3%)
  Neutral   (3★)         0.608         0.604       0.606       ████████████░░░░░  (60.6%)
  ───────────────────────────────────────────────────────────────────────────────
  Overall Macro Avg      0.684         0.684       0.684       █████████████░░░░  (68.4%)
```

> **Insight on Neutral Class Classification:**
> The **Neutral (3-star)** class has the lowest F1 score (60.6%) because customer reviews in this category inherently blend contradictory sentiments (e.g., *"tastes good but price is too high"*), making them the most challenging boundary in sentiment analysis.

---

## 🔍 Linguistic Insights & Explainability

### 1. Most Influential Sentiment Drivers (Logistic Regression Weights)

<div align="center">
  <img src="assets/feature_importance.svg" alt="Animated Top Feature Importance Predictors" width="100%" />
</div>

<br/>

<div align="center">

| 🔴 Top Negative Predictors | 🟡 Top Neutral Predictors | 🟢 Top Positive Predictors |
| :--- | :--- | :--- |
| `terrible` (+3.100) | `however` (+3.233) | `great` (+4.638) |
| `awful` (+2.847) | `okay` (+2.373) | `love` (+4.507) |
| `even` (+2.733) | `three star` (+2.319) | `best` (+3.973) |
| `worst` (+2.712) | `unfortunately` (+2.301) | `perfect` (+3.840) |
| `disappointing` (+2.550) | `still` (+2.279) | `delicious` (+3.576) |
| `horrible` (+2.517) | `though` (+1.894) | `excellent` (+3.387) |
| `disappointed` (+2.496) | `fine` (+1.825) | `favorite` (+3.116) |
| `waste money` (+2.048) | `little disappointed` (+1.572) | `highly recommend` (+2.291) |

</div>

<br/>

### 2. Review Length vs. Sentiment Analysis

<div align="center">
  <img src="assets/review_length_metrics.svg" alt="Animated Review Length Box Plots & Medians" width="100%" />
</div>

<br/>

- **Negative Reviews:** Median length **31 words** (IQR: 18 – 53 words). Reviewers provide elaborate descriptions explaining defects, packaging issues, or dissatisfaction.
- **Neutral Reviews:** Median length **33 words** (IQR: 19 – 58 words). Reviewers balance pros and cons across multiple sentences.
- **Positive Reviews:** Median length **26 words** (IQR: 16 – 45 words). Satisfied customers tend to leave short, punchy endorsements (*"Great flavor, loved it!"*).

---

## 💻 Interactive Analytics Dashboard

The project includes [`dashboard.html`](file:///d:/OIBSIP/DataAnalytics_Level1_Task4_Sentiment%20Analysis/dashboard.html), an interactive dashboard engineered with **Vanilla HTML5/CSS3** and **Chart.js**.

<details open>
<summary><strong>✨ Dashboard Highlights & Modules</strong></summary>
<br/>

1. **Live KPI Metric Ribbon:** Instant display of dataset size, sample distribution, vocabulary dimension, and top model accuracy.
2. **Distribution Comparison View:** Visualizes the skew of the 568K raw dataset vs. the 18K class-balanced sample.
3. **Floating Bar Length Distribution:** Custom Chart.js floating bars displaying 25th-75th percentiles with median markers.
4. **Interactive Model Switcher:** Real-time toggle between **Logistic Regression** and **Naive Bayes** with interactive **Confusion Matrix Heatmaps**.
5. **Feature Importance Explorer:** Dynamic bar charts showcasing top positive, neutral, and negative coefficient weights.
6. **Vocabulary Word Clouds:** Scaled word clusters for each sentiment category based on frequency analysis.
7. **Interactive Prediction Explorer:** Filter through 3,600 actual test predictions by ground truth, model outcome (Correct / Misclassified), and star rating.

</details>

---

## 📂 Repository Structure

```tree
DataAnalytics_Level1_Task4_Sentiment Analysis/
├── assets/
│   ├── banner.svg                 # Animated repository header banner
│   ├── architecture.svg           # Animated end-to-end pipeline diagram
│   ├── confusion_matrix.svg       # Animated confusion matrix & class gauges
│   ├── feature_importance.svg     # Animated top coefficient predictors
│   └── review_length_metrics.svg  # Animated IQR & median review length charts
├── chart.umd.min.js               # Local offline Chart.js v4.4.4 UMD bundle
├── dashboard.html                 # Interactive BI Intelligence Dashboard
├── sampled_reviews.csv            # 18,000 class-balanced sample dataset
├── Sentiment_Analysis.ipynb       # Jupyter Notebook with full EDA & ML code
├── Sentiment_Analysis.html        # Exported HTML version of the notebook
└── README.md                      # Project documentation
```

---

## 🚀 Getting Started

### 1. Prerequisites

Ensure you have **Python 3.8+** installed.

```bash
# Clone the repository
git clone https://github.com/your-username/Sentiment-Analysis-NLP.git
cd "DataAnalytics_Level1_Task4_Sentiment Analysis"
```

### 2. Install Dependencies

```bash
pip install numpy pandas scikit-learn nltk jupyter matplotlib seaborn
```

### 3. Run the Jupyter Notebook

Launch the notebook to inspect exploratory data analysis, text preprocessing, and model training:

```bash
jupyter notebook Sentiment_Analysis.ipynb
```

### 4. Launch the Interactive Dashboard

Simply double-click [`dashboard.html`](file:///d:/OIBSIP/DataAnalytics_Level1_Task4_Sentiment%20Analysis/dashboard.html) or open it in any modern browser. It loads offline using the included [`chart.umd.min.js`](file:///d:/OIBSIP/DataAnalytics_Level1_Task4_Sentiment%20Analysis/chart.umd.min.js) with zero external setup required!

```bash
# Alternatively, serve with Python's built-in HTTP server:
python -m http.server 8000
# Navigate to: http://localhost:8000/dashboard.html
```

---

## 🛠️ Tech Stack & Tools

<div align="center">

| Domain | Technologies & Libraries |
| :--- | :--- |
| **Language** | Python 3.10+, JavaScript (ES6+) |
| **Data Processing** | Pandas, NumPy |
| **NLP & ML** | Scikit-Learn (TF-IDF, MultinomialNB, LogisticRegression), NLTK, Regex |
| **Visualization** | Chart.js 4.4.4, Matplotlib, Seaborn |
| **UI & Styling** | HTML5, Vanilla CSS3 (Custom Glassmorphic Theme, Dark Mode) |

</div>

---

## 📜 License & Acknowledgements

* **Dataset:** [Amazon Fine Food Reviews Dataset](https://www.kaggle.com/datasets/snap/amazon-fine-food-reviews) (`sampled_reviews.csv`) — 18,000 stratified, class-balanced consumer food reviews engineered with TF-IDF n-grams for 3-class sentiment classification and text mining.
* **Internship Program:** OASIS INFOBYTE SIP (OIBSIP) — Data Analytics Internship Level 1, Task 4.
* **Developer:** [Jishnu Vardhan Kancharla](https://github.com/jishnuvardhankancharla2005)
* **License:** Distributed under the [MIT License](https://github.com/jishnuvardhankancharla2005/OIBSIP/blob/main/DataAnalytics_Level1_Task4_Sentiment%20Analysis/LICENSE).

---

<div align="center">
  <b>Developed for Oasis Infobyte Data Analytics Internship (Level 1 · Task 4)</b><br>
  <i>Built with precision engineering, clean design aesthetics, and advanced NLP text analytics.</i>
</div>
