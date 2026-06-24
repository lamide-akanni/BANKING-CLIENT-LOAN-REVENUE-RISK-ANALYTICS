
An analytics project — from raw client data to a live, interactive Power BI dashboard — covering exploratory analysis in Python, relational database design in MySQL, data modelling in Power BI, and live report hosting via Power BI Service.

Tools: Python · My(SQL) · Power BI · Canva
Dataset: 3,000 banking clients · 25 financial attributes


Project Overview

This project started with a single question: What does a banking client portfolio actually look like beneath the surface?

With 3,000 client records and 25 financial attributes to work with, the goal was to move through every stage of the analytics pipeline — from raw data sitting in a spreadsheet, all the way to a live, reporting and interactive dashboard that a business team could open and explore on their own. No shortcuts - No skipping steps.

The pipeline runs across three tools. Python handles the initial exploration — understanding the shape of the data, finding patterns, and generating visual evidence of how variables relate to each other. MySQL takes the cleaned data and gives it proper structure, turning a flat CSV file into a relational database that can be queried in multiple directions. Power BI then connects to that database, models the relationships between tables, and transforms everything into a four-page executive dashboard hosted live on Power BI Service.

The result is a complete picture of the client portfolio — credit risk exposure, deposit behaviour, cross-sell opportunities, and loan trends — all filterable, interactive, and ready for a real business audience.


Business Questions

The project was built to answer five core questions:


Which client segments carry the highest credit risk, and how does that risk distribute across regions and income bands?
Where are the strongest cross-sell opportunities — clients holding loans but no deposits, or the reverse?
Which clients carry dual-lending exposure, and what is the total value of that risk?
How does income band correlate with loan uptake, business lending, and processing fee revenue?
How long are clients typically engaged with the bank, and which segments show the longest relationships?



Repository Structure

Banking-Analytics-Dashboard/
│
├── data/
│   └── banking_clients.csv          # Raw dataset (3,000 records, 25 attributes)
│
├── python/
│   └── eda_analysis.ipynb           # Full exploratory data analysis notebook
│
├── sql/
│   ├── schema.sql                   # Database and table creation scripts
│   └── queries.sql                  # Analytical SQL queries — joins, aggregations, filters
│
├── dashboard/
│   └── Banking_Dashboard.pbix       # Power BI dashboard file
│
├── screenshots/
│   ├── 01_mysql_workbench_setup.png
│   ├── 02_python_eda_regression_plots.png
│   ├── 03_mysql_sql_queries.png
│   ├── 04_powerbi_data_model.png
│   ├── 05_canva_design.png
│   ├── 06_mysql_database_loaded.png
│   ├── 07_dashboard_qa_explorer.png
│   ├── 08_mysql_connect_database.png
│   ├── 09_dashboard_home.png
│   ├── 10_dashboard_loans.png
│   └── 11_dashboard_deposits.png
│
└── README.md


Phase 1 — Exploratory Data Analysis in Python

Tools: Python · Pandas · Matplotlib · Seaborn · Jupyter Notebook

Before any database was designed or any dashboard was built, the data needed to be understood. The exploratory analysis ran inside a Jupyter Notebook titled Risk Analytics in Banking and Finance, and it covered every dimension of the dataset systematically.

The first task was loading and inspecting the 3,000 client records. Missing values were identified and handled, data types were standardised, and duplicates were removed. Once the data was clean, the analysis moved into the patterns.

Seven regression analyses were run to examine the relationships between key financial variables. These included bank deposits against saving accounts, checking accounts against foreign currency holdings, estimated income against checking account balances, age against superannuation savings, and bank loans against credit card balances. Each regression was plotted as a scatter chart with a trend line overlaid, so the direction and strength of each relationship was immediately visible.

Show Image
Regression plots generated in Jupyter Notebook showing variable relationships across the client portfolio.

The outputs of this phase told a clear story before a single SQL query was written. High-income clients tended to hold larger loan balances but not proportionally larger deposits. Age showed little correlation with superannuation savings, which pointed to behavioural differences rather than age-driven accumulation. Business lending was positively correlated with total bank loans, suggesting that the same clients driving loan volume were also the biggest users of business credit facilities.

These findings shaped every decision made in the phases that followed.


Phase 2 — Building the Relational Database in MySQL

Tools: MySQL Workbench · SQL

Once the exploratory work was complete, the cleaned data needed a proper home. A flat CSV file is fine for exploration, but it is not a foundation you can build reliable queries on. The data was moved into MySQL and structured as a relational database.

Setting up the connection

The first step was opening MySQL Workbench and establishing a local connection. The connection was set up using Standard TCP/IP on localhost at port 3306, which is the default MySQL configuration for a local instance.

Show Image
MySQL Workbench open and connected to the local instance before the database schema was created.

Show Image
Configuring the database connection in MySQL Workbench using Standard TCP/IP.

Creating the schema and loading the data

