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

## 2. Analysis & Observations

### Why did the Agent fail when using Garbage Data?

When using garbage data, the Agent produces completely incorrect results because the input data contains several serious issues in both structure and content:

1. **Outliers:** The presence of "Nuclear Reactor" with an extremely high price ($999,999) misleads the Agent’s decision-making logic. The Agent simply scans for the largest numerical value without understanding that this is an unrealistic entity in a normal shopping context.

2. **Duplicate IDs:** Having multiple records with the same ID (e.g., id=1 appearing twice) creates confusion and reduces the consistency and uniqueness of the dataset.

3. **Wrong Data Types:** The "price" field contains text values ("ten dollars") instead of numeric values, preventing the Agent from performing accurate comparisons or calculations.

4. **Null Values:** Records with missing IDs or categories still pass through the system, reducing overall reliability.

All these factors demonstrate that without preprocessing and validation, the Agent blindly trusts corrupted data, leading to harmful or incorrect decisions.

---

## 3. Conclusion

**Quality Data > Quality Prompt?** **Strongly Agree.**

No matter how detailed, logical, or well-crafted a prompt is, if the input data is garbage, the output will also be garbage. This experiment reinforces the fundamental principle: **"Garbage In, Garbage Out."**

A reliable AI Agent must be built on a foundation of clean data. Investing in ETL processes and data quality control is far more important than only optimizing prompts, because data is the primary source of knowledge that the Agent relies on to perform its tasks.