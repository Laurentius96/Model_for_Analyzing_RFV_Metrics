readme_content = '''<div align="center">
  <h1>📊 RFV Analysis - Customer Segmentation</h1>
  <p><i>Complete RFV (Recency, Frequency, Monetary) analysis pipeline with interactive dashboard and strategic insights</i></p>
</div>

<p align="center">
  <a href="#-overview">Overview</a> •
  <a href="#-objective">Objective</a> •
  <a href="#-technologies-used">Technologies</a> •
  <a href="#-project-structure">Project Structure</a> •
  <a href="#-data-pipeline">Data Pipeline</a> •
  <a href="#-segmentation-strategy">Segmentation</a> •
  <a href="#-results-and-insights">Results & Insights</a> •
  <a href="#-how-to-use">How to Use</a> •
  <a href="#-deliverables">Deliverables</a> •
  <a href="#-next-steps">Next Steps</a> •
  <a href="#-license">License</a>
</p>

---

## 🔍 Overview

This project implements a **complete RFV (Recency, Frequency, Monetary) analysis pipeline** for customer segmentation using the Online Retail dataset. It combines data cleaning, statistical analysis, strategic segmentation, and interactive visualization to deliver actionable business insights.

The project demonstrates essential **Data Science and Business Intelligence skills** including:
- Exploratory Data Analysis (EDA) with 541,909 transactions
- Advanced data cleaning and preprocessing
- RFV score calculation using percentile-based methodology
- Strategic customer segmentation into 7 actionable groups
- Interactive dashboard development with React and Recharts
- ROI-focused recommendations with £965K opportunity identification

**Key Achievement**: Identified that 20% of customers (Champions) generate 61% of revenue, confirming the Pareto Principle and enabling targeted marketing strategies with projected 7.7:1 ROI.

---

## 🎯 Objective

The main goal is to segment customers based on their purchasing behavior and provide strategic recommendations through a systematic approach that ensures:

1. **Data Quality**: Clean and validate 541,909 transactions from Dec/2010 to Nov/2011
2. **RFV Calculation**: Compute Recency, Frequency, and Monetary metrics for 4,233 customers
3. **Score Assignment**: Create 1-5 scores using percentile-based methodology
4. **Strategic Segmentation**: Classify customers into 7 actionable groups
5. **Business Insights**: Identify £965K in growth opportunities (+15.75% revenue increase)
6. **Interactive Visualization**: Deliver web-based dashboard and executive report

---

## 🛠️ Technologies Used

<div align="center">

| Technology | Purpose | Version |
|------------|---------|---------|
| ![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white) | Core programming language | 3.11+ |
| ![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white) | Data manipulation and analysis | 2.0+ |
| ![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white) | Numerical computing | 1.24+ |
| ![Matplotlib](https://img.shields.io/badge/Matplotlib-11557c?style=for-the-badge&logo=python&logoColor=white) | Data visualization | 3.7+ |
| ![Seaborn](https://img.shields.io/badge/Seaborn-3776AB?style=for-the-badge&logo=python&logoColor=white) | Statistical visualization | 0.12+ |
| ![React](https://img.shields.io/badge/React-61DAFB?style=for-the-badge&logo=react&logoColor=black) | Interactive dashboard | 18.0+ |
| ![Recharts](https://img.shields.io/badge/Recharts-22B5BF?style=for-the-badge&logo=chartdotjs&logoColor=white) | Chart components | 2.5+ |
| ![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=for-the-badge&logo=html5&logoColor=white) | Dashboard structure | - |
| ![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=for-the-badge&logo=css3&logoColor=white) | Dashboard styling | - |
| ![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white) | Interactive development | - |

</div>

---

## 📁 Project Structure

```
09_Model_for_Analyzing_RFV_Metrics/
│
├── 📓 notebooks/
│   ├── main_analysis.ipynb                    # Main analysis notebook
│   └── rfv_analysis/                          # Output directory
│       ├── 🏠 index.html                      # Portal page
│       ├── 📊 dashboard_interativo.html       # Interactive dashboard
│       ├── 📄 relatorio_executivo.html        # Executive report
│       ├── 📋 dashboard_data.json             # Structured data
│       ├── 📊 rfv_segmentation_complete.csv   # Complete segmentation
│       ├── 👑 champions_list.csv              # VIP customers
│       ├── ⚠️ at_risk_urgent.csv              # At-risk customers
│       ├── 💎 potential_loyalists_email.csv   # Potential loyalists
│       ├── 📈 segment_summary.csv             # Segment statistics
│       ├── 🧹 online_retail_cleaned.csv       # Cleaned dataset
│       ├── 🐍 rfv_pipeline.py                 # Reusable pipeline
│       └── 📝 README.md                       # Documentation
│
├── 📊 data/
│   └── Online Retail.xlsx                     # Original dataset
│
├── 📄 README.md                               # This file
└── 📜 LICENSE.md                              # License information
```

---

## 🔄 Data Pipeline

### 1️⃣ **Data Loading and Initial Exploration**

```python
# Load dataset
df = pd.read_excel('Online Retail.xlsx')

# Initial statistics
- Total transactions: 541,909
- Variables: 8 (4 numerical, 4 categorical)
- Period: Dec/2010 to Dec/2011
- Countries: 38
- Customers: 4,372 (with CustomerID)
```

### 2️⃣ **Data Cleaning and Preprocessing**

**Removed Records (176,582 - 32.59%)**:
- ❌ Missing CustomerID: 127,216 (23.47%)
- ❌ Cancellations (InvoiceNo starting with 'C'): 8,548 (1.58%)
- ❌ Outliers (IQR method): 15,253 (4.01%)
- ❌ Incomplete December 2011: 25,525 (4.71%)

**Final Clean Dataset**: 365,327 transactions

### 3️⃣ **RFV Calculation**

```python
# Reference date: 2011-12-01 (last complete month)

# Recency: Days since last purchase
recency = (reference_date - last_purchase_date).days

# Frequency: Number of unique purchases
frequency = df.groupby('CustomerID')['InvoiceNo'].nunique()

# Monetary: Total amount spent
monetary = df.groupby('CustomerID')['TotalAmount'].sum()
```

**RFV Statistics**:
- Recency: 0 to 364 days (mean: 91.3 days)
- Frequency: 1 to 194 purchases (mean: 2.8 purchases)
- Monetary: £1.25 to £114,558 (mean: £1,448)

### 4️⃣ **Score Assignment (1-5 Scale)**

Using **percentile-based methodology**:

| Score | Percentile Range | Interpretation |
|-------|------------------|----------------|
| 5 | Top 20% | Excellent |
| 4 | 60-80% | Very Good |
| 3 | 40-60% | Good |
| 2 | 20-40% | Fair |
| 1 | Bottom 20% | Poor |

**Note**: For Recency, lower is better (inverted scale)

### 5️⃣ **Customer Segmentation**

7 strategic segments based on RFV score combinations:

| Segment | Criteria | Customers | % Base | Revenue | % Revenue |
|---------|----------|-----------|--------|---------|-----------|
| 👑 Champions | R≥4, F≥4, M≥4 | 866 | 20.46% | £3.7M | 60.89% |
| 🌟 Loyal Customers | R≥3, F≥3, M≥3 | 606 | 14.32% | £908K | 14.83% |
| 💎 Potential Loyalists | R≥3, F≥1, M≥1 | 1,078 | 25.47% | £494K | 8.08% |
| ⚠️ At Risk | R≤2, F≥2, M≥2 | 454 | 10.73% | £575K | 9.39% |
| 😴 About to Sleep | R=2, F≤3, M≤3 | 553 | 13.06% | £196K | 3.20% |
| 🪦 Hibernating | R≤2, F≤2, M≤3 | 619 | 14.62% | £146K | 2.40% |
| ❓ Other | Other combinations | 57 | 1.35% | £74K | 1.22% |

---

## 🎯 Segmentation Strategy

### 👑 **Champions (VIP) - 866 customers**

**Profile**:
- Recency: 11.7 days (bought very recently)
- Frequency: 10.9 purchases (highly loyal)
- Monetary: £4,309 (high spenders)
- Revenue: £3.7M (60.89% of total)

**Strategy**: REWARD AND RETAIN
- VIP program with exclusive benefits
- Early access to new products
- 5-10% cashback on all purchases
- Priority customer service

**Investment**: £50K | **Expected ROI**: 10:1 (£500K)

---

### 🌟 **Loyal Customers - 606 customers**

**Profile**:
- Recency: 33.4 days
- Frequency: 4.4 purchases
- Monetary: £1,499
- Revenue: £908K (14.83% of total)

**Strategy**: UPSELL AND CROSS-SELL
- Loyalty program with points
- Personalized offers based on history
- Incentives to increase average ticket

**Investment**: £20K | **Expected ROI**: 6:1 (£120K)

---

### 💎 **Potential Loyalists - 1,078 customers**

**Profile**:
- Recency: 30.9 days (recent purchase)
- Frequency: 1.5 purchases (low repeat rate)
- Monetary: £459
- Revenue: £494K (8.08% of total)

**Strategy**: CONVERT TO LOYAL CUSTOMERS
- Email marketing sequence (5 emails in 30 days)
- Progressive coupons: 10% → 15% → 20%
- Facebook/Google Ads remarketing
- Incentive for 2nd purchase

**Investment**: £30K | **Expected ROI**: 8:1 (£240K)

💡 **BIGGEST OPPORTUNITY**: If we convert 30%, we generate +£1.4M!

---

### ⚠️ **At Risk - 454 customers**

**Profile**:
- Recency: 162.5 days (5+ months without purchase)
- Frequency: 3.7 purchases (good history)
- Monetary: £1,267 (valuable customers)
- Revenue at Risk: £575K (9.39% of total)

**Strategy**: URGENT REACTIVATION
- Personalized email: "We miss you!"
- 20% coupon valid for 15 days
- Phone call to top 50 customers
- Satisfaction survey

**Investment**: £15K | **Expected ROI**: 5:1 (£75K)

🚨 **IMMEDIATE ACTION REQUIRED!**

---

### 😴 **About to Sleep - 553 customers**

**Profile**:
- Recency: 120.4 days (4 months)
- Low value and frequency
- Revenue: £196K (3.20% of total)

**Strategy**: WIN-BACK CAMPAIGN
- Aggressive discounts (30% OFF)
- SMS marketing
- Cart abandonment reminders

**Investment**: £10K | **Expected ROI**: 3:1 (£30K)

---

### 🪦 **Hibernating - 619 customers**

**Profile**:
- Recency: 271.6 days (9 months)
- Frequency: 1 purchase only
- Revenue: £146K (2.40% of total)

**Strategy**: LAST ATTEMPT OR REMOVAL
- Generic email with high discount
- Passive remarketing
- Consider removing from active list

**Savings**: £5K/year in email costs

---

## 📊 Results and Insights

### 🔍 **Key Findings**

1. **Pareto Principle Confirmed**
   - 20% of customers (Champions) generate 61% of revenue
   - Extreme value concentration in few customers
   - **Action**: Protect Champions at all costs!

2. **Massive Opportunity**
   - 1,078 Potential Loyalists (25% of base)
   - Bought recently (30 days), but only 1.5x
   - If we convert 30% to Champions: +£1.4M in revenue!

3. **Red Alert**
   - 454 "At Risk" customers (£575K at risk)
   - Haven't purchased in 162 days, but have good history
   - Urgent reactivation campaign can recover 50%

4. **Retention Problem**
   - 36% of customers purchased ONLY ONCE
   - 1,537 customers with Frequency Score = 1
   - Focus on 2nd purchase strategies is ESSENTIAL

5. **Geographic Concentration**
   - UK represents 91% of transactions
   - Limited international expansion opportunity
   - Or: Total focus on UK market to maximize ROI

---

### 💰 **Financial Impact**

**Current Situation**:
- Revenue: £6,129,262
- Customers: 4,233
- Average Ticket: £333.41
- Average Frequency: 2.8 purchases

**Projection (12 months)**:
- Revenue: £7,094,262 (+£965K)
- Growth: +15.75%
- ROI: 7.7:1 (£125K invested)

**Action Plan**:

| Action | Segment | Investment | ROI | Additional Revenue |
|--------|---------|------------|-----|-------------------|
| VIP Program | Champions (866) | £50K | 10:1 | £500K |
| Email Marketing | Potential (1,078) | £30K | 8:1 | £240K |
| Reactivation | At Risk (454) | £15K | 5:1 | £75K |
| Loyalty Program | Loyal (606) | £20K | 6:1 | £120K |
| Win-back Campaign | About to Sleep (553) | £10K | 3:1 | £30K |
| **TOTAL** | **3,557 customers** | **£125K** | **7.7:1** | **£965K** |

---

## 🚀 How to Use

### **Prerequisites**

```bash
# Python 3.11+
pip install pandas numpy matplotlib seaborn openpyxl jupyter
```

### **1️⃣ Run Analysis**

```bash
# Open Jupyter Notebook
jupyter notebook notebooks/main_analysis.ipynb

# Or run pipeline directly
python rfv_analysis/rfv_pipeline.py
```

### **2️⃣ View Dashboards**

**Option A: Portal Page**
```bash
# Open in browser
rfv_analysis/index.html
```

**Option B: Direct Access**
- `dashboard_interativo.html` → Interactive dashboard
- `relatorio_executivo.html` → Executive report

### **3️⃣ Use Data in CRM**

1. Import `champions_list.csv` into your CRM
2. Set up campaign with `at_risk_urgent.csv`
3. Email marketing with `potential_loyalists_email.csv`

### **4️⃣ Monthly Updates**

```bash
# Update analysis with new data
python rfv_pipeline.py --input new_data.csv --output rfv_results/
```

---

## 📦 Deliverables

### **Interactive Dashboards**
- ✅ `index.html` - Portal page with navigation
- ✅ `dashboard_interativo.html` - Interactive dashboard with Recharts
- ✅ `relatorio_executivo.html` - Executive report (print-ready)

### **Data Files**
- ✅ `rfv_segmentation_complete.csv` - 4,233 customers with scores
- ✅ `champions_list.csv` - 866 VIP customers
- ✅ `at_risk_urgent.csv` - 454 at-risk customers
- ✅ `potential_loyalists_email.csv` - 1,078 potential customers
- ✅ `segment_summary.csv` - Statistical summary by segment
- ✅ `online_retail_cleaned.csv` - 365,327 clean transactions
- ✅ `dashboard_data.json` - Structured data for integration

### **Code**
- ✅ `main_analysis.ipynb` - Complete analysis notebook
- ✅ `rfv_pipeline.py` - Reusable pipeline for monthly updates

### **Documentation**
- ✅ `README.md` - Complete project documentation
- ✅ Technical justifications for all decisions
- ✅ DNC Challenge compliance checklist

---

## ✅ DNC Challenge Compliance

All requirements were successfully met:

- ✅ **Exploratory Data Analysis (EDA)**
  - Analysis of 541,909 initial transactions
  - Identification of 8 variables (4 numerical, 4 categorical)
  - Detection and treatment of missing values (23.47% without CustomerID)
  - Identification of duplicates and outliers
  - Complete temporal analysis (12 months)
  - Geographic analysis (38 countries)

- ✅ **Data Cleaning and Preprocessing**
  - Removal of 176,582 invalid records (32.59%)
  - Treatment of missing values (CustomerID)
  - Removal of cancellations (8,548 records)
  - Outlier treatment using IQR method (percentiles 1-99%)
  - Creation of TotalAmount variable
  - Date parsing with validation
  - Final dataset: 365,327 valid transactions

- ✅ **RFV Calculation**
  - Recency: Days since last purchase (0-364 days)
  - Frequency: Number of unique purchases (1-194)
  - Monetary: Total amount spent (£1.25 - £114,558)
  - Average ticket calculation per customer
  - Aggregation by CustomerID

- ✅ **Score Creation (1-5 Scale)**
  - R_Score: Based on percentiles (lower = better)
  - F_Score: Based on percentiles (higher = better)
  - M_Score: Based on percentiles (higher = better)
  - Robust treatment of duplicate values
  - Combined RFV_Score (concatenation)
  - RFV_Total (sum of scores)

- ✅ **Strategic Segmentation**
  - 7 main segments identified
  - Segmentation logic based on RFV combinations
  - Statistical analysis by segment
  - Champions identification (866 VIP customers)
  - At-risk customer mapping

- ✅ **Visualizations**
  - 12+ professional charts created
  - RFV score distribution
  - 3D segmentation matrix
  - Recency vs Frequency heatmap
  - Pareto analysis (80/20)
  - Distribution boxplots
  - Temporal evolution charts

- ✅ **Insights and Recommendations**
  - Pareto Law identification (20/80)
  - Quantified growth opportunities (£965K)
  - Specific strategies by segment
  - Action prioritization (High/Medium/Low)
  - ROI projection by campaign
  - Implementation roadmap (12 months)

- ✅ **Data Export and Documentation**
  - 10 files exported
  - Commented and reusable code
  - Complete executive report
  - Interactive dashboard
  - Professional documentation

---

## 🎯 Next Steps

### **Short Term (30 days)**
1. Present analysis to stakeholders
2. Approve £125K budget for campaigns
3. Implement VIP program for Champions (866 customers)
4. Launch urgent reactivation campaign for At Risk (454 customers)
5. Start email marketing for Potential Loyalists (1,078 customers)

### **Medium Term (60 days)**
4. Implement loyalty program for Loyal Customers (606 customers)
5. Launch win-back campaign for About to Sleep (553 customers)
6. Conduct satisfaction survey with "Other" segment (57 customers)
7. Create real-time monitoring dashboard

### **Long Term (90+ days)**
8. Last attempt with Hibernating customers (619 customers)
9. Remove inactive customers (1+ year) from active list
10. Redo RFV analysis monthly for tracking
11. Implement Machine Learning for churn prediction
12. Develop CLV (Customer Lifetime Value) model
13. Market Basket Analysis (product association)
14. Advanced behavioral clustering

---

## 📜 License

This project is licensed under the **Creative Commons Attribution-NonCommercial-NoDerivatives 4.0 International License (CC BY-NC-ND 4.0)**.

### You are free to:
- **Share** — copy and redistribute the material in any medium or format

### Under the following terms:
- **Attribution** — You must give appropriate credit
- **NonCommercial** — You may not use the material for commercial purposes
- **NoDerivatives** — If you remix, transform, or build upon the material, you may not distribute the modified material

For more details, see the [LICENSE.md](LICENSE.md) file.

---

<div align="center">
  <p><strong>📊 RFV Analysis Project</strong></p>
  <p>DNC Challenge | 4,233 customers analyzed | £6.1M in revenue</p>
  <p><i>All challenge requirements successfully completed ✅</i></p>
  <br>
  <p>
    <a href="https://github.com/yourusername">GitHub</a> •
    <a href="https://linkedin.com/in/yourprofile">LinkedIn</a> •
    <a href="mailto:your.email@example.com">Contact</a>
  </p>
</div>
'''

readme_path = os.path.join(output_dir, 'README.md')
with open(readme_path, 'w', encoding='utf-8') as f:
    f.write(readme_content)

print(f"✅ README.md profissional criado: {readme_path}")
print("   • Seguindo o padrão dos seus projetos")
print("   • Com badges, tabelas e formatação completa")
print("   • Seções detalhadas e organizadas")
print("   • Links de navegação rápida")

print("\n" + "="*80)
print("🎉 README.md CRIADO COM SUCESSO!")
print("="*80)
```