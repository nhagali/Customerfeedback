# Prompt 2 — Better

> *You are helping a product manager decide which customer problems to investigate and address first.
> The goal is not merely to summarize the comments. The goal is to make product priorities clearer.
> Use the customer comment, rating, customer segment, product area, and cancellation status when available.
> Do not assume that frequency alone determines importance. Consider severity, affected segment, and
> possible business impact.*

Source: `FlowPilot_Customer_Feedback_Dataset.csv` (90 entries, May 25 – Aug 3, 2026).

## Bottom line

1. **Fix the Salesforce sync now.** It is behind every cancellation in the dataset. The workaround (a manual
   resync) isn't holding.
2. **Hotfix mobile login in v3.8.** It's a new regression that is still getting worse.
3. **Triage the permissions leak as a security incident**, then put enterprise permissions on the roadmap.
   That work is blocking expansion at 8 enterprise accounts.
4. **Don't prioritize dashboard customization** even though it's the loudest request. Look at it as a
   possible reason for Free accounts to upgrade.

## Priority ranking

| # | Priority | Issue | Mentions | Avg rating | Who is affected | Business signal | Recommended action |
|---|---|---|---|---|---|---|---|
| 1 | **P0** | Salesforce integration reliability | 10 | 1.5 | 7 Enterprise, 3 SMB | **4 of 4 cancellations**; 10/10 high churn risk; 9/10 escalated; ~$502k ACV on affected rows; manual resyncs → "issue recurred" / "still at risk" | Dedicated eng. owner; root-cause the skipped updates, latency, duplicates, and silent disconnects; add sync-health alerts; proactive outreach to the 6 at-risk accounts that haven't canceled |
| 2 | **P0** | Mobile login failure (v3.8) | 8 | 1.5 | Startup, SMB, 1 Enterprise (Pro/Enterprise plans) | 100% on v3.8; all reports Jul 26 – Aug 3 and still arriving; 4 escalations; only workaround is reinstall; blocks field teams | Hotfix/rollback the auth/session change in 3.8 (iOS Face ID + Android); add a mobile-login regression test to release checks |
| 3 | **P0 → P1** | Enterprise permissions & admin controls | 8 | 2.4 | 8 Enterprise | ~$684k ACV; blocks security reviews and expansion ("cannot expand beyond one business unit", "Expansion delayed" ×2); **F043: contractors can see projects they shouldn't = possible data exposure** | **Treat F043 as a security incident now.** Then roadmap: roles (view/edit/export), audit logs, external-collaborator approvals, field-level restrictions |
| 4 | **P2** | Performance at scale | 6 | 2.5 | 4 SMB, 2 Enterprise | Everyone affected is a high-usage account; degrades as workspaces grow; 2 escalations; all just "Monitoring" | Profile large workspaces (load, 6-month filters, exports, concurrent edits); set performance targets before it turns into churn |
| 5 | **P2** | Billing accuracy & clarity | 5 | 1.8 | Startup, Enterprise | Low ratings, but mostly fixed case by case (3 × "Customer satisfied") | Small fixes: prorate removed seats, PO number on invoices, clearer annual vs monthly pricing, first-bill preview |
| 6 | **P3** | Onboarding: first data source & setup steps | 4 | 2.3 | SMB (Pro) | Onboarding is mostly a **strength** (6 of 10 "Activated", avg 3.7); these friction points happen at activation | Guided first-connection flow; mark steps as required vs optional; easier teammate invites |
| 7 | **P3 / discovery** | Reporting guidance | 10 | 3.4 | 5 Free Startup, 5 SMB Pro | Low severity, no churn; but the *real* ask is "which metrics matter", not more templates | Discovery on goal-based guided reports / KPI recommendations. That serves this group better than blank templates, and could be a differentiator |
| 8 | **Not now** | Dashboard look & layout | 24 (12 unique) | 2.8 | **Free Startup only** | $0 ACV; no churn risk, escalations, or cancellations; low/medium usage; 15 × "No measurable change" after backlog adds | Don't build it as a fix. Consider a **Pro-tier upgrade hook** (custom layouts/themes). "Without upgrading" appears in the feedback |

## Why the ranking differs from frequency

- **Loudest ≠ most important.** Dashboard customization makes up 27% of all feedback. But half of it is
  duplicate text, and none of it comes from paying customers or risks churn.
- **Churn is concentrated.** Every cancellation (ENT-05, ENT-06, SMB-02, SMB-03) mentions Salesforce data
  trust, and customers say the sync fails at critical moments (quarter-end, pipeline reports).
- **Timing matters.** Mobile has fewer mentions, but every report arrived within 9 days of release 3.8, so
  it's a live regression rather than long-standing friction.
- **Security beats volume.** A single report of unauthorized access (F043) outranks any number of feature
  requests.
- **Expansion revenue is at stake as well as retention.** The permissions gaps are holding back deals with
  the largest accounts, not causing churn today.

## What's working (protect these)

Collaboration (avg 4.8; "main reason we renewed"), templates (4.7), fast and responsive support, and the
basics of onboarding (checklist, sample project, templates → "Activated"). Keep these in mind when
trade-offs come up.

## Caveats about the data

- **Small sample:** 90 rows, about 10 weeks. Treat this as a direction to investigate, not a statistically
  sound result.
- **Contract values aren't consistent per account.** The same account shows different ACVs on different
  rows (e.g. ENT-06 is $52k on one row and $120k on another), and a few Pro-plan values look implausible
  (SMB-01/SMB-02 at $54k/$72k; STP-12 at $87k). The ACV totals above add up affected rows, so read them as
  relative scale, not revenue.
- **Some product-area labels look wrong** (e.g. F089, a comment about the shared timeline, is labeled
  "Support"). This doesn't change the ranking.
- **Rating doesn't equal severity.** Reporting requests have middling ratings but low stakes, while a single
  3-star permissions note (F047, audit logs) is blocking a $120k account's security review.
