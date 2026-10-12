# Requirement Management Hub

Interactive prototype of a SharePoint Online requirements governance and traceability portal. It shows how a business change moves from request to release through six linked levels and seven approval gates (L0–L6), with every decision recorded for audit.

**Live site:** https://hujairy.github.io/reqgov-portal/

> All names, requests and figures are fictional sample data. Nothing is saved: reloading the page restores the original sample data.

## What it demonstrates

- **End-to-end traceability** – every business change request (BCR) links down to business requirements (BR), functional requirements (FR), a solution assessment, test cases, UAT sign-off and a change request.
- **Gated approvals** – a request only moves to the next level when that level's entry criteria pass and the named approver signs off.
- **Segregation of duties** – a requestor cannot approve their own BCR, and a test executor cannot sign UAT.
- **SLA tracking** – each gate has an SLA in working days (Sunday–Thursday, Bahrain working week); breaches are flagged.
- **Audit trail** – every action is logged with who, when, what record and comments.

## The six levels

| Level | Record | Purpose |
|---|---|---|
| L1 | Business Change Request (BCR) | The business driver: title, area, sponsor, justification, impacted systems, priority |
| L2 | Business Requirement (BR) | What the business needs, with acceptance criteria and a Business Owner |
| L3 | Functional Requirement (FR) | The system specification for one impacted system |
| L4 | Solution Assessment (SA) | Approach, vendor involvement, risk rating, effort and architecture approval |
| L5 | Test Cases & UAT | Tests linked to each BR, and the business acceptance sign-off |
| L6 | Change Request | Release approval, deployment and post-implementation review (PIR) |

## Approval gates

| Gate | Decision | Approvers | SLA |
|---|---|---|---|
| L0 | Submission check | Automatic validation | Immediate |
| L1 | BCR approval | Business Sponsor, then Demand Manager | 5 days |
| L2 | FR approval | System Owner approves each FR; Lead BA confirms | 5 days |
| L3 | BR approval & baseline | Business Owner approves each BR; Lead BA baselines | 5 days |
| L4 | Solution assessment | ARB, InfoSec and Risk approve; ARB chair confirms | 10 days |
| L5 | UAT sign-off | QA Lead approves tests; Business Owner signs UAT; Governance Office confirms | 3 days |
| L6 | CAB & release | Change Manager / CAB approve; PIR completed; Change Manager closes | 7 days |

Some reviewers are added automatically: any vendor involvement adds **Third-Party Risk** to the solution assessment, and a High or Critical risk rating adds **Operational Risk**. The change type decides the release route: Normal goes to Change Manager then CAB, Standard to Change Manager only, and Emergency to the Emergency CAB.

## Screens

- **Overview** – the requirements pipeline by level, SLA status and traceability exceptions.
- **BCR Register** – all requests, searchable and filterable by business area and priority. Open one to see its traceability matrix, review cards for each level and its record history.
- **My approvals** – everything waiting for a decision, with a Review button on each item.
- **Audit log** – the full, filterable history of actions.
- **Framework** – reference view of the six levels, their fields, the approval matrix and the controls.
- **Admin** – edit gate SLAs and the dropdown lists (business areas, systems and their owners, priorities, risk ratings, change types and more). Values that drive workflow rules are locked.
- **New request** – raise a BCR; it passes the L0 check, gets an ID and goes to L1.

## Trying it out

1. Open the live site and look at the **Overview** pipeline.
2. Go to **My approvals** and review a pending item. Choose who the decision is recorded by – the prototype enforces the right approver.
3. Open the request in the **BCR Register** to see its status, matrix and history update.
4. Check the **Audit log** for the entry you just created.
5. Raise a **New request** and follow it through the gates.

## Technical notes

- A single self-contained `index.html` (HTML, CSS and plain JavaScript) with no build step or external dependencies.
- Data lives in memory only; there is no backend or browser storage.
- Hosted on GitHub Pages from the `main` branch root (`.nojekyll` disables Jekyll processing).
- In a real deployment each level maps to a SharePoint list with lookups to its parent, and the approval steps map to Power Automate flows (referenced in the audit log as F1–F8).

## Making changes

Edit `index.html` and push to `main`. GitHub Pages republishes the site within a minute or two.