A new schema called banking_case was created to hold all the project tables. The main client table, clients_banking, was defined with client_id as the primary key — a VARCHAR field that uniquely identifies each record. The remaining 24 columns were mapped to appropriate data types: numerical fields for financial values, text fields for categorical attributes like nationality and loyalty class, and date fields for time-based columns like join date.

The cleaned CSV was loaded directly into the table using LOAD DATA INFILE, which populated all 3,000 rows in a single operation. A quick SELECT * FROM clients_banking LIMIT 50 confirmed the data had loaded correctly and the field types were reading as expected.

Show Image
The banking_case schema with the clients_banking table showing all 3,000 rows successfully loaded and the field structure visible in the Field Types panel.

Writing the analytical queries

With the data in place, a series of SQL queries were written to answer the business questions directly from the database. These included multi-table joins to bring in lookup data from supporting tables — investment advisors, banking relationship types, and gender classifications — as well as aggregation queries to calculate totals and segment breakdowns.

One of the more specific queries checked for duplicate client IDs using GROUP BY client_id HAVING COUNT(*) > 1, which returned zero rows and confirmed the data integrity of the primary key across all 3,000 records.

Show Image
SQL queries running in MySQL Workbench, including joins and aggregations against the clients_banking table. The output panel shows successful execution logs.

The action output panel tracked every query execution, showing row counts, timing, and any errors. By the end of this phase, the database was clean, structured, and fully queryable — ready to be connected to Power BI.


Phase 3 — Connecting MySQL to Power BI

Tools: Power BI Desktop · MySQL Connector

The bridge between the database and the dashboard was built through Power BI's native MySQL connector. Inside Power BI Desktop, the data import process started by selecting MySQL Database as the source, then pointing it at the local instance on localhost:3306 and selecting the banking_case schema.

Power BI pulled in all the tables from the schema in a single connection — the main clients_banking fact table along with the supporting dimension tables for investment advisors, banking relationships, and gender classifications. Each table loaded as a separate query inside Power Query Editor, where the data types were reviewed and confirmed before the load completed.

The connection ran through the MySQL ODBC driver, which meant once the initial setup was done, refreshing the data in Power BI was as simple as clicking the Refresh button — the dashboard would pull the latest state of the database automatically.


Phase 4 — Data Modelling and Star Schema

Tools: Power BI Desktop — Model View

Once the tables were loaded, the relationships between them needed to be defined. This was done in Power BI's Model View, where the tables were arranged and connected to form a star schema.

The bankingx table — the main fact table — sat at the centre, holding the transactional and financial data for all 3,000 clients. The dimension tables radiated out from it: gender connected on GenderId, investment-advisors connected on IAId, and banking-realtionships connected on BRId. Each relationship was a one-to-many link, with the dimension table on the one side and the fact table on the many side, which is the correct structure for a star schema.

Show Image
The Power BI data model showing the star schema structure, with the main client fact table connected to dimension tables for gender, investment advisors, and banking relationships.

Getting this structure right before building any visuals was important. A correctly defined model means that when a user filters by gender or banking relationship type on the dashboard, that filter flows correctly through the relationships and affects every visual on the page — without any manual adjustments or workarounds.


Phase 5 — Dashboard Design with Canva

Tools: Canva

Before a single visual was placed in Power BI, the dashboard layout was designed first in Canva. This is a step that many analytics projects skip, and it shows. Without a design foundation, dashboards tend to end up as a collection of visuals placed wherever there was space — functional, but not professional.

The design work in Canva established the colour palette, the navigation bar layout, the positioning of KPI cards across the top of each page, and the dark background theme that would run consistently across all four dashboard pages. The navigation buttons — Home, Loans, Deposits, and Q&A — were designed as rounded pill shapes and positioned at the top centre of each page, giving the dashboard a clean, app-like feel.

Show Image
Early stage dashboard background being designed in Canva, establishing the dark theme and layout grid that was then imported into Power BI as the page background.

The finished background was exported as a PNG and imported into Power BI as the canvas background for each of the four report pages. All the Power BI visuals were then placed on top of this background, aligned to the design grid established in Canva.


Phase 6 — Building the 4-Page Interactive Dashboard

Tools: Power BI Desktop · DAX

With the data modelled and the design backgrounds in place, the dashboard was built page by page. Each page was given a specific focus and a consistent set of interactive filters that a user could adjust without leaving the page.

DAX Measures

Before placing visuals, the core measures were defined using DAX. These included:


Total Loan — calculated using SUMX across the loan columns to aggregate the full portfolio value
Total Deposit — summing all deposit product types: bank deposits, savings accounts, checking accounts, and foreign currency holdings
Total Fees — aggregating processing fee revenue across the client base
High Risk Clients — a CALCULATE and FILTER measure that counts clients above a defined risk weighting threshold
Total Clients by Engagement Timeframe — using DATEDIFF to calculate how long each client has been with the bank and grouping them into ranges


Page 1 — Banking Analytics Dashboard (Home)

