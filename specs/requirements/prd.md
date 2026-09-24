# Expense Claims — PRD

## Problem Statement

Employees pay for business expenses out of pocket and today have no consistent
way to submit them for reimbursement. Managers lack a clear queue of what needs
their sign-off, and finance has to manually chase approved amounts before they
can be handed off to payroll — a slow, error-prone process with no audit trail
of who approved what and when.

## Solution

A web application where employees submit expense claims with supporting
receipts, their manager reviews and approves or rejects each claim, and finance
gathers all approved claims and exports them for payroll processing — giving
every claim a clear owner and status from submission to payout.

## Actors

- **Employee** — submits expense claims with receipts, views the status of
their own claims, and edits and resubmits a rejected claim.
- **Manager** — reviews claims submitted by the employees who report to them,
and approves or rejects each with an optional comment.
- **Finance** — views all approved claims, exports them to payroll, and marks
exported claims as processed so they are not exported twice.
- **Admin** — assigns each employee to their approving manager, maintaining the
reporting line the approval workflow routes on.

## User Stories

1. As an Employee, I want to submit an expense claim with an amount, category,
 date and description, so that I can be reimbursed for a business expense.
2. As an Employee, I want to attach a receipt to my claim, so that my manager
 and finance have proof of the expense.
3. As an Employee, I want to view the status of my submitted claims (pending,
 approved, rejected), so that I know where each one stands.
4. As an Employee, I want to edit and resubmit a rejected claim, so that I can
 correct the issue my manager flagged and get it approved.
5. As a Manager, I want to see all pending claims from the employees who
 report to me, so that I can review them.
6. As a Manager, I want to approve or reject a claim with an optional comment,
 so that the employee understands my decision.
7. As Finance, I want to view all approved claims across the organization, so
 that I can prepare them for payroll.
8. As Finance, I want to export approved claims to a file, so that I can hand
 them off for payroll processing.
9. As Finance, I want to mark exported claims as processed, so that they are
 never exported to payroll twice.
10. As an Admin, I want to assign each employee to a manager, so that a
 submitted claim routes to the correct approver.

## Product Decisions

- Approval workflow is single-level: an employee's manager is the only
approver, and an approved claim is immediately ready for finance to export.
- Each employee has one designated manager (a fixed reporting line), assigned
by an admin; only that manager sees and approves the employee's claims.
- Sign-in is via SSO through Thunder, the platform identity provider (org
default).
- Receipt attachments are required on every claim. *assumed*
- Employees and managers are notified by email when a claim is submitted and
when it is decided. *assumed*
- Payroll export is a downloadable file (CSV) finance generates on demand;
there is no direct integration into a specific payroll system. *assumed*
- Claims are recorded in a single organization-wide currency. *assumed*
- Expense categories are a fixed predefined list (e.g. Travel, Meals,
Accommodation, Office Supplies, Other). *assumed*

## Out of Scope

- Direct API integration with a specific payroll system — export is a
generated file only.
- Multi-currency claims and conversion.
- Multi-level or delegated approval chains (e.g. finance sign-off before
export, backup approvers).
- Spending limits or policy-based auto-rejection of claims.
- Mobile native apps — web only.

## Open Questions

1. Are there spending limits or per-category policy rules (e.g. a cap on meal
 expenses) that claims must be checked against before approval?
2. Does the payroll export need a specific file layout (columns, format) to
 match an existing payroll system, or is a general CSV of claim data
 sufficient?

## Further Notes

None.