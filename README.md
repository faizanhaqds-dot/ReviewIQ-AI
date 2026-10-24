# ReviewIQ AI: Customer Review Intelligence Platform

ReviewIQ AI is an NLP and machine-learning platform that classifies customer reviews as positive, neutral, or negative, and will later detect common complaints and key aspects (quality, delivery, price, packaging, customer service).

## Problem

Businesses receive a huge number of reviews, and star ratings don't explain *why* customers are happy or unhappy. A single review can mix opinions, e.g. "The product quality is excellent, but the delivery was late." ReviewIQ AI aims to analyze reviews automatically and give businesses useful insights.

## Target Users

- E-commerce businesses and online sellers
- Customer experience teams
- Product managers and marketing teams

## Dataset

- **Source:** SetFit Amazon Reviews Multi English dataset (Hugging Face)
- **Sample:** stratified, `random_state=42`
  - Train: 30,000 | Validation: 3,000 | Test: 3,000
- **Label mapping:**
  - Ratings 0, 1 → Negative
  - Rating 2 → Neutral
  - Ratings 3, 4 → Positive

## Data Preparation

- Checked missing values; removed duplicate reviews
- Lowercased text; removed HTML tags, URLs, special characters, extra spaces
- Removed empty reviews after cleaning
- Removed reviews appearing in more than one split (prevents data leakage)

**Final cleaned dataset (35,942 reviews):**

| Split      | Reviews |
|------------|---------|
| Train      | 29,960  |
| Validation | 2,992   |
| Test       | 2,990   |

## Feature Extraction

- TF-IDF with unigrams and bigrams, max 10,000 features
- Vectorizer fitted on training data only, then applied to validation and test data

| Matrix     | Shape            |
|------------|------------------|
| Train      | (29,960, 10,000) |
| Validation | (2,992, 10,000)  |
| Test       | (2,990, 10,000)  |

## Exploratory Data Analysis

- Sentiment distribution (14,376 negative, 14,374 positive, 7,192 neutral)
- Original rating distribution
- Review length distribution
- Review length by sentiment class

## Limitations

- Sarcasm and mixed opinions are hard for basic models
- Model may not generalize to other platforms
- Sentiment labels come from ratings, which may not always match the review text
- No personally identifiable information is used; review ID is only a record identifier

## Roadmap

- [x] Deliverable 1: problem definition, data acquisition, cleaning, EDA, TF-IDF features
- [ ] Train Naive Bayes, Logistic Regression, and SVM models
- [ ] Compare models using accuracy, precision, recall, and F1-score
- [ ] Aspect detection
- [ ] Recurring complaint detection
- [ ] Business recommendations
- [ ] Web application

## Tech Stack

Python, Google Colab, Hugging Face `datasets`, scikit-learn, pandas, matplotlib, seaborn

## Authors

- Emaad Faisal
- Faizan ul Haq

## References

1. SetFit. Amazon Reviews Multi English Dataset. Hugging Face.
2. Hugging Face. Datasets Library.
3. Scikit-learn Developers. Scikit-learn Machine Learning Library.# ReviewIQ-AI
ReviewIQ AI is an NLP and machine-learning platform that classifies customer reviews as positive, neutral, or negative (using TF-IDF features on a cleaned Amazon reviews dataset), with plans to add aspect detection, complaint tracking, and business recommendations.
