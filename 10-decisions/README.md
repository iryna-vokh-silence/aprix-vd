# Decisions

One file per decision: `ADR-NNN_slug.md`.

```
# ADR-NNN — <title>

Date: YYYY-MM-DD
Status: proposed | accepted | superseded by ADR-NNN
Owner: <name>
Affects: VD-x.y, IB-n, VP-n

## Context
## Decision
## Consequences
```

## Closed — to be written up as ADRs

| Decision | Date |
| --- | --- |
| pgvector and a dedicated PostgreSQL instance | 14/09/2026 |
| Vendor identity via Entra External ID, separate tenant | 03/09/2026 |
| Workfront is not part of the target architecture | 28/08/2026 |
| Front end stays Angular, reusing the existing Aprix design system | 22/09/2026 |

## Open — each needs an owner and a date

| # | Question | Blocks | Needed by |
| --- | --- | --- | --- |
| 1 | Aprix-direct vs Data Lake for period inputs | Module 2 | sprint 3 |
| 2 | Field weights in the match calculation | VD-1.4, VD-4.7 | before Module 4 acceptance |
| 3 | Is the 98% threshold measured per design or per field | VD-4.7 | before Module 4 acceptance |
| 4 | Image-bank metadata model (BI-01) and the N:M relation (BI-12) | IB-1 | sprint 8 |
| 5 | Fate of the existing text-reading robot: replace, reuse or coexist | Module 4 | — |
| 6 | Does MEP raise an internal cross-charge for the shared platform | cost model | — |
| 7 | Who carries the run-cost of the OCR service on MEP's ARO | infrastructure | — |
| 8 | OCR model selection — PaddleOCR / TrOCR / docTR — and validation on real artwork | phase P1 | — |
| 9 | Workfront cutover criteria, who verifies parity and on which period | VP-2 | — |
| 10 | BI-04 and BI-11 are absent from the client PDF | traceability | before planning |
| 11 | Which SI applies — 446120 or 446457 | commercial | — |
| 12 | VD contracted as a standalone application, while the backlog and solution design describe it as a module inside Aprix. Affects the reuse of the promotional calendar (P1–P13), roles and users, and the `Consulta de Movimientos` pattern — all three costed as reuse in the Tech Lead model. | scope, estimate | architecture review |

## Inconsistencies found in the source material

- BR-05.04 and the v1 *Out of scope* section still state that the module consumes the image
  bank and does not administer it, while Block B is precisely its administration.
- VD-6.4 AC-01 offers two mutually exclusive rules for closing a cycle with open items, and
  the same question appears unresolved in the open points.
- IB-10 (folder structure and templates) sits outside the 54 stories, yet IB-1 AC-07 already
  requires every image to belong to a folder and inherit its metadata.
- Vendor isolation is stated in four places — VD-1.6 AC-03, VD-3.5 AC-06, IB-4 AC-04,
  BR-VP.02 — in different wording. Worth one cross-cutting requirement with one acceptance test.
- No story covers migration of in-flight cycles or documents at the Workfront cutover.
