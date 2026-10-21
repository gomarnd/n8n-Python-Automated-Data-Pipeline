# n8n-Python-Automated-Data-Pipeline
Automated Data Pipeline & Workflow Automation (n8n & Python)

#  Project Overview
This project is an enterprise-grade **Automated Data Pipeline** engineered to bridge automated data ingestion, programmatic data manipulation, and real-time storage systems. It eliminates manual intervention by autonomously fetching, processing, and logging live marketing and operational data streams into centralized databases and cloud spreadsheets.

---

# Key Components & Architecture

[Webhook / Schedule Trigger] ──> [REST API Payload Ingestion]
│
▼
[Google Sheets Real-Time Log] <── [Python / Pandas Transformation Node]


1. n8n Workflow Automation:**
   - Manages asynchronous triggers and automated cron schedules.
   - Executes dynamic **REST API** requests to fetch real-time JSON data payloads from external services (e.g., currency exchange rates, ad networks).
2. Python Data Processing Engine (Pandas):**
   - Ingests, cleans, and restructures raw API datasets.
   - Programmatically derives core performance KPIs such as **Cost-Per-Click (CPC)** and **Click-Through-Rate (CTR)**.
   - Categorizes campaign performance dynamically based on threshold logic.
3. Google Sheets Real-Time Sync:**
   - Serves as a dynamic cloud database layer, receiving clean, structured records instantaneously.

---

# Pipeline Stages
- Stage 1 (Ingestion & Triggering):** Webhook execution and payload listener initialization.
- Stage 2 (API Fetching & ETL):** Querying external endpoints to pull live financial/marketing records and applying Pandas transformations.
- Stage 3 (Persistence & Reporting):** Automated data mapping and row serialization into centralized Google Sheets dashboards.

---

# Sample Python Transformation Script (Pandas Node)

```python
import pandas as pd

def process_marketing_payload(raw_data):
    # Load raw JSON response into DataFrame
    df = pd.DataFrame(raw_data)
    
    # Calculate Core Performance Metrics
    df['CPC'] = (df['spend'] / df['clicks']).round(2)
    df['CTR_%'] = ((df['clicks'] / df['impressions']) * 100).round(2)
    
    # Dynamic Performance Classification
    df['Performance_Tier'] = df['CPC'].apply(
        lambda x: 'High Efficiency' if x < 1.5 else 'Needs Optimization'
    )
    
 return df.to_dict(orient='records')
 Strategic Business Value
Zero Human Intervention: Automates repetitive data collection and transformation tasks, saving hours of operational labor.

Real-Time Visibility: Ensures decision-makers always have access to up-to-date performance dashboards.
