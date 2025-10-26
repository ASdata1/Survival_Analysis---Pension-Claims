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






IPCW weights are estimated using the **Kaplan–Meier estimator** for the censoring survival function \(\hat G(t)\):  
\[
w_i = \frac{1}{\hat G(t_i)} \quad \text{for events, and } w_i = 0 \text{ for censored records.}
\]  
Patients who experience events later in time receive larger weights, compensating for censored peers.

### 🧩 3. Model Evaluation  
Models such as **Cox Proportional Hazards**, **Weibull AFT**, **Logistic Regression**, and **Decision Trees** are trained on each censoring-adjusted dataset.  
Performance is evaluated using:  
- 🧠 **Discrimination:** Uno’s C-index  
- 📈 **Calibration:** Integrated Brier Score (IBS)  
- 🔁 **Reclassification:** Net Reclassification Improvement (NRI)

---

## 📊 Key Insights (Expected)  

- Naïve methods (Zero, Discard) underestimate long-term event probabilities.  
- IPCW reduces bias and improves discrimination.  
- Proper reweighting enhances calibration for late-event predictions.  

---

---

## 🧠 Theoretical Background  

- **Survival Function:** \(S(t)=P(T>t)\) – probability the event hasn’t occurred by *t*.  
- **Hazard Function:** \(h(t)=\frac{f(t)}{S(t)}\) – instantaneous event rate given survival to *t*.  
- **Weibull Model:** Flexible parametric model where shape *k > 1* indicates increasing hazard.  
- **Kaplan–Meier Estimator:** Non-parametric estimate of \(S(t)\) accounting for censored data.  
- **IPCW:** Adjusts the likelihood by weighting each observation inversely by its censoring probability.  

---

## 📈 Metrics  

| Metric | Interpretation | Goal |
|---------|----------------|------|
| **C-index (Uno’s)** | Probability the model correctly ranks two patients’ risks | ↑ Higher = better |
| **Integrated Brier Score (IBS)** | Time-averaged calibration error | ↓ Lower = better |
| **Net Reclassification Improvement (NRI)** | % correctly reclassified between models | ↑ Higher = better |

---

## 🔮 Future Extensions  

- Implement **time-dependent ML models** (e.g., Random Survival Forests, DeepSurv).  
- Extend IPCW to **stabilized or dynamic weights**.  
- Compare against **multiple imputation** for censored outcomes.  
- Validate using **real-world longitudinal datasets**.  

---

## 🧩 Key Takeaway  

This project provides a reproducible framework for exploring how **censoring mechanisms affect survival predictions**, demonstrating how statistical reweighting techniques like **IPCW** can correct bias and improve the performance of machine learning models applied to censored time-to-event data.






