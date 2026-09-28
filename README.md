\# NoodlesCrypto Analytics Platform



\## Project Overview



NoodlesCrypto is an end-to-end cryptocurrency and social-engagement analytics solution built using Python, pandas, MySQL, SQLAlchemy, SQL analytical views, DAX, and Power BI.



The project transforms raw JSON source data into a structured analytics warehouse and interactive business-intelligence dashboards.



The solution covers:



\- Data extraction and transformation

\- Data cleaning and validation

\- MySQL data warehousing

\- Star-schema modelling

\- Aggregation tables

\- SQL analytical views

\- Power BI semantic modelling

\- DAX measures and time intelligence

\- Interactive dashboards

\- Executive-level reporting and storytelling



\---



\## Business Objective



The objective of this project is to convert cryptocurrency and social-media engagement data into structured, decision-ready insights.



The solution enables users to analyse:



\- Overall engagement performance

\- Token performance

\- Reddit vs Twitter engagement

\- Historical engagement trends

\- Currency-level performance

\- Top-performing tokens

\- Executive-level insights



\---



\## Architecture



The end-to-end pipeline follows this structure:



JSON Source Files  

↓  

Python ETL / pandas  

↓  

Data Cleaning \& Validation  

↓  

MySQL `noodles\_dw`  

↓  

Star Schema  

↓  

Python Aggregation Layer  

↓  

SQL Analytical Views  

↓  

Power BI Semantic Model  

↓  

Interactive Power BI Dashboards



\### Architecture Diagram



\[View Architecture Diagram](docs/architecture-diagram.png)



\---



\## Data Warehouse



The analytics warehouse uses a star-schema design.



\### Dimension Tables



\- `DimCurrency`

\- `DimDate`

\- `DimPlatform`



\### Fact Table



\- `FactSocialEngagement`



The central fact table contains social-engagement measures and connects to the currency, date, and platform dimensions using foreign keys.



\---



\## Aggregation Layer



Python and pandas are used to generate analytics-ready aggregation structures, including:



\- `CurrencySummary`

\- `DailySocialSummary`

\- `SocialEngagementSummary`

\- `FactSocialEngagementEnriched`



These structures reduce transformation requirements inside Power BI and support efficient reporting.



\---



\## SQL Analytical Views



The reporting layer uses analytical SQL views including:



\- `vw\_executivedashboard`

\- `vw\_timeseries`

\- `vw\_platformdaily`

\- `vw\_socialanalytics`



These views provide Power BI-ready datasets for executive reporting, platform comparison, time-series analysis, and social analytics.



\---



\## Data Quality \& Validation



The pipeline includes checks for:



\- Null values

\- Duplicate records

\- Data types

\- Aggregation accuracy

\- Expected row counts

\- Referential integrity

\- Orphaned records



Validation is performed before data is consumed by Power BI.



\---



\## Power BI Dashboard



The final Power BI solution contains five analytical pages:



1\. Executive Overview

2\. Platform Analysis

3\. Time Series Analysis

4\. Currency Deep Dive

5\. Executive Storytelling



\### Key Features



\- KPI cards

\- Interactive slicers

\- Cross-filtering

\- Drill-through

\- Bookmarks

\- Time intelligence

\- Month-over-month analysis

\- Token ranking

\- Dynamic Top N

\- Platform comparison

\- Executive storytelling



\---



\## Technologies Used



\- Python

\- pandas

\- MySQL

\- SQLAlchemy

\- Jupyter Notebook

\- SQL

\- Power BI

\- DAX

\- Git / GitHub



\---



\## Main Notebooks



\### `05\_data\_warehouse\_design.ipynb`



Responsible for:



\- Creating the MySQL warehouse

\- Building dimension tables

\- Building `FactSocialEngagement`

\- Loading JSON source data

\- Creating the star schema



\### `06\_powerbi\_prep.ipynb`



Responsible for:



\- Preparing Power BI datasets

\- Creating aggregation structures

\- Creating SQL analytical views

\- Validating aggregation accuracy

\- Running data-quality checks



\---



\## Documentation



Project documentation is available in the `docs/` folder.



\- \[Architecture Diagram](docs/architecture-diagram.png)

\- \[Data Dictionary](docs/data-dictionary.xlsx)

\- \[Technical Runbook](docs/technical-runbook.md)

\- \[User Guide](docs/user-guide.md)

\- \[Demo Presentation](docs/demo-presentation.pptx)



\---



\## Demo Video



A recorded demonstration of the complete solution is available here:



\*\*Loom Demo:\*\* \[Watch the NoodlesCrypto Demo](https://www.loom.com/share/bc83a1c640974d06a5432e84504fc1e8)



The video demonstrates:



\- Architecture overview

\- MySQL star schema

\- Python / Jupyter workflow

\- SQL analytical views

\- Data-quality validation

\- Power BI dashboard pages

\- Interactive reporting features

\- Executive insights



A local copy is also included at:



`docs/demo-video.mp4`



\---



\## Key Insights



The completed dashboard supports analysis of:



\- Recent engagement spikes

\- Leading tokens by engagement

\- Platform-level engagement differences

\- Historical engagement patterns

\- Currency-level performance

\- Engagement momentum and ranking



The Executive Storytelling page combines these findings into a concise management-level reporting view.



\---



\## Documentation Files



| File | Purpose |

|---|---|

| `docs/architecture-diagram.png` | End-to-end system architecture |

| `docs/data-dictionary.xlsx` | Data model and field documentation |

| `docs/technical-runbook.md` | Technical operations and troubleshooting |

| `docs/user-guide.md` | Stakeholder dashboard user guide |

| `docs/demo-presentation.pptx` | Portfolio presentation |

| `docs/demo-video.mp4` | Recorded project demonstration |



\---



\## Project Outcome



This project demonstrates an end-to-end analytics workflow from raw JSON data through Python ETL, data-quality validation, MySQL warehousing, SQL analytical views, and interactive Power BI reporting.



The final solution converts raw cryptocurrency and social-engagement data into structured, reusable, and decision-ready analytical insights.



\---



\## Author



\*\*Reece Gow\*\*



NoodlesCrypto Analytics Platform  

September 2026

