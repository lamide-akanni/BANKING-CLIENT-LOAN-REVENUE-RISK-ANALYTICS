# BANKING-CLIENT-RISK-REVENUE-ANALYTICS
Data analytics, from raw data (banking client dataset) ingestion through Python based exploratory data analysis, a normalised MySQL relational database, SQL querying, feature engineering, and into a 4-page interactive Power BI dashboard powered by custom DAX measures


1. Project Overview
Banks sit on large volumes of client-level financial data — loans, deposits, credit card exposure, advisor relationships — but that data is only valuable once it has been cleaned, modelled, and turned into something decision-makers can act on. This project simulates that real-world workflow end to end.

Business problem framed for this project:
Where is the bank's lending risk concentrated, and which client segments carry the heaviest debt burden?
Which client segments represent the strongest deposit and cross-sell opportunity?
How can client-level financial data be structured into a queryable database and a self-service BI dashboard that executives can use without touching code?


The project was built as a full-stack analytics portfolio piece, deliberately using three different tools in sequence — Python, MySQL, and Power BI — to demonstrate competency across the entire analytics lifecycle rather than just the visualisation layer.

2. Tech Stack

LayerTool / LibraryPurposeData SourceCSV (Banking.csv)Raw client-level banking datasetData AnalysisPython 3, Jupyter NotebookExploratory Data Analysis (EDA)LibrariesPandas, NumPyData wrangling, cleaning, feature engineeringLibrariesMatplotlib, SeabornUnivariate/bivariate visualisation, correlation analysisDatabaseMySQL 8, MySQL WorkbenchRelational storage, star-schema modellingConnectivitymysql-connector-pythonLoading cleaned data from Python into MySQLQueryingSQLData validation, aggregation, business questionsBI / VisualisationPower BI DesktopData modelling, Power Query transformations, dashboardingModelling LanguageDAXCalculated columns and KPI measures

3. Project Architecture
4. Raw CSVBanking.csvPythonEDA · Cleaning · FeatureEngineeringMySQLStar-Schema RelationalDatabaseSQLValidation & BusinessQueriesPower BIData Model · Power Query ·DAX4-Page Interactive

5. The pipeline is intentionally linear: each stage hands off a cleaner, more structured version of the data to the next tool, mirroring how a real data team would split responsibilities between data preparation, data engineering, and business intelligence.

5. Dataset & Data Sourcing

The project uses an anonymised, client-level banking dataset of 3,000 records across 25 attributes, structured to mimic a real bank's client portfolio — demographics, account balances, lending exposure, and relationship-management metadata. It was sourced as a structured "fact table" suited to a star-schema design, paired with three lookup/dimension files (Gender, Branch, Investment Advisor) that are joined back to the main table via foreign keys during the MySQL phase.

During data validation, the raw file was found to contain 3,000 total rows but only 2,940 unique Client IDs — a deliberate data-quality scenario that the project surfaces and  rather than silently ignores, reflecting how duplicate-detection is handled in a production setting.

Example cleaning snippet:
import pandas as pd

df = pd.read_csv("data/Banking.csv")

# Integrity check
assert df.isnull().sum().sum() == 0, "Unexpected nulls found"

# Parse join date
df["Joined Bank"] = pd.to_datetime(df["Joined Bank"], format="%d-%m-%Y")

Future Enhancements


Automate the Python → MySQL load with a scheduled script rather than a manual notebook run
Add a basic credit-risk classification model (e.g. logistic regression) on top of the existing Risk Weighting and lending features
Deploy the dataset to a cloud-hosted MySQL instance (e.g. AWS RDS / Azure Database for MySQL) so the dashboard can refresh without a local connection
Publish the dashboard to the Power BI Service and apply Row-Level Security (RLS) by branch/advisor
Add geographic mapping of clients by branch/location for a regional view of risk and revenue

p.s: The dataset used is anonymised and intended for educational and portfolio purposes only.


OLAMIDE AKANNI | Data Scientist
akannilmd@gmail.com
🔗 LinkedIn · GitHub · Portfolio · Email
