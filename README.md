# fortis-resort# 🏨 Fortis Downtown Resort — Operational & Revenue Performance Analytics

![SQL](https://shields.io)
![Python](https://shields.io)
![Power BI](https://shields.io)
![Status](https://shields.io)

## 📌 Project Overview
This end-to-end data analytics case study evaluates the operational and commercial performance of **Fortis Downtown Resort** across **September and October 2026**. By analyzing 9,440 validated guest transactions across 5 core service units, this project uncovers key revenue drivers, customer demographic trends, room occupancy patterns, and retention bottlenecks to guide peak-season (winter) pricing and targeted marketing strategies.

---

## 🎯 Business Objectives
1. **Revenue & Growth Tracking:** Evaluate Month-over-Month (MoM) financial performance and identify high-performing service categories.
2. **Customer Segmentation:** Analyze guest demographics, payment preferences, and segment revenue shares (Corporate vs. Leisure).
3. **Retention & Churn Reduction:** Identify repeat booking patterns and formulate actionable strategies to convert one-time visitors into loyal guests.
4. **Demand Forecasting:** Project November 2026 occupancy and revenue targets ahead of the winter corporate retreat season.

---

## 🛠️ Tech Stack & Methodology
* **SQL:** Data extraction, schema validation, deduplication, null handling, and creation of aggregated production views.
* **Python (`Pandas`, `Matplotlib`, `Seaborn`):** Statistical trend modeling, category-wise revenue breakdown, and exploratory data analysis (EDA).
* **Power BI:** Executive dashboarding, KPI tracking, and interactive visual storytelling.

---

## 🧹 Data Preparation & SQL Pipeline
Raw operational logs from POS systems, room bookings, and spa records contained **9,812 rows**. After removing **372 records (3.8%)** consisting of duplicate check-ins, null revenue entries, and cancelled test bookings, **9,440 clean records** were loaded into the production view:

```sql
CREATE VIEW vw_fortis_sep_oct AS
SELECT 
    booking_month,
    service_category,
    payment_method,
    COUNT(DISTINCT guest_id) AS total_guests,
    SUM(net_revenue_bdt) AS total_revenue,
    AVG(stay_duration) AS avg_nights,
    ROUND(SUM(net_revenue_bdt) / COUNT(DISTINCT guest_id), 2) AS arpu
FROM fortis_resort_bookings
WHERE booking_month IN ('Sep', 'Oct')
  AND status = 'Completed'
  AND net_revenue_bdt IS NOT NULL
GROUP BY 1, 2, 3;
```

---

## 📊 Key Performance Metrics (Sep – Oct 2026)

| KPI / Metric | September 2026 | October 2026 | Overall / MoM Change |
| :--- | :--- | :--- | :--- |
| **Total Revenue** | BDT 12.68M | BDT 15.77M | **BDT 28.45M (+24.2% MoM)** |
| **Total Guest Visits** | 4,210 | 5,230 | **9,440 Guests (+24.2% MoM)** |
| **Room Occupancy Rate** | 71.2% | 85.6% | **78.4% Average** |
| **Average Spend / Guest** | — | — | **BDT 3,014** |
| **Repeat Guest Retention** | — | — | **68.5% Repeat** (31.5% Churn Risk) |

---

## 🔍 Key Analytical Insights
* **Primary Revenue Drivers:** **Rooms & Suites** generated **46.4% (BDT 13.20M)** of total revenue, followed by **Dining & Buffet** at **22.5% (BDT 6.40M)**.
* **Segment & Age Dominance:** **Corporate & Family** guests contributed **58%** of total revenue, while **Leisure & Couples** accounted for **42%**. Guests aged **26–45** represent the highest-spending demographic.
* **Corporate Loyalty:** The **Corporate Banquet Hall** achieved the highest repeat utilization rate at **82.5%**, supported by **142 active VIP/Corporate accounts** (led by `ACC-104` with BDT 840K across 14 events).
* **Digital Payment Adoption:** Cashless transactions dominated bookings, led by **Credit Cards (3,120 transactions)** and **Mobile Banking (2,480 transactions)**.
* **Retention Bottleneck:** While overall retention is strong at 68.5%, **Day-Out Picnic Packages** showed the lowest repeat rate (**54.0%**), and **2,974 visitors** were one-time guests.

---

## 📈 November 2026 Forecasted Outlook
* **Projected Revenue:** **BDT 17.85M** (+13.2% projected growth over October).
* **Expected Occupancy:** **89.0%**, driven by early winter corporate retreats and banquet bookings.

---

## 💡 Actionable Business Recommendations
1. **Targeted Weekend Win-Back Campaign:** Launch automated email/SMS retargeting offering a **15% return voucher** specifically for the **420 first-time weekend guests** from October to reduce the 31.5% churn rate.
2. **Day-Out Package Bundling:** Increase the 54.0% repeat rate of Day-Out Picnic guests by introducing bundled cross-sell packages combining day tours with **Spa & Herbal Therapy** and **All-Day Buffet Dining**.
3. **Corporate Early-Bird Retainers:** Offer priority booking incentives to top corporate accounts (`ACC-104`, `ACC-219`, `ACC-118`) for Q4 retreats to lock in the **89.0% November occupancy target**.

---

## 💻 Python Visualization Snippet
```python
import pandas as pd
import matplotlib.pyplot as plt

# Load cleaned dataset
df = pd.read_csv('fortis_resort_sep_oct.csv')

# Aggregate revenue by service category and month
summary = (
    df.groupby(['Category', 'Month'])['Revenue_BDT']
    .sum()
    .unstack()
    .sort_values(by='October', ascending=False)
)

# Plot comparative bar chart
summary.plot(kind='bar', figsize=(10, 6), color=['#3B82F6', '#F59E0B'])
plt.title('Fortis Resort: Revenue by Category (Sep vs Oct)')
plt.ylabel('Total Revenue (BDT Millions)')
plt.xticks(rotation=12)
plt.tight_layout()
plt.show()
```

---

## 📂 Repository Structure
```text
├── data/
│   └── fortis_resort_sep_oct.csv        # Cleaned dataset (9,440 records)
├── sql/
│   └── data_cleaning_and_views.sql      # SQL queries & production view script
├── notebooks/
│   └── fortis_sep_oct_analysis.py       # Python EDA & visualization script
├── dashboard/
│   └── Fortis_Resort_Dashboard.pbix     # Power BI interactive dashboard file
└── README.md                            # Project documentation
```

---

## 📬 Contact & Links
* **Author:** [md zulfiqar uddin]
* **LinkedIn:** [Your LinkedIn Profile Link]
* **Portfolio / Power BI Live Demo:** [Your Dashboard Link]
