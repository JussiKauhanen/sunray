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
