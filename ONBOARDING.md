# Getting started on Aprix — Design Validation

Read this first. Fifteen minutes, and you will know what the product does, what is being
built, where the documents are and which one wins when two of them disagree.

---

## 1. The problem

OXXO runs promotional periods across its stores. Each period needs printed artwork —
shelf tags, POP material, posters — roughly **5,000 designs per period, 13 periods a year,
across 5 promotional processes**.

Every one of those designs has to be checked against what was actually approved: the right
price, the right SKU, the right product image, the right legal text and validity dates.
Today about **six people in Promotions Operations do this by hand**. An approved design goes
straight to print, so anything they miss reaches the shelf. A robot exists, but it only reads
text and cannot match exactly.

The bottleneck is not making the designs. It is checking them at volume.

## 2. What we are building

An engine that performs that check automatically. It takes a design, compares it field by
field against the sources of truth, computes a match percentage and issues a verdict:

`Aprobado` · `Pendiente de revisión` · `Rechazado` · `Bloqueado por insumo`

The auto-approval threshold is **98%**, configurable by the Administrator only. Target time
is **one minute per design**.

Three sources of truth are compared against:

| Source | Carries |
| --- | --- |
| Production List | what is actually being printed |
| Promotions Report | promotion terms, prices, mechanics |
| Image bank | reference product images |

Four comparison techniques: OCR for text and prices, QR / Aruco decoding for codes, visual
matching for product images (detection plus embeddings), and date and legal-text checks.

## 3. Three blocks

Option B — the approved scope — is 54 user stories in three blocks:

| Block | What | Stories | ID prefix |
| --- | --- | --- | --- |
| A | Design Validation module — 9 modules | 41 | `VD-<m>.<n>` |
| B | Owned image bank `gdp-image-bank`, Release 1 | 9 | `IB-<n>` |
| C | Vendor portal `vendor-portal-web` + external identity | 4 | `VP-<n>` |

**Why the bank is ours now.** Reference images live in Adobe DAM today. Block B replaces that
with an owned bank and migrates the content — roughly 88 GB, 30,000 SKU images. It is a shared
service: MEP, CCT and PIEP consume it too, not only validation.

**Why the portal is separate.** Artwork is submitted by external print vendors, today through
Workfront. They cannot be let into the internal Aprix portal, so they get their own application
with its own identity. Workfront is retired after parity is verified.

## 4. How it reaches production

Three stages, agreed between OXXO and IceMobile:

1. Print-vendor designs + Adobe bank + manual validation in Workfront — *today*
2. Print-vendor designs + Adobe bank + **IceMobile AI validation**
3. Print-vendor designs + **owned bank** + AI validation — Workfront retired

AI validation ships first, still reading from Adobe, and migrates to the owned bank afterwards.
This is why the engine sits in sprints 3–6 of the backlog and the bank in sprints 8–9.

## 5. Where the UI lives

Two surfaces, split by audience rather than by module.

**Inside Aprix** — a new sidebar node, plus two administrative screens:

- `Administración` — VD-1.1 … VD-1.6
- `Operación` — Modules 2, 3, 4, 6, 8
- `Banco de imágenes` — IB-5 administers the bank from Aprix
- `Proveedores y usuarios` — VP-3, vendor and vendor-user administration

**`vendor-portal-web`** — a separate Angular application, public behind Front Door + WAF + APIM.
The admin portal is never exposed (BR-VP.01). It re-hosts design upload (VD-3.1), the vendor
tray (VD-3.5), read-only results from VD-6.x and POP upload (IB-4).

Screens are duplicated across the two surfaces; **rules are not** — BR-VP.06 forbids a second
implementation, so the portal consumes the module's own APIs.

## 6. Stack and design system

Angular throughout, reusing the existing Aprix design system — the mature system already
carrying the whole product. No separate design system is introduced, the vendor portal
included. What differs between the two shells is density and copy, not tokens or components.

The AI core is **not** built here: product detection (YOLO), embeddings (SigLIP on ONNX
Runtime) and vector search (pgvector) are consumed over API from MEP, the platform IceMobile
already built for OXXO. The only net-new AI component is an open-source OCR service.

## 7. Source hierarchy

When two documents disagree, the higher one wins:

1. **The user story** — acceptance criteria in the functional backlog. This is the requirement
   of record. Anything a design spec or wireframe does that no AC covers is new scope: raise it
   against the user story, do not design around it.
2. **The design spec** — interprets the ACs into behaviour, states and copy.
3. **The wireframe** — a working aid. It shows intent; it does not settle requirements. Its
   demo scaffolding, seed data and shortcuts are not specifications.

A wireframe that behaves more sensibly than an AC is an argument for changing the AC, not a
licence to build the wireframe's version.

## 8. Where things are

```
00-source/     incoming documents as received — never edited
10-decisions/  one file per decision; open questions with owners
20-design/     design system usage, screen specs, assets
30-delivery/   handoff specs, release notes
90-archive/    superseded material
```

Start with [`00-source/INDEX.md`](00-source/INDEX.md): it lists what is held and, just as
usefully, what is referenced but still missing.

## 9. Where the project stands

Authorised 18/09/2026. Twelve two-week sprints, 21/09/2026 – 07/03/2027.
Priorities across the 54 stories: 36 High · 12 Medium-High · 6 Medium.

Screen VD-1.1 `Calendario de validación` is the first into design, with a v1.1 spec and a
wireframe covering all seven of its surfaces.

Things a newcomer should know are still open:

- The contract is signed for a **standalone application**, while the backlog and the solution
  design still describe VD as a module inside Aprix. The reuse of the promotional calendar,
  roles and the `Consulta de Movimientos` pattern was costed as reuse.
- Whether period dates come from the Aprix `Calendario Promocional` or a module-owned calendar
  is unresolved, and AC-02 of VD-1.1 depends on the answer.
- Field weights in the match calculation are undefined, so the 98% threshold cannot yet be
  computed or tested.

The full list is in [`10-decisions/README.md`](10-decisions/README.md).
