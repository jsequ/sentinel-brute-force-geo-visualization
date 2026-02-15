# Azure Sentinel Brute Force Geo Analysis

## Project Overview

This project demonstrates detection and visualization of potential brute-force authentication activity using Microsoft Sentinel and Kusto Query Language (KQL).

The objective was to identify geographic patterns of repeated failed sign-in attempts and build an operational monitoring layer to improve investigation speed, visibility, and threat prioritization.

---

## Objective

Detect and visualize high-volume failed login attempts over a 30-day period to identify potential brute-force or credential-stuffing activity targeting identity infrastructure.

---

## Tools & Technologies Used

- Microsoft Sentinel
- Azure Log Analytics
- Kusto Query Language (KQL)
- Sentinel Workbooks
- Geo-visualization (Map view)
- Azure Entra ID Sign-in Logs

---

## Detection Logic

The detection logic aggregates failed authentication attempts and groups them by country to identify geographic attack concentration.

### Investigation Flow:

1. Filter sign-in logs for failed authentication attempts.
2. Extract geographic metadata from login records.
3. Aggregate failed attempts by country.
4. Visualize results using a Sentinel Workbook map.
5. Use geographic concentration to prioritize high-volume sources for investigation.

---

## KQL Query

<img width="1919" height="791" alt="image" src="https://github.com/user-attachments/assets/d5cad6e6-4127-4b5f-8ae9-7a143cda9626" />

```kql
SigninLogs
| where TimeGenerated >= ago(30d)
| where ResultType != 0
| extend Country = tostring(LocationDetails.countryOrRegion)
| where isnotempty(Country)
| summarize FailedAttempts = count() by Country
| sort by FailedAttempts desc```markdown
## 📊 Dashboard Overview

![Sentinel Brute Force Dashboard](https://github.com/user-attachments/assets/d5cad6e6-4127-4b5f-8ae9-7a143cda9626)
