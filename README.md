#  Text Sentiment & Category Labeling Dataset

A structured data labeling project focused on classifying user-generated text by **sentiment** and **topic category** — simulating real-world annotation tasks found on platforms like **Remotasks** and **Appen**.

---

##  Project Overview

| Property | Details |
|---|---|
| **Task Type** | Text Classification / Sentiment Analysis |
| **Data Source** | Amazon Product Reviews (public domain) |
| **Total Records Labeled** | 500 entries |
| **Labels Applied** | Sentiment (3-class) + Category (8-class) |
| **Tools Used** | Python, pandas, CSV |
| **Platform Simulated** | Remotasks / Appen |

---

##  Label Schema

### Sentiment Labels
| Label | Description |
|---|---|
| `positive` | Text expresses satisfaction, praise, or approval |
| `neutral` | Text is factual, mixed, or neither positive nor negative |
| `negative` | Text expresses dissatisfaction, complaint, or frustration |

### Category Labels
| Label | Description |
|---|---|
| `electronics` | Reviews about tech products, gadgets, devices |
| `home_kitchen` | Household items, appliances, cookware |
| `clothing` | Apparel, shoes, accessories |
| `books` | Physical or digital books, educational content |
| `sports` | Sports gear, outdoor equipment |
| `beauty` | Cosmetics, skincare, personal care |
| `food` | Edible products, supplements, beverages |
| `other` | Doesn't fit a specific category |

---

##  Project Structure

```
text-labeling-sentiment-dataset/
├── data/
│   ├── raw/
│   │   └── reviews_raw.csv          # Original unlabeled data
│   └── labeled/
│       └── reviews_labeled.csv      # Final labeled dataset
├── guidelines/
│   └── labeling_guidelines.md       # Annotation rules and edge cases
├── samples/
│   └── sample_50.csv                # First 50 rows for review
└── README.md
```

---

##  Labeling Guidelines Summary

To ensure **consistency and quality**, the following rules were applied during annotation:

1. **Sentiment is based on overall tone**, not individual words. A review saying *"This broke after 2 days, but customer service was great"* = `negative` (product experience takes priority).
2. **Sarcasm is labeled by literal meaning** unless context makes intent unambiguous.
3. **Neutral is used sparingly** — only when the text truly contains no emotional direction.
4. **Category is assigned by the product being reviewed**, not the tone of the text.
5. **Edge cases were flagged** with a `needs_review` column set to `true` for QA review.

---

##  Dataset Sample

| review_id | text | sentiment | category | confidence | needs_review |
|---|---|---|---|---|---|
| 001 | "Absolutely love this blender, works perfectly!" | positive | home_kitchen | high | false |
| 002 | "Arrived on time. Does what it says." | neutral | electronics | high | false |
| 003 | "Stopped working after a week. Very disappointed." | negative | electronics | high | false |
| 004 | "It's okay I guess, not what I expected." | neutral | clothing | medium | true |

---

##  Quality Assurance

- **Inter-annotator agreement** was simulated using a 10% re-labeling pass on random samples
- Entries with `confidence: low` were double-checked against the labeling guidelines
- Final dataset achieved a **label consistency rate of ~94%** on the re-labeled sample

---

##  How to Use

```python
import pandas as pd

df = pd.read_csv('data/labeled/reviews_labeled.csv')

# View label distribution
print(df['sentiment'].value_counts())
print(df['category'].value_counts())

# Filter flagged entries
flagged = df[df['needs_review'] == True]
```

---

## 🔗 Related Platforms

This project mirrors the annotation workflow used on:
- [Remotasks](https://www.remotasks.com) — Text classification tasks
- [Appen](https://appen.com) — Sentiment and intent labeling
- [Scale AI](https://scale.com) — NLP data labeling pipelines
