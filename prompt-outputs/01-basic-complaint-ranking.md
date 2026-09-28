# Prompt 1 — Basic

> *Summarize and rank the most common customer complaints in this dataset*

Source: `FlowPilot_Customer_Feedback_Dataset.csv` (90 feedback entries, May 25 – Aug 3, 2026).
Ranked purely by **how often** each complaint theme appears. Positive feedback is excluded.

| Rank | Complaint theme | Mentions | Avg rating | What customers say |
|---|---|---|---|---|
| 1 | **Dashboard customization** | 24 | 2.8 | Want to change colors, themes, fonts, layouts; move/hide widgets; dark mode; more templates. |
| 2 | **Salesforce integration reliability** | 10 | 1.5 | Sync skips records, arrives hours late, creates duplicates, drops connection; data can't be trusted. |
| 2 | **Reporting guidance** | 10 | 3.4 | Want report templates (exec, board), but mainly don't know which metrics/KPIs matter. |
| 4 | **Mobile login failures** | 8 | 1.5 | Login loops, session expires instantly, Face ID/Android login broken since v3.8. |
| 4 | **Permissions & admin controls** | 8 | 2.4 | Need role-based permissions, audit logs, external-collaborator approvals; contractors see projects they shouldn't. |
| 6 | **Performance at scale** | 6 | 2.5 | Large projects load slowly, filters sluggish, exports time out, freezes under concurrent edits. |
| 7 | **Billing** | 5 | 1.8 | Charged for removed seat, unclear annual vs monthly pricing, missing PO number, surprise first bill. |
| 8 | **Onboarding friction** | 4 | 2.3 | Connecting first data source confusing; unclear required vs optional steps; inviting teammates hard. |

**Summary:** The most frequent complaint by far is dashboard customization (24 mentions, ~27% of all feedback),
followed by Salesforce integration problems and requests for reporting help (10 each). Mobile login and
permissions follow at 8 each.

---

### Why this is "not the best" (teaching note)

This ranking answers the literal question, but it is a poor guide for what to fix first:

- **All 24 dashboard complaints come from Free-plan Startup accounts with $0 contract value**, none at
  churn risk — and 12 of the 24 are verbatim repeats of the other 12.
- **All 4 cancellations in the dataset are Salesforce integration complaints**, which rank only #2.
- **Mobile login is a fresh regression** (every report is on v3.8, all within 9 days), which frequency alone
  can't reveal.
- A **security issue** ("contractors can see projects they should not have access to") is buried inside the
  permissions theme.

See [`02-prioritized-analysis.md`](02-prioritized-analysis.md) for the "Better" prompt.
