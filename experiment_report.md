# Experiment Report: Data Quality Impact on AI Agent

**Student ID:** 2A202600481  
**Name:** Nguyen Manh Quyen  
**Date:** 2026-04-15  

---

## 1. Experiment Results

Run `agent_simulation.py` with two datasets and record the results:

| Scenario | Agent Response | Accuracy (1-10) | Notes |
|----------|----------------|-----------------|-------|
| **Clean Data** (`processed_data.csv`) | "Based on my data, the best choice is Laptop at $1200." | 9 | Accurate and useful response. Laptop is correctly identified as a top electronic product. |
| **Garbage Data** (`garbage_data.csv`) | "Based on my data, the best choice is Nuclear Reactor at $999999." | 1 | Completely incorrect. The agent suggests an extreme outlier that is clearly not a realistic product. |

---

## 2. Analysis

Why did the Agent fail when using Garbage Data?

The agent failed because the garbage dataset breaks the assumptions that the selection logic depends on. It contains an unrealistic outlier, duplicate identifiers, missing fields, and text values inside the price column. When the agent reads this noisy input, it does not understand context or common sense; it only reacts to the values that appear in the file. As a result, the extreme price of "Nuclear Reactor" dominates the result and hides the normal products that a real user would expect. This shows that prompt quality alone is not enough. Without cleaning, validation, and transformation, bad data can directly produce bad decisions.

More specifically, the outlier price pushes the agent toward the wrong recommendation, duplicate IDs reduce trust in the records, invalid price strings prevent reliable comparison, and null categories or IDs make the dataset incomplete. Clean data gives the model a fair input, while garbage data causes the model to amplify the errors already present in the table.

---

## 3. Conclusion

**Quality Data > Quality Prompt?** **Strongly Agree.**

No matter how detailed, logical, or well-crafted a prompt is, if the input data is garbage, the output will also be garbage. This experiment reinforces the fundamental principle: **"Garbage In, Garbage Out."**

A reliable AI Agent must be built on a foundation of clean data. Investing in ETL processes and data quality control is far more important than only optimizing prompts, because data is the primary source of knowledge that the Agent relies on to perform its tasks.
