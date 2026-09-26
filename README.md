
*The Power BI `.pbix` source file is available on request — it exceeds GitHub's direct upload size limit.*

---

## ⚠️ Limitations

- This dataset is from 2013 and one specific region — real-world fraud patterns evolve constantly
- The anonymized features (V1–V28) have unknown real-world meaning, by design, for privacy
- The Wide rule, as-is, is too noisy for automatic deployment
- These are **proposed analytical triggers**, not a production-ready system — a real deployment would combine many more signals and require ongoing monitoring

---

## 🤖 Why No Machine Learning

Simple, explainable threshold rules are fast to compute, transparent, and easy for a non-technical fraud team to trust and adjust — which matters more for a real-time alert system than squeezing out marginal accuracy gains from a black-box model. Every finding in this project traces back to a specific, reproducible calculation.

---

**Author:** Shalu | Data Analyst Portfolio Project
