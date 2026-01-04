# Hybrid Information Extraction

Extract **symptoms, diseases, and body parts** from clinical notes using a **two-stage hybrid pipeline**.

---

## Workflow

1. **Rule-based Matching (High Precision)**
   - Exact string matching against curated lists:
     - Symptoms: `["pain", "tooth pain", "sensitivity"]`
     - Diseases: `["caries", "dental caries", "decay"]`
     - Body parts: `["tooth", "molar", "molar 17"]`
   - Ensures **high-confidence extraction** of known entities.

2. **Embedding-based Semantic Matching (High Recall)**
   - Uses **Sentence-BERT embeddings** (`all-MiniLM-L6-v2`) to detect semantically similar terms.
   - Captures variations and synonyms not explicitly in the word lists.
   - Matches above a similarity threshold (e.g., 0.75) are added as `_sim`.

3. **Merge & Output**
   - Combine rule-based and embedding-based results.
   - Rule-based: high-precision.
   - Embedding-based: boosts recall.

---

## Evaluation

- **Metrics**: Precision, Recall, F1-score.
- **Example** (against human-labeled data):

```text
Precision: 0.78
Recall:    1.00
F1-score:  0.88
