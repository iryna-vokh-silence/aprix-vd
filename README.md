# Aprix — Design Validation (VD)

Working documentation for the Design Validation product: the validation module, the owned
image bank (`gdp-image-bank`) and the vendor portal (`vendor-portal-web`).
Client: OXXO. Delivery: IceMobile.

Sibling to the `Aprix` repository, which is the client **handover package** for the existing
product. This repository is the opposite: a working repository for a product still being
built. Open questions, deviations and decisions-in-progress belong here, not there.

## Scope

Option B, authorised 18/09/2026 — 54 user stories in three blocks:

| Block | What | Stories |
| --- | --- | --- |
| A | Design Validation module — 9 modules | 41 (`VD-<m>.<n>`) |
| B | Owned image bank `gdp-image-bank`, Release 1 | 9 (`IB-<n>`) |
| C | Vendor portal `vendor-portal-web` + external identity | 4 (`VP-<n>`) |

12 sprints, 21/09/2026 – 07/03/2027. Priorities: 36 High · 12 Medium-High · 6 Medium.

## Layout

| Folder | What goes here |
| --- | --- |
| `00-source/` | Incoming documents **as received**. Never edited — a new version is a new file. |
| `10-decisions/` | One file per decision (ADR). Closed open points land here. |
| `20-design/` | Design system usage, screen specs, exported assets. |
| `30-delivery/` | Handoff specs, release notes, anything shipped to the client. |
| `90-archive/` | Superseded material, kept for traceability. |

## Conventions

- **File names:** `YYYY-MM-DD_slug_vN_LANG.ext`. The date is the document's own date, not
  the day it was filed.
- **Languages:** source documents exist in ES and EN; the suffix is mandatory where both
  exist. Product terminology, UI labels and requirement quotes stay **Spanish, verbatim** —
  never translated, following the convention of the `Aprix` repository.
- **Source is immutable.** Corrections go into a new dated file; the superseded one moves to
  `90-archive/` only once formally replaced.
- **IDs:** `VD-<module>.<story>`, `IB-<n>`, `VP-<n>`, `BR-<module>.<nn>`, `AC-<nn>`.
  The client's complementary bank backlog uses `BI-<nn>`; traceability lives in `10-decisions/`.
- **Binaries** (docx, xlsx, pptx, images) are committed as-is. Expect no useful diffs — the
  decision records carry the human-readable history.

## Getting started

New to the project: read [`ONBOARDING.md`](ONBOARDING.md) first.

## Current inventory

See [`00-source/INDEX.md`](00-source/INDEX.md).

## Status

- Authorisation 18/09/2026 (Renato Bressa). SI issued 21/09/2026.
- Rollout in three stages, agreed Renato / Andrew:
  1. Print-vendor designs + Adobe bank + manual validation in Workfront *(today)*
  2. Print-vendor designs + Adobe bank + IceMobile AI validation
  3. Print-vendor designs + owned bank + AI validation — Workfront retired after cutover
- Contract signed for Option B as a **standalone application**. The backlog and the solution
  design still describe VD as a module inside Aprix. See `10-decisions/`, open point 12.
