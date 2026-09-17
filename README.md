# Customer Sentiment Analysis System

A comprehensive Python-based customer sentiment analysis system that transforms unstructured customer feedback into structured business intelligence – identifying sentiment patterns, pain points, and actionable recommendations for data-driven decision-making.

---

## Table of Contents

- [Project Overview](#Project-Overview)
- [Business Problem](#business-problem)
- [Dataset](#dataset)
- [Data Dictionary](#data-dictionary)
- [Data Cleaning](#data-cleaning)
- [Methodology](#methodology)
- [Risk Scoring Model](#risk-scoring-model)
- [Analysis & Findings](#analysis--findings)
- [Key Insights](#key-insights)
- [Recommendations](#recommendations)
- [Limitations](#limitations)
- [Conclusion](#conclusion)
- [Project Structure](#project-structure)
- [System Requirements](#system-requirements)
- [Installation & Setup](#installation--setup)
- [Connect With Me](#connect-with-me)

---

## Project Overview

AfriCart Digital Services receives customer feedback across **four African markets** (Nigeria, Ghana, Kenya, South Africa) through **four channels** (Website, App, WhatsApp, Social Media). This project analyses **30 customer feedback records** to understand customer sentiment, identify pain points, and provide actionable recommendations.

### What This System Does

- **Classifies sentiment** (Positive, Neutral, Negative) using rule-based keyword matching
- **Scores customer risk** using a weighted risk model (Low → Critical)
- **Identifies complaint categories** (Delivery, Product Quality, Customer Service, Payment, Other)
- **Generates business intelligence** for management decision-making
- **Produces actionable recommendations** prioritized by business impact

---

## Business Problem

AfriCart receives hundreds of unstructured customer comments daily. Management could not easily answer:

- Are customers happy?
- What are customers complaining about?
- Which country has the most negative feedback?
- Which channel receives the most complaints?
- Are delivery problems affecting customer sentiment?
- Are unresolved complaints associated with negative feedback?
- Which issues should management address first?

**The Challenge:** Turn unstructured customer feedback into structured business intelligence so management can make evidence-based decisions.

---

## Dataset

| Attribute | Details |
|-----------|---------|
| **Source** | `customer_feedback.csv` (synthetic dataset for educational/portfolio purposes) |
| **Total Records** | 30 (sample version) |
| **Columns** | 12 |
| **Countries** | 4 (Nigeria, Ghana, Kenya, South Africa) |
| **Channels** | 4 (Website, App, WhatsApp, Social Media) |
| **Product Categories** | 3 (Electronics, Fashion, Groceries) |

---

## Data Dictionary

| Column | Meaning |
|--------|---------|
| Feedback_ID | Unique identifier for each feedback record |
| Customer_ID | Unique customer identifier |
| Date | Date feedback was submitted |
| Country | Customer's country |
| Channel | Platform through which feedback was received |
| Product_Category | Category of product purchased |
| Rating | Customer rating from 1–5 |
| Delivery_Days | Actual delivery duration (in days) |
| Expected_Delivery_Days | Expected delivery duration (in days) |
| Resolution_Status | Whether complaint was resolved (Resolved/Unresolved) |
| Resolution_Days | Number of days taken to resolve the complaint |
| Feedback_Text | Customer's written feedback (unstructured text) |

---

## Data Cleaning

| Step | Action | Method |
|------|--------|--------|
| 1 | **Missing Values** | Date column had missing values (FB004 onwards) – noted but did not affect sentiment analysis |
| 2 | **Case Standardization** | Feedback text converted to lowercase using `.lower()` |
| 3 | **Whitespace Trimming** | Extra spaces removed using `.strip()` |
| 4 | **Data Type Conversion** | Numeric fields converted from strings to integers using `int()` |
| 5 | **Category Consistency** | Country and Channel values checked for consistent capitalization |

---

## Methodology

### Sentiment Classification (Rule-Based)

Advanced NLP was not used. Instead, a simple **rule-based sentiment classifier** was built using keyword matching.

**Positive Words:**
`excellent, great, good, fast, helpful, love, loved, quick`

**Negative Words:**
`bad, poor, late, slow, failed, disappointing, disappointed, terrible`

**Logic:**
1. Convert feedback text to lowercase
2. Count how many positive words appear
3. Count how many negative words appear
4. If `positive_count > negative_count` → **Positive**
5. If `negative_count > positive_count` → **Negative**
6. If equal → **Neutral**

### Tools Used

- Python's built-in `csv` module (no Pandas)
- Basic Python: variables, loops, conditionals, lists
- Microsoft Excel for data visualisation

---

## Risk Scoring Model

### Weighted Risk Factors

| Factor | Weight |
|--------|--------|
| Rating (1) | 25 points |
| Rating (2 and 3) | 15 points |
| Severe Delivery Delay (>5 days) | 20 points |
| Moderate Delivery Delay (3 to 5 days) | 10 points |
| Unresolved Complaint (aging) | 20 points |
| Unresolved Complaint (new) | 10 points |
| **Maximum** | **100 points** |

### Risk Classification

| Score Range | Risk Level |
|-------------|------------|
| 0–19 | Low Risk |
| 20–39 | Medium Risk |
| 40–59 | High Risk |
| 60+ | Critical |

---

## Analysis & Findings

### 7.1 Sentiment Distribution

| Sentiment | Count | Percentage |
|-----------|-------|------------|
| Positive | 15 | 50.0% |
| Neutral | 3 | 10.0% |
| Negative | 12 | 40.0% |
| **Total** | **30** | **100%** |

**Negative Rate: 40%**

![Overall Sentiment Distribution]<img width="742" height="452" alt="image" src="https://github.com/user-attachments/assets/7ce17026-4ede-4dd7-b5b2-1fb880a50897" />

*Figure 1: Overall Sentiment Distribution (Positive 50%, Neutral 10%, Negative 40%)*

### 7.2 Customer Rating

**Average Rating: 3.27 / 5.00**

| Rating | Count |
|--------|-------|
| 1 star | 5 |
| 2 stars | 6 |
| 3 stars | 4 |
| 4 stars | 6 |
| 5 stars | 9 |

![Customer Rating Distribution]<img width="480" height="288" alt="image" src="https://github.com/user-attachments/assets/b648fab2-3114-4153-a49a-54633f6875c0" />

*Figure 2: Customer Rating Distribution (30 records)*

### 7.3 Delivery Analysis

| Delivery Status | Count | Percentage |
|-----------------|-------|------------|
| On Time | 18 | 60.0% |
| Slight Delay | 3 | 10.0% |
| Moderate Delay | 8 | 26.7% |
| Severe Delay | 1 | 3.3% |

![Delivery Delay vs Sentiment]<img width="494" height="307" alt="image" src="https://github.com/user-attachments/assets/f48987ea-972d-42b5-b93d-e415b9f45073" />

*Figure 3: Delivery Delay vs Sentiment (severe delays always produce negative feedback)*

### 7.4 Resolution Analysis

| Status | Count | Percentage |
|--------|-------|------------|
| Resolved | 19 | 63.3% |
| Unresolved | 11 | 36.7% |

![Resolution Status vs Sentiment]<img width="485" height="352" alt="image" src="https://github.com/user-attachments/assets/9db0326d-498e-4f9c-ba13-1fa846f76fd3" />

*Figure 4: Resolution Status vs Sentiment (unresolved complaints are 100% negative)*

### 7.5 Negative Feedback by Country

| Country | Negative | Total | Negative Rate |
|---------|----------|-------|---------------|
| Nigeria | 6 | 11 | 54.5% |
| Ghana | 4 | 7 | 57.1% |
| Kenya | 1 | 7 | 14.3% |
| South Africa | 1 | 5 | 20.0% |

![Negative Feedback by Country]<img width="752" height="494" alt="image" src="https://github.com/user-attachments/assets/1e06c47a-a32f-4aec-bee4-7abdd7aba5eb" />

*Figure 5: Negative Feedback by Country*

![Sentiment by Country]<img width="512" height="379" alt="image" src="https://github.com/user-attachments/assets/6b9623f1-f06a-4a18-89b9-6443fa1402cf" />

*Figure 6: Sentiment by Country*

### 7.6 Negative Feedback by Channel

| Channel | Negative | Total | Negative Rate |
|---------|----------|-------|---------------|
| Website | 3 | 11 | 27.3% |
| App | 3 | 7 | 42.9% |
| WhatsApp | 0 | 6 | 0.0% |
| Social Media | 6 | 6 | 100.0% |

![Sentiment by Channel]<img width="792" height="504" alt="image" src="https://github.com/user-attachments/assets/07f9d62f-7c5d-47c2-85ab-04d0b580480f" />

*Figure 7: Sentiment by Channel (Social Media 100% negative)*

---

## Sample Delivery Report Output

<img width="1163" height="644" alt="0" src="https://github.com/user-attachments/assets/2c6c0a00-9226-4bb3-8338-832708c959ab" />
<img width="1145" height="558" alt="1" src="https://github.com/user-attachments/assets/9f997ac8-13b8-45ef-8ef7-31e105dd58f0" />
<img width="1153" height="565" alt="2" src="https://github.com/user-attachments/assets/47ff92dc-e038-4c6e-8747-bbf5d7c90174" />
<img width="1126" height="555" alt="4" src="https://github.com/user-attachments/assets/c565b66e-742a-4c67-847f-3dd0589b360e" />
<img width="1107" height="556" alt="5" src="https://github.com/user-attachments/assets/f47b85bf-e396-4235-acdd-5bcd89b6af7b" />
<img width="1150" height="557" alt="6" src="https://github.com/user-attachments/assets/7a0d73ef-1533-4d88-ba1b-46e109aa3481" />
<img width="1146" height="533" alt="7" src="https://github.com/user-attachments/assets/03dba54b-c4ea-4c78-b05f-2a22f49a1109" />
<img width="1239" height="558" alt="8" src="https://github.com/user-attachments/assets/2df07793-7318-4046-82d8-02784e5eb5ba" />
<img width="1119" height="549" alt="9" src="https://github.com/user-attachments/assets/3fcb90c6-a09f-4473-8a08-02ef842962a7" />
<img width="1138" height="540" alt="10" src="https://github.com/user-attachments/assets/8b75f635-bcc2-4290-844c-5bbbebe09785" />
<img width="1197" height="553" alt="11" src="https://github.com/user-attachments/assets/ab0452be-529d-4345-9b08-51ca7da7fbc1" />












## Key Insights

### Finding 1: Unresolved Complaints Are 100% Negative
All 11 unresolved complaints produced negative sentiment. Resolved complaints had only a **5.3% negative rate**. Resolution status is the strongest predictor of customer sentiment.

### Finding 2: Delivery Is the Most Common Complaint Category
**15 out of 30 records (50%)** mention delivery issues. This is by far the largest source of complaints.

![Issue Category]<img width="725" height="452" alt="image" src="https://github.com/user-attachments/assets/d8af7084-6b00-49da-8efd-158ba5dde37d" />

*Figure 8: Issue Category from Customer Feedback Text*

### Finding 3: Severe Delays Guarantee Negative Sentiment
Every severe delay (>5 days) produced negative sentiment. Severe delays are **catastrophic** for customer experience.

### Finding 4: Social Media Is Overwhelmingly Negative
**100% of Social Media feedback** (6 out of 6) was negative. WhatsApp, by contrast, had **0% negative feedback**.

### Finding 5: Ghana and Nigeria Have the Highest Negative Rates
- Ghana: **57.1%** negative rate
- Nigeria: **54.5%** negative rate
- Kenya and South Africa perform significantly better.

### Finding 6: Rating Strongly Aligns with Sentiment
All 1-star ratings were negative. All 5-star ratings were positive. Rating is a reliable proxy for sentiment.

### Finding 7: Payment Failures Produce Strong Negative Sentiment
Only 2 records mentioned payment, but both were negative (100%). Payment failures are **low volume but high impact**.

### Finding 8: 11 Customers Are in HIGH or CRITICAL Risk
Based on the weighted risk model, 5 of 30 customers (16.7%) are at HIGH or CRITICAL risk. All share the profile: **low rating + unresolved complaint + some delay**.

### Finding 9: The Highest-Risk Customer Is FB014
Rating 1, delay of 6 days, unresolved → **risk score 59 → HIGH**

### Finding 10: Product Category Does Not Drive Sentiment
Electronics, Fashion, and Groceries all had mixed sentiment. **Delivery experience overrides product category** as a driver of dissatisfaction.

---

## Recommendations

### PRIORITY 1 — Resolve All 11 Unresolved Complaints Immediately
Unresolved complaints are 100% negative. Every day they remain open increases churn risk.
**Action:** Assign these to a dedicated resolution team with a 48-hour SLA.

### PRIORITY 2 — Fix Severe Delivery Delays
Severe delays guarantee negative sentiment.
**Action:** Audit the logistics process for orders that exceed 5 days past expected delivery. Identify bottlenecks and fix them.

### PRIORITY 3 — Investigate Social Media Complaints
100% of Social Media feedback is negative.
**Action:** Assign a dedicated social media customer service agent to respond within hours, not days.

### PRIORITY 4 — Improve Ghana and Nigeria Operations
Both countries have negative rates above 50%.
**Action:** Review delivery and resolution processes in these two markets. Compare them with Kenya and South Africa.

### PRIORITY 5 — Fix Payment Failure Handling
Payment failures are 100% negative and generate very low ratings.
**Action:** Add automatic retry logic for failed payments and proactive customer notification.

### PRIORITY 6 — Replicate WhatsApp's Success Across All Channels
WhatsApp has 0% negative feedback — the best of any channel.
**Action:** Study why WhatsApp users are happier and apply the same principles to other channels.

### PRIORITY 7 — Maintain Same-Day Complaint Resolution
Resolved complaints with 1-day resolution were overwhelmingly positive.
**Action:** Keep resolution times short and set a company-wide target of resolving complaints within 24 hours.

### PRIORITY 8 — Contact All 11 HIGH/CRITICAL Risk Customers Directly
These customers are at highest churn risk.
**Action:** Reach out personally to each, apologize, resolve their issue, and offer compensation where appropriate.

---

## Limitations

1. **Rule-based classifier** – Uses keyword matching and cannot correctly interpret negation, sarcasm, context, or mixed sentiment.
2. **Small synthetic dataset** – With only 30 records, findings may not generalize to the full customer base.
3. **Correlation ≠ causation** – We found unresolved complaints are associated with negative sentiment, but cannot prove resolving complaints causes positive sentiment.
4. **Risk score weights based on judgement** – A production model would use historical data to calibrate weights.
5. **No repeat customers** – The "repeat complaint" factor in the risk model did not trigger for any customer.
6. **Missing dates limit time-series analysis** – Several records had missing dates, so monthly trends could not be analyzed.

---

## Conclusion

### What Management Should Remember

AfriCart has **two critical problems**:

1. **Delivery delays** – affecting 40% of all feedback and driving most complaints.
2. **Unresolved complaints** – 100% of which are negative.

These two issues are the **root cause of nearly all negative sentiment**. If AfriCart fixes delivery and resolution, the majority of negative sentiment will disappear.

### Strengths to Maintain

-  **WhatsApp channel** – 0% negative feedback
-  **Fast resolution** – Same-day resolution produces positive sentiment
-  **High ratings** – 50% of customers gave 4 or 5 stars

### Three Actions Management Should Take This Quarter

1. **Resolve all 11 unresolved complaints within 48 hours.**
2. **Audit and fix severe delivery delays** – target: zero deliveries beyond 5 days late.
3. **Personally contact the 5 HIGH/CRITICAL risk customers.**

> *AfriCart's path forward is clear: fix delivery, fix resolution, and the sentiment will follow.*

---

## Project Structure

customer-sentiment-analysis-system/
│

├── customer_sentiment_analysis.py    # Main analysis script
│

├── customer_feedback.csv             # Dataset (synthetic)
│

├── README.md                         # Project documentation
│
├── screenshots/                      # Visualizations
│   ├── sentiment_distribution.png
│   ├── rating_distribution.png
│   ├── delivery_vs_sentiment.png
│   ├── resolution_vs_sentiment.png
│   ├── negative_by_country.png
│   ├── sentiment_by_country.png
│   ├── sentiment_by_channel.png
│   └── issue_category.png
│
└── requirements.txt                  # Project dependencies

## Author

**Mustapha Emmanuel Oladeji**  
*Team Captain & Lead Data Analyst*  
Python Study Group – Team H

 **Email:** [mustaphaemmanuelola@gmail.com]  
 **LinkedIn:** [https://www.linkedin.com/in/mustaphaemmanuelola]  
 **GitHub:** [https://github.com/Emmanouhl]

---

## Collaborators

| Role | Name |
|------|------|
| Junior Data Analyst | Ehilawa Blessing Mmesoma |
| Junior Data Analyst | Nnadiukwu Vivian Glory |
| Junior Data Analyst | Ekashili Kechukwu Promise |

---

## Acknowledgments

This project was prepared as part of the **Python Study Group (Team H) Project** – Customer Sentiment Analysis System.

**AfriCart Digital Services** – Turning Customer Feedback into Business Intelligence.
