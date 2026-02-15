# Azure Sentinel Brute Force Geo Analysis

## Project Overview

This project demonstrates how to detect and visualize potential brute-force authentication activity using Microsoft Sentinel and Kusto Query Language (KQL).

The goal was to identify geographic patterns of repeated failed sign-in attempts and build a visual monitoring layer to improve investigation speed and visibility.

---

## Objective

Detect and visualize high-volume failed login attempts over a 30-day period to identify potential brute-force or credential-stuffing activity.

---

## Tools & Technologies Used

- Microsoft Sentinel
- Azure Log Analytics
- Kusto Query Language (KQL)
- Sentinel Workbooks
- Geo-visualization (Map view)

---

## Detection Logic

The detection logic aggregates failed authentication attempts and groups them by country to identify geographic attack concentration.

Key steps:

1. Filter sign-in logs for failed authentication attempts.
2. Extract geographic metadata from login records.
3. Aggregate failed attempts by country.
4. Visualize results using a Sentinel Workbook map.

---

## KQL Query

```kql
SigninLogs
| where TimeGenerated >= ago(30d)
| where ResultType != 0
| extend Country = tostring(LocationDetails.countryOrRegion)
| where isnotempty(Country)
| summarize FailedAttempts = count() by Country

---

<img width="1919" height="791" alt="image" src="https://github.com/user-attachments/assets/087310e2-4089-4a4a-ab32-902042186568" />
