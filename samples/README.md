# Customer Feedback AI Comparison

This project evaluates two approaches for analyzing multilingual customer feedback: **AWS Comprehend** and **Bedrock (Claude)**.

## Summary

| Feature | AWS Comprehend | Bedrock (Claude) |
|---------|----------------|-----------------|
| Primary strength | Low-cost sentiment detection | High-quality insight extraction |
| Category detail | Broad, generic | Fine-grained, actionable |
| Multilingual accuracy | Good detection | Strong semantic understanding |
| Sentiment quality | Probability-based, often “mixed” | Context-aware, decisive |
| Summaries | Generic | Clear, business-ready |
| Demo & stakeholder value | Low–medium | High |
| Cost | Very low | Moderate |

## Example Feedback & Labels (with Pros & Cons)

### Sample 1
**Feedback:** *"Tuote oli hyvä mutta toimitus myöhässä. Asiakaspalvelu auttoi kuitenkin hyvin!"* (Finnish)

| Field | Comprehend | Claude |
|-------|------------|--------|
| Category | service | delivery |
| Subcategory | general_service | late_delivery |
| Sentiment | mixed | negative |
| Summary | Customer feedback with mixed sentiment about service | Product was good but delivery was late, however customer service helped well |
| Pros | ✅ Detects sentiment <br>✅ Identifies service-related topic | ✅ Fine-grained category <br>✅ Actionable subcategory <br>✅ Clear summary |
| Cons | ⚠️ Mixed sentiment is confusing <br>⚠️ Too generic | ⚠️ Slightly more expensive to run |

---

### Sample 2
**Feedback:** *"Terrible experience! Product broke immediately AND customer service was rude. Never shopping here again."* (English)

| Field | Comprehend | Claude |
|-------|------------|--------|
| Category | service | product |
| Subcategory | general_service | poor_quality |
| Sentiment | negative | negative |
| Summary | Customer feedback with negative sentiment about service | Product broke immediately |
| Pros | ✅ Correct negative sentiment | ✅ Correct negative sentiment <br>✅ Specific actionable category <br>✅ Clear summary |
| Cons | ⚠️ Category is too generic | ⚠️ Cost slightly higher |

---

### Sample 3
**Feedback:** *"Prekė gera, kaina normali, bet pristatymas užtruko 2 savaites. Per ilgai."* (Lithuanian)

| Field | Comprehend | Claude |
|-------|------------|--------|
| Category | general | delivery |
| Subcategory | general_general | late_delivery |
| Sentiment | mixed | negative |
| Summary | Customer feedback with mixed sentiment about general | Product delivery took 2 weeks, which is too long |
| Pros | ✅ Detects multilingual text | ✅ Accurate category & sentiment <br>✅ Actionable for ops |
| Cons | ⚠️ Generic category <br>⚠️ Mixed sentiment hard to interpret | ⚠️ Slightly higher cost |

---

> **Tip:** Use Comprehend for **cheap bulk tagging**, Claude for **high-value insight extraction**.


---

## Business Impact

- **AWS Comprehend**
  - Best for **large-scale, low-cost tagging**
  - Suitable for dashboards and trend tracking
  - Requires post-processing to be actionable

- **Bedrock (Claude)**
  - Best for **issue classification, routing, and insights**
  - Produces **human-readable summaries**
  - Ideal for demos, operations, and decision-making

## Cost Overview (Indicative)

| Service | Cost Profile |
|---------|-------------|
| AWS Comprehend | Fractions of a cent per feedback item |
| Bedrock (Claude) | Cents per hundreds of feedback items |

> **Note:** Claude is more expensive per item, but delivers significantly higher business value per record.

## Recommendation

- Use **Comprehend** for **cheap bulk sentiment signals**
- Use **Claude** where **accuracy, specificity, and insight quality matter**
- A **hybrid approach** offers the best cost-to-value ratio
