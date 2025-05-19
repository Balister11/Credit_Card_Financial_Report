
# # 💳 Credit Card Financial Dashboard

This project is a comprehensive end-to-end data analysis and dashboard solution for credit card operations. It integrates customer and transaction data from PostgreSQL and provides real-time insights using Power BI.

---

## 📌 Project Objective

To develop an interactive **Credit Card Weekly Dashboard** that provides real-time insights into performance metrics such as revenue, customer growth, transaction trends, and credit utilization. The dashboard empowers stakeholders to make data-driven decisions regarding customer engagement, churn reduction, and business strategy.

---

## 🧩 Data Sources

- **customer.csv** — Demographic and account-level data of customers.
- **credit_card.csv** — Weekly transaction and financial data.
- Data imported and stored in **PostgreSQL**.
- Connected live to **Power BI** for real-time reporting.

---

## 🔄 Data Flow Process


# CSV Files → PostgreSQL (ETL & Queries) → Power BI (Visuals & DAX Measures)

Data Processing Steps:
Prepared and cleaned raw CSV files.

Created SQL tables and imported data into PostgreSQL.

Connected Power BI directly to PostgreSQL.

Created DAX measures and calculated columns for grouping.

Refreshed data by appending 185 new rows to test dashboard flexibility.

# 🧮 DAX Measures & Groupings
DAX
Copy
Edit
-- Age Grouping
AgeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[customer_age] < 30, "20-30",
    'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
    'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
    'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
    'public cust_detail'[customer_age] >= 60, "60+",
    "unknown"
)

-- Income Grouping
IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Medium",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)

-- Revenue Calculation
Revenue = 'public cc_detail'[annual_fees] + 
          'public cc_detail'[total_trans_amt] + 
          'public cc_detail'[interest_earned]

-- Weekly Revenue Comparison
Current_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(ALL('public cc_detail'), 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2]))
)

Previous_week_Revenue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(ALL('public cc_detail'), 'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1)
)``` text

# 📊 Key KPIs on Dashboard
KPI	 Description
Total Revenue : Aggregated from annual fees, interest, and transactions

Customer Count : Total active customers

Total Transactions : Weekly and YTD transaction volume

Revenue YoY / WoW : Weekly and yearly revenue changes

Delinquency Rate : % of customers with late payments

Activation Rate : Customers actively using credit cards

Top Performing States : TX, NY, and CA contribute 68% of revenue

Card Category Contribution	: Blue & Silver cards account for 93% of usage

Gender-Based Revenue Split	Males: 31M

# 📈 Business Insights (Week 53)
📈 Revenue increased by 28.8% WoW.

💳 Total transaction amount and count saw a notable rise.

👥 Customer count also increased (details available in dashboard).

🧾 YTD Revenue: $57M.

🔁 Total Interest Earned: $8M.

💵 Transaction Volume: $46M.

👨‍👩‍👧‍👦 Blue & Silver Cards: 93% of overall transactions.

📍 Top States: TX, NY, CA → 68% of total revenue.

✅ Activation Rate: 57.5%, 🚫 Delinquency Rate: 6.06%.