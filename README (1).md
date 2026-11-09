# People & Workplace Operations Tracker (Google Sheets)

A small spreadsheet tracker, built in Google Sheets, that connects **HR contract data** with **physical office tasks**, so nothing falls through the cracks when people join or leave.

> **Sample data only.** All names, IDs, dates and asset numbers in this file are invented. No real personal data is stored.

I built it to practise how HR systems such as Personio organise master data, and to solve one common problem: contract and document checks in HR often live apart from the office tasks they should trigger (laptop, badge, safety briefing).

## What is in the file

The workbook has three tabs. It was built in Google Sheets and is included here as an `.xlsx` export (`People_Workplace_Ops_Tracker_v2.xlsx`), so it also opens in Excel:

| Tab | What it does |
|---|---|
| `Master_Data_Contracts` | One row per employee: role type, start and end date, probation end, tax and social security documents received, GDPR data deleted. Formulas add a **contract alert**, a **compliance check** and a **probation alert**. |
| `Onboarding_Office_Assets` | Lifecycle status (Active, Onboarding, Offboarding), laptop, access badge, safety briefing and desk setup. A formula gives an **asset handover alert**. |
| `Executive_Dashboard` | KPIs for management: active headcount, working students and interns, urgent or expired contracts, missing documents, pending asset collections, probation periods ending soon, headcount by department. |

## Alerts the tracker gives

- **Contracts:** `URGENT: Renew/Offboard` when a fixed-term contract ends within 60 days, `EXPIRED: Offboard now` when it has already ended, `Permanent` when there is no end date.
- **Documents:** `ACTION REQUIRED: Missing Docs` when the tax or social security documents are not yet received.
- **Probation:** `PROBATION ENDS SOON` when probation ends within the next 30 days.
- **Offboarding:** `COLLECT LAPTOP & BADGE` (or only the laptop or only the badge) when someone is set to Offboarding and still has company equipment.
- **Onboarding:** `SCHEDULE SAFETY BRIEFING` when someone is Onboarding and the briefing is still pending.

## Screenshots

**Dashboard**

![Executive dashboard](images/dashboard.png)

**Contract data and alerts**

![Contract data](images/contracts.png)

**Office assets and lifecycle alerts**

![Office assets](images/office-assets.png)

## How it works

- Spreadsheet formulas (Google Sheets, also work in Excel): `IF`, `COUNTIF`, `INDEX`/`MATCH`, `TODAY`
- Dropdowns (data validation) for role type, lifecycle status and Yes/No fields
- Conditional formatting for the alerts
- Tabs are linked by **employee ID**, not by row position, so sorting does not break the data

Example of the contract alert:

```
=IF(F2="","Permanent",IF(F2<TODAY(),"EXPIRED: Offboard now",IF(F2-TODAY()<=60,"URGENT: Renew/Offboard","Active")))
```

## How to use it

1. Download `People_Workplace_Ops_Tracker_v2.xlsx`.
2. Open it in Google Sheets or Excel and add or change rows in `Master_Data_Contracts`.
3. Add the same employee ID to `Onboarding_Office_Assets` and set the lifecycle status.
4. The alerts and the dashboard update automatically.

## Limits and next steps

- Alerts are flags inside the sheet. They do not send emails or notifications.
- Lifecycle status is set by hand and is not driven by the contract end date.
- Next ideas: a reminder list sorted by due date, and a printable checklist for onboarding and offboarding.

Built by Syed Shaheryar Hussain Shah, November 2026.