The home page opens with four KPI cards at the top showing the headline numbers: 3,000 total clients, 4.38bn in total loans, 3.77bn in total deposits, and 158.19M in total fees. Below the KPI cards, the page breaks down the client base by banking relationship type, by income band, by loyalty class, and by region. A filter panel on the right allows users to slice the entire page by join year, engagement timeframe, gender, and age range.

Show Image
The Home page of the Banking Analytics Dashboard showing KPI cards, client breakdown by banking relationship, income band, loyalty class, and regional distribution.

Page 2 — Loan and Risk Analysis

The loans page focuses on credit risk. The headline KPIs show total loan value broken into bank loans and business lending, credit card balance exposure, and the count of high-risk clients — 482 flagged clients out of the 3,000 total. Three charts run across the middle of the page: total loan by region as a horizontal bar chart, high-risk clients by year as a line chart, and total loan by occupation as another bar chart. Below these sits a detailed client table showing each client's name, total loan value, loyalty class, risk weighting, and assigned investment advisor. A secondary time-series chart tracks bank loans against business lending year by year.

Show Image
The Loans page showing credit risk KPIs, high-risk client trends over time, loan exposure by region and occupation, and the full client-level loan table.

Page 3 — Deposit Analysis

The deposits page mirrors the loans page in structure but focuses on the liability side of the portfolio. Five KPI cards along the top show total deposit at 801.24M, broken into bank deposits at 424.00M, savings accounts at 150.54M, checking accounts at 207.11M, and foreign currency at 19.60M. Charts on this page show total deposit by region, total deposit by loyalty class, and a donut chart breaking down the product mix across the four deposit types. A client engagement timeframe chart shows how long clients have been active, segmented into 1-5 years, 5-10 years, and more than 10 years.

Show Image
The Deposit Analysis page showing deposit KPIs broken down by product type, region, loyalty class, and client engagement duration.

Page 4 — Data Explorer (Q&A)

The fourth page provides an open-ended exploration tool built around a decomposition tree visual. Starting from the total loan value of 4.38bn, users can drill down by region, then by occupation, then by risk weighting — or in any order they choose. The decomposition tree recalculates in real time as the user selects drill-down paths, making it possible to answer questions that were never anticipated when the dashboard was designed.

Show Image
The Data Explorer page showing the decomposition tree breaking down total loan value by region, occupation, and risk weighting.


Phase 7 — Publishing to Power BI Service

Tools: Power BI Service (app.powerbi.com)

Once the dashboard was complete in Power BI Desktop, it was published to Power BI Service to make it accessible as a live report. Publishing to Power BI Service converted the .pbix file into a hosted report that any authorised user can open in a browser — no Power BI Desktop installation required.

The live report preserves all the interactivity built into the dashboard. Every filter, every drill-down, and every cross-visual highlight works exactly as it does in the desktop version. The report is currently accessible via Power BI Service at the link below.

View the Live Dashboard on Power BI Service


Key Findings


The total loan portfolio across 3,000 clients stands at 4.38bn, with European clients accounting for the largest share by region.
482 clients were flagged as high risk, representing a segment that warrants closer monitoring from investment advisors.
Business lending of 2.60bn sits alongside bank loans of 1.77bn, with a notable upward trend in business lending in the years approaching 2020.
The deposit portfolio totals 801.24M, with bank deposits making up the largest share and foreign currency holdings representing the smallest.
The majority of clients — over 50 percent — fall in the mid income band, which also accounts for the largest share of loan uptake.
Client engagement data shows a significant portion of the client base has been with the bank for more than 10 years, suggesting high retention in the core portfolio.



Skills Demonstrated

Python · Pandas · Matplotlib · Seaborn · Jupyter Notebook · MySQL · SQL · Relational Schema Design · Multi-Table Joins · Data Cleaning · Exploratory Data Analysis · Power BI · DAX · Star Schema · Data Modelling · Power Query · KPI Dashboard Design · Canva · Business Intelligence · Data Storytelling · Power BI Service


How to Run This Project

Python EDA

bashpip install pandas matplotlib seaborn jupyter
jupyter notebook python/eda_analysis.ipynb

MySQL Setup

sqlSOURCE sql/schema.sql;
SOURCE sql/queries.sql;

Power BI Dashboard


Open dashboard/Banking_Dashboard.pbix in Power BI Desktop
Update the MySQL data source to point to your local instance
Click Refresh to reload the data
Navigate between pages using the top navigation bar



Feedback welcome — connect with me on LinkedIn or drop me an email.
---

## Connect:

OLAMIDE AKANNI

[![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://www.linkedin.com/in/olamide-akanni-b240ab18a/)
[![Substack](https://img.shields.io/badge/Substack-FF6719?style=for-the-badge&logo=substack&logoColor=white)]([YOUR_SUBSTACK_URL](https://substack.com/@lamideakanni03))
[![Gmail](https://img.shields.io/badge/Gmail-EA4335?style=for-the-badge&logo=gmail&logoColor=white)](mailto:akannilmd@gmail.com)

---

Feedback welcome!
