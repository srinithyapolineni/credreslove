# CredResolve – Collections Analytics & Recovery Analysis

## 📌 Project Overview

This project analyzes a synthetic collections analytics dataset for **CredResolve** to understand portfolio quality, payment behavior, recovery performance, data quality issues, and operational collection effectiveness.

The analysis was performed as part of the **CredResolve Data Analyst Assignment**.

The dataset contains multiple relational tables representing accounts, borrowers, payments, calls, agents, campaigns, complaints, field visits, promises to pay, messaging events, and other collections activities.

The analysis focuses on two major areas:

1. **Data Forensics & Quality Assessment**
2. **Recovery & Collections Performance Analysis**

---

## 🎯 Objectives

The key objectives of this analysis are:

- Assess the quality and consistency of the collections datasets.
- Identify duplicate records and inconsistent identifiers.
- Analyze missing values and schema variations.
- Validate financial relationships between principal and outstanding amounts.
- Analyze payment duplication and payment status.
- Calculate overall recovery performance.
- Analyze recovery trends over time.
- Compare recovery across risk segments, DPD buckets, and loan types.
- Evaluate payment-method performance.
- Generate actionable business recommendations for collections operations.

---

## 📂 Dataset

The raw dataset contains **17 relational datasets**.

### Raw Data Files

| Dataset | Description |
|---|---|
| `accounts.csv` | Account and loan-level information |
| `account_status_history.csv` | Historical account status changes |
| `agents.csv` | Collection agent information |
| `agent_sessions.csv` | Agent session activity |
| `borrowers.csv` | Borrower information |
| `call_attempts.csv` | Call attempt records |
| `call_dispositions.csv` | Call disposition information |
| `calls.csv` | Collection call records |
| `campaigns.csv` | Collection campaign definitions |
| `complaints.csv` | Customer complaints |
| `daily_targeting.csv` | Daily collection targeting |
| `data_dictionary.csv` | Dataset and field definitions |
| `field_visits.csv` | Field collection visits |
| `payments.csv` | Payment transactions |
| `promises_to_pay.csv` | Promise-to-pay records |
| `sms_events.csv` | SMS communication events |
| `vendor_telephony.csv` | Vendor telephony records |
| `whatsapp_events.csv` | WhatsApp communication events |

---

## 🛠️ Tools & Technologies

- **Python**
- **Pandas**
- **NumPy**
- **Jupyter Notebook**
- **SQL**
- **GitHub**
- Data analysis and exploratory data analysis techniques

---

# 🔎 1. Data Forensics

The dataset was intentionally designed with several data-quality challenges.

These include:

- Duplicate records
- Duplicate payment IDs
- Duplicate payment references
- Missing values
- Conflicting timestamps
- Multiple time zones
- Multiple schema versions
- Inconsistent identifiers
- Late-arriving events
- Legacy disposition codes
- Multiple agent identifiers
- Inconsistent campaign definitions
- Overwritten-style status history

The analysis therefore begins with a systematic data-quality and consistency audit.

---

## 📊 Accounts Dataset – Key Findings

The accounts dataset contains:

**30,000 rows**

### Status Distribution

| Status | Records |
|---|---:|
| ACTIVE | 7,539 |
| CLOSED | 7,496 |
| PAID | 7,486 |
| WRITEOFF | 7,479 |

No missing status values were found.

### Risk Segment Distribution

| Risk Segment | Accounts |
|---|---:|
| HIGH | 7,552 |
| MEDIUM | 7,533 |
| LOW | 7,513 |
| NPA | 7,402 |

### Loan Type Distribution

| Loan Type | Accounts |
|---|---:|
| CREDIT_CARD | 6,080 |
| AUTO | 6,079 |
| PERSONAL | 5,983 |
| CONSUMER | 5,930 |
| BNPL | 5,928 |

---

## 🌍 Time Zone Distribution

The accounts contain three time zones:

| Time Zone | Records |
|---|---:|
| UTC | 10,096 |
| Asia/Kolkata | 9,981 |
| Asia/Dubai | 9,923 |

