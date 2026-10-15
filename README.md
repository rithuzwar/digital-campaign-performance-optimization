# Digital Campaign Performance & Optimization System

A portfolio project demonstrating a lightweight campaign reporting workflow built with Google Sheets, Looker Studio, and Google Apps Script.

> **Data notice:** All campaign data in this repository is synthetic and illustrative. It is not Google Ads account data, client data, or verified business performance. The fictional scenario is a premium-homes lead-generation campaign. The dashboard screenshot is a preview of the author's prototype.

## Project goals

- Organize daily campaign metrics into a consistent source of truth.
- Calculate and compare campaign KPIs such as CTR, CPC, lead conversion rate, CPL, qualified-lead rate, cost per qualified lead, CPA, and ROAS.
- Add data-quality checks and campaign/channel summary views.
- Track budgets, illustrative leads, creative tests, optimization actions, milestones, and risks.
- Visualize campaign and operational status in Looker Studio.
- Generate a weekly summary and append a run record using Apps Script.

## Tools

- Google Sheets — raw data, calculated fields, dictionaries, QA checks, trackers and summary tables
- Looker Studio — campaign and milestone dashboard
- Google Apps Script — weekly report generation and run logging

## Repository layout

```text
.
├── README.md
├── data/
│   └── synthetic_campaign_performance.csv
├── apps-script/
│   └── Code.gs
├── docs/
│   ├── data-dictionary.md
│   └── validation-and-limitations.md
└── assets/
    └── dashboard-preview.png
```

## Dataset

The CSV contains 120 daily campaign records for September 1–30, 2026 (four fictional campaigns). The row grain is one campaign per day. Monetary values are denominated in INR. See `docs/validation-and-limitations.md` for assumptions and caveats.

## KPI definitions

| KPI | Definition |
|---|---|
| CTR | Clicks / Impressions |
| CPC | Spend / Clicks |
| Lead conversion rate | Leads / Clicks |
| CPL | Spend / Leads |
| Qualified-lead rate | Qualified leads / Leads |
| Cost per qualified lead | Spend / Qualified leads |
| CPA | Spend / Sales |
| ROAS | Attributed revenue / Spend |

For aggregated reporting, calculate ratios from summed numerators and denominators; do not average daily ratios unless that is explicitly the intended metric.

## Apps Script setup

1. Create a Google Sheets workbook and import the CSV into a tab named `Raw_Data`.
2. Create `Weekly_Report` and `Reporting_Log` tabs.
3. Put these headers in `Reporting_Log!A1:J1`: `Run_Timestamp`, `Report_Start_Date`, `Report_End_Date`, `Source_Rows`, `Spend_INR`, `Clicks`, `Leads`, `Qualified_Leads`, `Sales`, `Run_Status`.
4. Open **Extensions → Apps Script**, paste `apps-script/Code.gs`, and replace `PASTE_SPREADSHEET_ID_HERE` with your workbook ID.
5. Save and run `generateWeeklyReport` once; review the requested permissions and only authorize if they match the script's spreadsheet-reporting purpose.
6. In Apps Script **Triggers**, add a time-driven weekly trigger for `generateWeeklyReport`.

The script uses the latest date present in the dataset and summarizes the seven-day window ending on that date. With the included September-only sample, scheduled runs will continue to report the same window until newer dated records are added. This is intentional for reproducible demonstration; it is not a live ad-platform integration.

## Dashboard

The Looker Studio report is built separately in the user's Google account. The screenshot in `assets/` is a static preview; it is not an interactive dashboard link. Add a shareable Looker Studio URL here only after setting appropriate access permissions:

`Dashboard URL: TODO — add your shareable Looker Studio report URL`

## Limitations and responsible presentation

- Data is synthetic, not pulled from Google Ads or any client platform.
- The lead pipeline, creative tests, optimization actions, budget plan, and milestone/risk records are illustrative trackers and should not be described as verified historical business activity.
- No real-world reporting-time reduction or setup-time improvement has been measured. Do not claim a 50% reduction without a documented before/after test.
- Attribution and revenue assumptions are simplified for demonstration. They are not a substitute for a production attribution model.
- The weekly trigger is a scheduled Apps Script execution; successful scheduled runs should be verified in Apps Script **Executions** and in `Reporting_Log`.

## Suggested walkthrough

1. Show the data dictionary and QA checks.
2. Explain how the campaign and channel summaries calculate KPIs from totals.
3. Walk through the Looker Studio campaign dashboard and milestone/risk view.
4. Demonstrate `generateWeeklyReport` and the appended `Reporting_Log` entry.
5. Explain what would change before using real ad-platform data: authentication, source refresh, conversion/attribution definitions, permissions, and monitoring.
