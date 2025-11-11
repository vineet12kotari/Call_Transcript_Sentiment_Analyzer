# 🚀 AI-Powered Call Center Analytics: Snowflake Cortex & Streamlit

**A secure, zero-data-movement solution for real-time customer sentiment analysis and summarization, fully deployed within the Snowflake Data Cloud.**  
This project integrates operational call transcript data with **Generative AI** to provide support managers with **immediate, actionable insights** into customer satisfaction and critical issues.

[![Built with Streamlit](https://img.shields.io/badge/Streamlit-Powered-FF4B4B?logo=streamlit)](https://streamlit.io/)
[![Data Source: Snowflake](https://img.shields.io/badge/Data%20Source-Snowflake%20Cloud-0099E6?logo=snowflake&logoColor=white)](https://www.snowflake.com/)
[![AI Engine: Cortex](https://img.shields.io/badge/AI%20Engine-Snowflake%20Cortex-2EA44F)](https://www.snowflake.com/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status: Live Demo](https://img.shields.io/badge/Status-Deployed%20in%20Snowflake-2EA44F)](<LINK_TO_YOUR_SNOWSIGHT_APP_HERE>)

---

## 💡 Core Idea / Project Purpose

This project directly addresses the challenge of **scaling call center quality assurance** and **customer risk management**.  
Manually reviewing high volumes of call transcripts is inefficient, leading to delayed responses to frustrated customers — ultimately causing **customer churn** and **brand damage**.

**The primary goal is to transform unstructured call data into immediate, actionable intelligence:**

* **Risk Prioritization:** Instantly identify *negative sentiment* calls to flag high-risk customers for urgent follow-up.  
* **Operational Efficiency:** Generate concise AI summaries to quickly understand call context without reading the full transcript.  
* **Issue Routing:** Automatically classify topics (e.g., *Billing, Technical Support*) to ensure fast and accurate escalation.  

By running this analysis **natively inside Snowflake**, the solution guarantees:
- 🔒 **Zero data egress** — all processing occurs within Snowflake  
- ⚡ **High-speed inference** using serverless AI  
- 🧱 **Enterprise-grade security and compliance**

---

## 🛠️ Technical Stack: Cloud-Native & Secure

This project leverages a **fully integrated, cloud-native stack** for end-to-end AI-driven analytics.

| Component | Technology | Showcase Skill / Purpose |
| :--- | :--- | :--- |
| **Application Hosting** | **Streamlit in Snowflake (SiS)** | Interactive, secure data apps with **zero data movement** and native deployment inside Snowflake. |
| **Data Engine** | **Snowflake Data Cloud** | Centralized, secure storage for raw `CALL_TRANSCRIPTS`. |
| **AI / NLP Engine** | **Snowflake Cortex AI** | Serverless AI functions for sentiment, summarization, and topic classification. |
| **Data Orchestration** | **Snowpark (Python)** | Executes SQL + Cortex calls directly from Python for real-time analysis. |

---

## 🧠 AI Capabilities & Functionality

The application leverages four **on-demand AI functions** powered by **Snowflake Cortex** — executed only when required to optimize cost.

| Feature | Cortex Function | Purpose | Cost Implication |
| :--- | :--- | :--- | :--- |
| **Sentiment Analysis** | `SNOWFLAKE.CORTEX.SENTIMENT()` | Detects emotional tone (Positive, Negative, Neutral) | 💰 Low (input tokens only) |
| **Summarization** | `SNOWFLAKE.CORTEX.SUMMARIZE()` | Generates 2–3 sentence summaries of long transcripts | 💰💰 Moderate–High |
| **Classification** | `SNOWFLAKE.CORTEX.CLASSIFY_TEXT()` | Categorizes calls into topics (e.g., “Billing”, “Technical Support”) | 💰 Low–Moderate |

These features empower managers to **focus on what matters** — customer emotion, context, and resolution priority.

---

## ⚙️ Key Technical Achievements

This project demonstrates strong engineering and data integration skills within the Snowflake ecosystem:

* **Native Cloud AI Integration:** Combined multiple serverless AI functions (`SUMMARIZE()`, `SENTIMENT()`, `CLASSIFY_TEXT()`) inside the Streamlit workflow — *no external models or APIs needed*.  
* **Secure Parameterized SQL:** Implemented variable passing between Python and Snowflake using the `$$` delimiter, preventing SQL injection and invalid identifiers.  
* **Dynamic Classification Logic:** Constructed flexible SQL arrays (`ARRAY_CONSTRUCT`) to enable adaptive topic tagging.  
* **Cost-Efficient Design:** AI functions run *only when triggered by the user*, aligning with token-based pricing for Cortex.

---

## 🧩 Setup & Running the Project

### 1️⃣ Snowflake Prerequisites

Ensure your Snowflake account has:
- ✅ **Cortex AI functions enabled**  
- ✅ Role with `USAGE` privileges on Cortex  
- ✅ A **virtual warehouse** (e.g., `X-Small`) with **auto-suspend** for cost control  

---

### 2️⃣ Database and Table Setup

Run the following SQL scripts inside Snowsight or SnowSQL:

```sql
-- Create database and schema
CREATE OR REPLACE DATABASE STREAMLIT_DB;
CREATE OR REPLACE SCHEMA STREAMLIT_SCHEMA;

-- Create table for transcripts
CREATE OR REPLACE TABLE CALL_TRANSCRIPTS (
    CALL_ID STRING,
    AGENT_NAME STRING,
    CUSTOMER_NAME STRING,
    CALL_DATE DATE,
    TRANSCRIPT TEXT
);

-- Load sample transcript data
INSERT INTO CALL_TRANSCRIPTS VALUES
('C001', 'Amit', 'John Doe', '2025-10-01', 'Customer reported poor service response...'),
('C002', 'Maya', 'Jane Smith', '2025-10-02', 'Customer appreciated the agent support...'),
('C003', 'Raj', 'Michael Lee', '2025-10-03', 'Billing issue unresolved, customer upset...');
