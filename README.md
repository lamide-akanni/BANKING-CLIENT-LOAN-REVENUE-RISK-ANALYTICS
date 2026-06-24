
📌 **Data Analytics Pipeline: From raw client data to an Interactive Power BI KPI dashboard**

— Covering EDA, Relational Database Design, and Business IReporting.


📌 **Project Overview**

— Analyses of 3,000 banking client records across 25 financial attributes to uncover credit risk patterns, cross-sell opportunities, and dual-lending exposure. 
— The pipeline spans three tools — **Python for exploration,**  **MySQL for structured storage,** and **Power BI for interactive reporting** 
— producing a 4-page executive dashboard with actionable business insights.


📌 **Business Questions Answered**


— Which client segments carry the highest credit risk?
— Where are the strongest cross-sell opportunities (loans + deposits)?
— Which clients hold dual-lending products — and what is the exposure value?
— How does income band correlate with loan uptake and processing fee revenue?
— What is the average client engagement duration across product lines?


📌 **Tech Stack**

— Python (Pandas, Matplotlib, Seaborn, EDA, cleaning, visualisation, Storage)
— SQL & MySQL (Database Storage, Relational schema, multi-table joins)
— Power BI (Reporting, DAX, KPI dashboard)


**Repository Structure**

Banking-Analytics-Dashboard/
│
├── data/
│   └── banking_clients.csv          # Raw dataset (3,000 records, 25 attributes)
│
├── python/
│   └── eda_analysis.ipynb           # Exploratory data analysis notebook
│
├── sql/
│   ├── schema.sql                   # Database and table creation scripts
│   └── queries.sql                  # Analytical SQL queries used in the project
│
├── dashboard/
│   └── Banking_Dashboard.pbix       # Power BI dashboard file
│
├── screenshots/
│   ├── home.png
│   ├── loan_analysis.png
│   ├── deposit_analysis.png
│   └── qa_explorer.png
│
└── README.md


**Phase 1 — Exploratory Data Analysis (Python)**

Tools: Pandas · Matplotlib · Seaborn

Loaded and inspected 3,000 records across 25 financial attributes
Handled missing values, standardised data types, and removed duplicates
Conducted 7 regression analyses across income, loan amount, and engagement duration
Generated distribution plots, correlation heatmaps, and segment breakdowns
Identified key risk flags: dual-lending clients and high-exposure income bands


**Phase 2 — Relational Database (MySQL)**

Tools: MySQL Workbench · SQL

Designed a normalised relational schema across multiple linked tables
Loaded cleaned CSV data into MySQL using LOAD DATA INFILE
Wrote multi-table JOIN queries to answer core business questions
Created aggregated views for loan exposure, deposit balances, and client segmentation


**Phase 3 — Power BI Dashboard (4 Pages)**

Tools: Power BI Desktop · DAX

📌 **Key Findings**


£4.38B total loan portfolio across 3,000 clients and 5 regions
Dual-lending clients represent the highest-value and highest-risk segment
Mid-to-high income bands account for 67% of total loan exposure
Cross-sell opportunity identified in ~1 in 4 clients holding only one product type
Average client engagement duration: 42 months across the full portfolio


📌 **Skills Demonstrated**

Python Pandas Matplotlib Seaborn MySQL SQL JOINs Relational Schema Design Power BI DAX Data Cleaning EDA KPI Dashboard Design Business Intelligence Data Storytelling

---

## Connect:

OLAMIDE AKANNI

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/olamide-akanni-b240ab18a/)
[![Substack](https://img.shields.io/badge/Substack-FF6719?style=for-the-badge&logo=substack&logoColor=white)]([YOUR_SUBSTACK_URL](https://substack.com/@lamideakanni03))
[![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:akannilmd@gmail.com)

---

Feedback welcome!
