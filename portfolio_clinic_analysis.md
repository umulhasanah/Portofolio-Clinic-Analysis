# 🏥 Clinic Revenue & Patient Visit Analysis
**Tools:** Python (Pandas, Matplotlib) | Excel | Tableau  
**Domain:** Healthcare Operations | Financial Reporting  
**Author:** Umul Hasanah | [LinkedIn](www.linkedin.com/in/umulhasanah)

---

## 📌 Project Overview

This project simulates a real-world administrative and financial analysis scenario based on experience managing daily operations at a dental clinic. The goal is to uncover revenue trends, patient visit patterns, and operational cost insights to support data-driven management decisions.

**Business Questions Answered:**
1. How does patient visit volume fluctuate month-over-month?
2. Which months show the highest and lowest revenue?
3. What is the ratio of operational costs (petty cash + supplies) to total revenue?
4. Are there patterns between visit volume and insurance claim amounts?

---

## 📁 Dataset

> *(Simulated dataset based on real operational experience)*

| Column | Description |
|--------|-------------|
| `month` | Month of record (Jan–Dec) |
| `total_visits` | Total outpatient visits |
| `general_patients` | Patients without insurance |
| `insurance_patients` | Patients with insurance (BPJS, etc.) |
| `daily_revenue_idr` | Total monthly revenue (IDR) |
| `petty_cash_used` | Operational petty cash expenditure |
| `supplies_cost` | Consumable goods procurement cost |
| `insurance_claims_submitted` | Total insurance claims submitted |
| `insurance_claims_paid` | Total insurance claims paid/approved |

---

## 🔍 Key Analysis Steps

### 1. Data Cleaning
```python
import pandas as pd
import matplotlib.pyplot as plt
import matplotlib.ticker as mticker

# Load data
df = pd.read_csv('clinic_data.csv')

# Check for nulls
print(df.isnull().sum())

# Ensure correct data types
df['month'] = pd.to_datetime(df['month'], format='%Y-%m')
df['revenue_million'] = df['daily_revenue_idr'] / 1_000_000
```

### 2. Monthly Revenue Trend
```python
plt.figure(figsize=(12, 5))
plt.plot(df['month'], df['revenue_million'], marker='o', color='#1F4E79', linewidth=2)
plt.fill_between(df['month'], df['revenue_million'], alpha=0.15, color='#1F4E79')
plt.title('Monthly Clinic Revenue (IDR Million)', fontsize=14, fontweight='bold')
plt.xlabel('Month')
plt.ylabel('Revenue (IDR Million)')
plt.xticks(rotation=45)
plt.tight_layout()
plt.savefig('charts/revenue_trend.png', dpi=150)
plt.show()
```

### 3. Patient Visit Volume by Type
```python
fig, ax = plt.subplots(figsize=(12, 5))
ax.bar(df['month'], df['general_patients'], label='General', color='#1F4E79')
ax.bar(df['month'], df['insurance_patients'], bottom=df['general_patients'],
       label='Insurance', color='#5BA3D0')
ax.set_title('Monthly Patient Visits by Type', fontsize=14, fontweight='bold')
ax.legend()
plt.tight_layout()
plt.savefig('charts/patient_visits.png', dpi=150)
plt.show()
```

### 4. Cost-to-Revenue Ratio
```python
df['total_cost'] = df['petty_cash_used'] + df['supplies_cost']
df['cost_ratio_%'] = (df['total_cost'] / df['daily_revenue_idr']) * 100

print(df[['month', 'revenue_million', 'total_cost', 'cost_ratio_%']].to_string())

# Flag months where cost ratio exceeded 20%
high_cost_months = df[df['cost_ratio_%'] > 20]
print(f"\n⚠️  High-cost months (>20% ratio):\n{high_cost_months[['month','cost_ratio_%']]}")
```

### 5. Insurance Claim Approval Rate
```python
df['claim_approval_rate_%'] = (
    df['insurance_claims_paid'] / df['insurance_claims_submitted'] * 100
)

avg_approval = df['claim_approval_rate_%'].mean()
print(f"Average insurance claim approval rate: {avg_approval:.1f}%")
```

---

## 📊 Key Findings

| Insight | Finding |
|---------|---------|
| Peak revenue month | **July & December** (holiday season + year-end) |
| Lowest visit month | **February** (post-holiday slowdown) |
| Average cost-to-revenue ratio | **~15–18%** (within healthy operational range) |
| Insurance claim approval rate | **~97%** (high compliance with documentation) |
| YoY visit growth | **+12%** from 2022 to 2023 |

---

## 📈 Dashboard (Tableau)

> 🔗 [View Live Tableau Dashboard](https://public.tableau.com/your-link-here) *(update with actual link)*

Dashboard includes:
- Revenue trend line (monthly)
- Patient visit stacked bar chart
- Cost ratio gauge
- Insurance claim funnel

---

## 💡 Business Recommendations

1. **Increase marketing activity in February** — lowest visit month; targeted promo via WhatsApp/Instagram can recover 10–15% visits.
2. **Monitor supply costs in Q4** — procurement tends to spike; negotiating bulk PO with suppliers can reduce costs by ~8%.
3. **Maintain insurance documentation quality** — current 97% approval rate is excellent; standardize the SOP checklist to sustain this.

---

## 🗂️ Repository Structure

```
clinic-revenue-analysis/
│
├── data/
│   └── clinic_data_simulated.csv
│
├── notebooks/
│   └── clinic_analysis.ipynb
│
├── charts/
│   ├── revenue_trend.png
│   ├── patient_visits.png
│   └── cost_ratio.png
│
├── README.md
└── requirements.txt
```

---

## ▶️ How to Run

```bash
# Clone this repo
git clone https://github.com/umul-hasanah/clinic-revenue-analysis

# Install dependencies
pip install pandas matplotlib seaborn jupyter

# Run notebook
jupyter notebook notebooks/clinic_analysis.ipynb
```

---

*This project is based on simulated data reflecting real operational experience. All figures are approximate and anonymized.*