This highlights the importance of timezone normalization when performing time-based operational analysis.

---

## 🧩 Schema Version Distribution

| Schema Version | Records |
|---|---:|
| v1 | 10,152 |
| v2 | 10,026 |
| v3 | 9,822 |

Multiple schema versions indicate that schema-aware processing is important when integrating the datasets.

---

# 💰 Financial Data Quality

The accounts dataset contains principal and outstanding amounts.

### Principal Amount

- Mean: **₹403,455.52**
- Minimum: **₹10,055.11**
- Maximum: **₹799,968.38**

### Outstanding Amount

- Mean: **₹349,634.51**
- Minimum: **₹1,002.67**
- Maximum: **₹699,963.89**

### Financial Consistency Issue

A major data-quality issue was identified:

> **13,029 rows have outstanding amount greater than principal amount.**

This represents a significant financial consistency issue that should be investigated before using the raw outstanding values for production reporting.

No negative principal or outstanding values were identified.

---

# 📅 DPD Analysis

The dataset contains Days Past Due (DPD) values ranging from:

**0 to 180 days**

### DPD Statistics

| Metric | Value |
|---|---:|
| Minimum | 0 |
| Average | 56.51 |
| Maximum | 180 |

The most common DPD buckets include:

- 0
- 1
- 5
- 15
- 30
- 45
- 60
- 75
- 90
- 120
- 180

---

# 👤 Identifier Quality

### Account IDs

- Total account IDs: **30,000**
- Unique account IDs: **30,000**
- Duplicate account ID rows: **0**

Account IDs therefore behave as unique identifiers in the accounts table.

### Borrower IDs

- Total rows: **30,000**
- Unique borrower IDs: **10,943**
- Duplicate borrower ID rows: **19,056**

This indicates that borrowers can have multiple accounts.

---

# 💳 2. Payment Analysis

The payments dataset contains payment transaction records with information such as:

- Payment ID
- Account ID
- Borrower ID
- Payment reference
- Amount
- Payment status
- Payment method
- Provider ID
- Event timestamp

---

## 🔁 Payment Duplication

The payment dataset contains:

- **25,000 unique payment IDs**
- **500 duplicated payment IDs**
- **1,000 rows involved in duplicate payment IDs**
- **486 exact duplicate rows**

This demonstrates that duplicate transaction records must be handled carefully before calculating recovery metrics.

---

# 💵 Payment Status Analysis

### Raw Payment Status

| Status | Payments |
|---|---:|
| SUCCESS | 17,880 |
| FAILED | 3,744 |
| PENDING | 2,592 |
| REVERSED | 1,284 |

Successful transactions form the majority of payment records.

---

## Successful Payment Deduplication

Before deduplication:

**Successful payment rows:** 17,880

After deduplication:

**Unique successful payments:** 17,534

### Recovery Amount

| Metric | Amount |
|---|---:|
| Raw SUCCESS amount | ₹1,341,485,926.33 |
| Deduplicated SUCCESS amount | ₹1,315,583,964.64 |
| Duplicate amount removed | ₹25,901,961.69 |

This demonstrates why deduplication is essential before reporting collection recovery.

---

# 🎯 3. Recovery Analysis

Successful payments were matched against account records to determine account-level recovery.

### Payment-to-Account Matching

- Unique successful payments: **17,534**
- Matched payments: **17,534**
- Unmatched payments: **0**
- Match rate: **100%**

---

## 📈 Overall Recovery Performance

| Metric | Value |
|---|---:|
| Total accounts | 30,000 |
| Accounts with successful recovery | 13,284 |
| Accounts without successful recovery | 16,716 |
| Total recovered | ₹1,315,583,964.64 |
| Total outstanding | ₹10,489,035,343.00 |
| Overall recovery rate | **12.54%** |

The overall recovery rate is calculated as:

```text
Recovery Rate =
Total Recovered Amount / Total Outstanding Amount × 100
