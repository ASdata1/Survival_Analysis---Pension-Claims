# 🧮 Pension Claims Survival Analysis: Censoring Methods & Machine Learning Comparison  

## 📘 Overview  

This project investigates how different **censoring-handling techniques** influence the accuracy and bias of **machine learning models** trained on **time-to-event (survival) data**.  
Censoring occurs when an individual’s event outcome is unknown within the observation period — a common issue in domains like **pensions**, **healthcare**, and **finance**. Improperly managing censored data can lead to misleading conclusions and poor predictive performance.  

To address this, a **synthetic pension-claim dataset** was generated using a **Weibull distribution**, allowing control over both event rates and right-censoring proportions. The dataset simulates realistic characteristics where each individual’s time to claim a pension depends on:
- Age at entry  
- Income level  
- Health score  
- Pension contribution rate  

This controlled setup provides a known “ground truth” for benchmarking different censoring strategies and evaluating model performance.

---

## 🎯 Research Goals  

1. **Accurately synthesize time-to-event data** with controlled censoring patterns.  
2. **Quantify how censoring bias affects survival and ML model performance.**  
3. **Compare alternative censoring-handling methods:**
   - **Zero method:** keep censored samples with event = 0  
   - **Discard method:** remove censored samples entirely  
   - **Split method:** divide censored durations into sub-intervals  
   - **IPCW (Inverse Probability of Censoring Weighting):** reweight uncensored samples based on censoring probability  
4. **Evaluate models** using robust survival metrics:
   - **Discrimination:** Uno’s C-index  
   - **Calibration:** Integrated Brier Score (IBS)  
   - **Reclassification:** Net Reclassification Improvement (NRI)  

---

## ⚙️ Methodology  

### 🧩 1. Data Generation  
A synthetic dataset of 5 000 individuals was generated using a **Weibull Accelerated Failure Time (AFT)** model, ensuring an increasing hazard rate (shape parameter *k > 1*) to reflect the rising likelihood of pension claims over time.  
Right-censoring times were drawn from a uniform distribution to simulate incomplete observations.

### 🧩 2. Censoring Methods Preparation  
Each censoring method is implemented and saved separately in:  



