# EmoLens Dataset — Kryonara AI Lab Challenge #001

<div align="center">

![Kryonara AI Lab](https://img.shields.io/badge/Kryonara-AI%20Lab-0f172a?style=for-the-badge&logoColor=white)
![Challenge](https://img.shields.io/badge/Challenge-%23001-2563eb?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-OPEN-22c55e?style=for-the-badge)
![License](https://img.shields.io/badge/License-CC%20BY--NC%204.0-94a3b8?style=for-the-badge)

**Can your model read between the lines?**

*Predict nuanced human emotion from text and context — beyond positive and negative.*

 [Submit Results](#submission)

</div>

---

## Overview

Sentiment analysis has been solved. Positive. Negative. Neutral. Done.

But human emotion is not binary — and anyone who has ever misread a text message knows that.

**EmoLens** is a natural language understanding challenge that pushes beyond surface-level sentiment into the territory of nuanced, multi-dimensional human emotion. Given a short piece of text and its contextual metadata, your goal is to classify the underlying emotion from a rich label set spanning frustration, excitement, sarcasm, anxiety, joy, disappointment, pride, and more.

This is the problem at the heart of every AI product that tries to understand people — customer support bots, mental health tools, social listening platforms, and conversational agents. It is hard. It is unsolved. And it matters.

EmoLens is **Challenge #001** from Kryonara AI Lab — the first of many.

---

## The Task

**Input:** A short text sample (tweet, chat message, review, or support ticket) and contextual metadata including platform, topic category, and time of day.

**Output:** A predicted emotion label from the following 8 classes:

| Label | Description |
|---|---|
| `joy` | Genuine happiness or delight |
| `excitement` | High-energy anticipation or enthusiasm |
| `frustration` | Blocked goals, irritation, or annoyance |
| `anxiety` | Worry, nervousness, or uncertainty |
| `sarcasm` | Ironic or mocking tone |
| `disappointment` | Unmet expectations or letdown |
| `pride` | Accomplishment or self-satisfaction |
| `neutral` | No strong emotional signal |

---

## Dataset

### Files

| File | Rows | Description |
|---|---|---|
| `train.csv` | 12,000 | Labeled training data |
| `test.csv` | 3,000 | Unlabeled test data for prediction |
| `sample_submission.csv` | 3,000 | Correct submission format |

### Columns

| Column | Type | Description |
|---|---|---|
| `id` | int | Unique sample identifier |
| `text` | string | The raw text input |
| `platform` | string | Source platform: `twitter`, `support_ticket`, `review`, `chat` |
| `topic` | string | General topic: `customer_service`, `product_feedback`, `work`, `personal`, `tech`, `finance`, `health`, `social` |
| `time_of_day` | string | `morning`, `afternoon`, `evening`, `night` |
| `text_length` | int | Character count of the text |
| `has_emoji` | bool | Whether the text contains emoji |
| `word_count` | int | Word count of the text |
| `contains_punctuation_emphasis` | bool | Whether text contains `!`, `?`, or `...` |
| `emotion` | string | **Target label** — train set only |

### Class Distribution
The dataset is **perfectly balanced** — 1,500 samples per emotion class in the training set, 375 per class in the test set.

---

## Evaluation

Submissions are evaluated on **Weighted F1 Score** across all 8 emotion classes.

```
F1 = 2 × (Precision × Recall) / (Precision + Recall)
```

Weighted F1 accounts for class balance by weighting each class proportionally to its support. A random baseline scores approximately **0.125**. A strong submission is expected to exceed **0.70**.

---

## Download

```bash
# Clone the full repository
git clone https://github.com/kryonara/emolens-dataset.git
```

Or download individual files directly:

- [`train.csv`](https://github.com/kryonara/emolens-dataset/raw/main/train.csv)
- [`test.csv`](https://github.com/kryonara/emolens-dataset/raw/main/test.csv)
- [`sample_submission.csv`](https://github.com/kryonara/emolens-dataset/raw/main/sample_submission.csv)

---

## Submission

Email your submission to **kryonara@gmail.com** with the subject line:

```
EmoLens Submission — [Your Name or Team Name]
```

Your submission file must be a CSV with exactly two columns:

```csv
id,emotion
1,frustration
2,joy
3,sarcasm
...
```

**Rules:**
- Maximum **5 submissions per participant or team per day**
- Maximum team size of **4**
- Pre-trained language models (BERT, RoBERTa, etc.) are permitted
- External data is **not permitted**
- All submitted code must be reproducible upon request

---

## Timeline

| Date | Milestone |
|---|---|
| Challenge Opens | Submissions accepted |
| Day 14 | Midpoint leaderboard update posted |
| Day 28 | Challenge closes — no more submissions |
| Day 30 | Winners announced on Instagram @kryonara |

---

## Getting Started

Here is a simple baseline to get you going:

```python
import pandas as pd
from sklearn.feature_extraction.text import TfidfVectorizer
from sklearn.linear_model import LogisticRegression
from sklearn.metrics import f1_score

# Load data
train = pd.read_csv('train.csv')
test = pd.read_csv('test.csv')

# Simple TF-IDF baseline
vectorizer = TfidfVectorizer(max_features=10000, ngram_range=(1,2))
X_train = vectorizer.fit_transform(train['text'])
X_test = vectorizer.transform(test['text'])

# Train
model = LogisticRegression(max_iter=1000)
model.fit(X_train, train['emotion'])

# Predict
predictions = model.predict(X_test)

# Build submission
submission = pd.DataFrame({
    'id': test['id'],
    'emotion': predictions
})
submission.to_csv('my_submission.csv', index=False)
print("Submission ready.")
```

> This baseline scores approximately **0.42 F1** — beat it.

---

## Tips

- The `platform` and `time_of_day` columns contain useful contextual signal — do not ignore them.
- Sarcasm and frustration are the hardest classes to distinguish. Context matters.
- Fine-tuning a pre-trained transformer (RoBERTa, DeBERTa) will outperform TF-IDF significantly.
- Ensemble methods combining text features with metadata tend to perform well.

---

## Citation

If you use this dataset in your work, please cite:

```
@dataset{kryonara2025emolens,
  title     = {EmoLens: Nuanced Emotion Detection Dataset},
  author    = {Kryonara AI Lab},
  year      = {2025},
  publisher = {GitHub},
  url       = {https://github.com/kryonara/emolens-dataset}
}
```

---

## License

This dataset is released under the [Creative Commons Attribution-NonCommercial 4.0 International License](https://creativecommons.org/licenses/by-nc/4.0/). Free for research and educational use. Not for commercial use without permission.

---

## About Kryonara AI Lab

Kryonara is an independent AI product lab building intelligent systems at the intersection of language, data, and human behavior. EmoLens is our first open research challenge — with more to come.

- 🌐 [kryonara.ai](https://kryonara.ai)
- 📸 [@kryonara](https://instagram.com/kryonara)
- 📧 kryonara@gmail.com

---

<div align="center">
  <sub>Built with purpose by Kryonara AI Lab · Challenge #001 · 2026</sub>
</div>
 
