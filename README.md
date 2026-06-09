# Portofolio-Clinic-Analysis
A healthcare data analytics project that evaluates clinic performance through patient visit and revenue analysis. The project uncovers trends, monitors key KPIs, and presents actionable insights using an interactive Tableau dashboard to support data-driven decision-making in healthcare operations.

# 🏥 Clinic Revenue & Patient Visit Analysis

![Python](https://img.shields.io/badge/Python-3.10-blue?logo=python)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-green)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-orange)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Domain](https://img.shields.io/badge/Domain-Healthcare%20Finance-purple)

> **Author:** Umul Hasanah  
> **LinkedIn:** [linkedin.com/in/umul-hasanah](https://linkedin.com/in/umul-hasanah)  
> **Tools:** Python · Pandas · Matplotlib · Microsoft Excel  

---

## 📌 Project Overview

This project analyzes **12 months of operational and financial data** from a dental clinic to uncover revenue patterns, identify cost inefficiencies, and provide actionable recommendations for management decision-making.

This analysis is grounded in **real administrative experience** gained while serving as Administrative Staff Coordinator at Etama Dental Clinic, Batam (2021–2026), where responsibilities included daily revenue recording, petty cash management, insurance claim submission, and monthly patient visit reporting.

**Why this matters:** Many clinics track numbers daily but rarely analyze them systematically. This project demonstrates how data analytics can turn routine operational records into strategic business insights.

---

## ❓ Business Questions

1. Which months generate the highest and lowest revenue — and why?
2. Is the clinic's cost-to-revenue ratio within a healthy operational range?
3. What is the trend of patient visits throughout the year?
4. How effective is the monthly insurance claim submission process?

---

## 📁 Dataset

> Simulated dataset based on real operational patterns observed during 4+ years managing clinic administration in Batam, Indonesia.

| Column | Description |
|--------|-------------|
| `month` | Month of record (2023-01 to 2023-12) |
| `total_visits` | Total outpatient visits per month |
| `general_patients` | Patients without insurance |
| `insurance_patients` | Patients covered by insurance (BPJS etc.) |
| `daily_revenue_idr` | Total monthly revenue (IDR) |
| `petty_cash_used` | Operational petty cash expenditure |
| `supplies_cost` | Consumable goods procurement cost |
| `insurance_claims_submitted` | Total insurance claims submitted |
| `insurance_claims_paid` | Total claims approved & paid |

📄 [Download Dataset](data/clinic_data_simulated.csv)

---

## 🔍 Analysis Steps

```python
# Step 1 — Load & validate data
df = pd.read_csv('clinic_data_simulated.csv')
print(df.isnull().sum())  # check for missing values

# Step 2 — Calculate key metrics
df['revenue_million']  = df['daily_revenue_idr'] / 1_000_000
df['total_cost']       = df['petty_cash_used'] + df['supplies_cost']
df['cost_ratio_%']     = (df['total_cost'] / df['daily_revenue_idr']) * 100
df['claim_approval_%'] = (df['insurance_claims_paid'] / df['insurance_claims_submitted']) * 100

# Step 3 — Flag high-cost months
high_cost = df[df['cost_ratio_%'] > 20]

# Step 4 — Visualize & extract insights
```

📓 [View Full Notebook](notebooks/clinic_analysis.ipynb)

---

## 📊 Key Findings

### 1. Revenue Trend

![Revenue Trend](charts/revenue_trend.png)

> 💡 **Finding:** December recorded the highest monthly revenue **(IDR 58.1M)** driven by year-end demand, while February was the lowest **(IDR 31.5M)** — a **46% gap** between peak and low season. This pattern is consistent with typical healthcare service demand cycles.

---

### 2. Patient Visit Volume

![Patient Visits](charts/patient_visits.png)

> 💡 **Finding:** Insurance patients consistently make up approximately **40% of total monthly visits**, making insurance claim management a critical operational function. Total visits peaked in December **(1,020 visits)** and dropped significantly in February **(610 visits)**.

---

### 3. Cost-to-Revenue Ratio

![Cost Ratio](charts/cost_ratio.png)

> 💡 **Finding:** February was the **only month exceeding the 20% cost threshold**, with a ratio of **22.5%**. Despite being the lowest-revenue month, it recorded the highest supply procurement cost — indicating a misalignment between purchasing cycles and patient demand.

---

## 📈 Summary Statistics

| Metric | Value |
|--------|-------|
| Total Annual Revenue | IDR 521.3 Million |
| Average Monthly Revenue | IDR 43.4 Million |
| Peak Revenue Month | December (IDR 58.1M) |
| Lowest Revenue Month | February (IDR 31.5M) |
| Average Cost-to-Revenue Ratio | ~15.8% |
| Average Insurance Claim Approval Rate | ~97.1% |
| Total Patient Visits (2023) | 10,120 visits |

---

## 💡 Business Recommendations

| # | Problem Identified | Recommendation |
|---|-------------------|----------------|
| 1 | February revenue 46% below peak | Launch targeted patient acquisition campaigns via WhatsApp & Instagram in **January** to stimulate February bookings |
| 2 | February cost ratio exceeded 20% | **Shift bulk supply procurement to March** to avoid cost spikes in the lowest-revenue month |
| 3 | ~40% of visits are insurance patients | **Standardize monthly SOP checklist** for insurance documentation to maintain 97%+ claim approval rate |
| 4 | Large revenue gap between peak & low season | Consider introducing **loyalty program or periodic promo packages** to smooth out seasonal fluctuations |

---

## 🗂️ Repository Structure

```
clinic-revenue-analysis/
│
├── 📁 data/
│   └── clinic_data_simulated.csv      # Dataset (12 months, 2023)
│
├── 📁 charts/
│   ├── revenue_trend.png              # Monthly revenue line chart
│   ├── patient_visits.png             # Stacked bar - patient types
│   └── cost_ratio.png                 # Cost ratio bar chart
│
├── 📁 notebooks/
│   └── clinic_analysis.ipynb          # Full analysis notebook
│
└── README.md
```

---

## ▶️ How to Run

**Option 1 — Google Colab (Recommended, no installation needed)**

1. Open [colab.research.google.com](https://colab.research.google.com)
2. Upload `clinic_analysis.ipynb`
3. Upload `clinic_data_simulated.csv` to the Colab file sidebar
4. Click **Runtime → Run All**

**Option 2 — Local**

```bash
git clone https://github.com/umul-hasanah/clinic-revenue-analysis
cd clinic-revenue-analysis
pip install pandas matplotlib
jupyter notebook notebooks/clinic_analysis.ipynb
```

---

## 👩‍💼 About the Author

**Umul Hasanah, S.M.**  
Bachelor of Management — Financial Management Concentration  
Universitas Riau Kepulauan (GPA 3.75 / 4.00, Cum Laude)

4+ years of experience as Administrative Staff Coordinator at a dental clinic in Batam, with hands-on expertise in financial recording, budgeting, insurance claims, and operational reporting. Certified in Full Stack Data Analytics (RevoU, 2024).

🔗 [LinkedIn](https://linkedin.com/in/umul-hasanah) · 💻 [GitHub](https://github.com/umul-hasanah) · ✉️ umulhasanah30@gmail.com

---

*Dataset is simulated based on real operational experience. All figures are approximate and anonymized for privacy.*

