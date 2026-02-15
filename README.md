# Azure Sentinel Brute Force Geo Analysis
Objective

Detect and visualize brute-force login attempts using Microsoft Sentinel.

Tools Used

Microsoft Sentinel

KQL

Azure Log Analytics

Sentinel Workbooks

Detection Logic

Aggregated failed authentication attempts over 30 days by country to identify high-volume attack regions.

Query
SigninLogs
| where TimeGenerated >= ago(30d)
| where ResultType != 0
| extend Country = tostring(LocationDetails.countryOrRegion)
| where isnotempty(Country)
| summarize FailedAttempts = count() by Country

Visualization

Configured Sentinel Workbook map:

Location: Country/Region

Size by: FailedAttempts

Coloring: Heatmap

Outcome

Identified geographic concentration of authentication failures and established a baseline for monitoring brute-force activity.
