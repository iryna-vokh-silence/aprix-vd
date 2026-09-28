# Design

| Folder | Contents |
| --- | --- |
| `tokens/` | Platform-neutral token export, so Figma and the Angular code read from one source. |
| `specs/` | Per-module screen specs. One file per module: `VD-M<n>_<slug>.md`. |
| `assets/` | Exported icons, images, diagrams. |

## Design system

The existing Aprix design system is used as-is — a mature Angular system already carrying the
whole product. No separate system is introduced for this project, for the vendor portal
included. What differs between the two shells is density and copy, not tokens or components.

Figma library: `PrimeOne 3.1.0` — `vSr6bOBNh0hbBXXqWIXMZn`, per the `Aprix` repository.

## Two UI surfaces

**Inside Aprix** — a new sidebar node with two sections, plus two administrative screens:

- `Administración` — VD-1.1 … VD-1.6
- `Operación` — Modules 2, 3, 4, 6, 8
- `Banco de imágenes` — IB-5, administered from Aprix (IB-5 user story), roles in IB-8
- `Proveedores y usuarios` — VP-3, vendor and vendor-user administration

**`vendor-portal-web`** — a separate Angular application, public behind Front Door + WAF +
APIM (VP-1 AC-01); the admin portal is never exposed (BR-VP.01). It re-hosts VD-3.1 (design
upload), VD-3.5 (vendor tray), the read-only result and observation views from VD-6.x, and
IB-4 (POP upload), per VP-2 AC-01.

Screens are duplicated across the two surfaces; business rules are not — BR-VP.06 forbids a
second implementation, so the portal consumes the module's own APIs.

## Baseline tokens observed in the M1 wireframe

Brand `#81001E` with soft and mid variants · sidebar `#262626`, 272px · radius 8px containers,
6px controls · Inter, tabular-nums on numeric columns · semantic sets green / amber / info /
red / grey, each with text, background and border · 2px focus ring in the brand colour.

To be reconciled against the production design system rather than treated as the source.

## Patterns the wireframe establishes

Data table with status chips · side drawer for edit forms · confirmation modal for anything
with operational impact · savebar for unsaved changes · banners · toasts · permission-gated
screens with an explicit no-access state · read-only mode for closed periods · global audit-log
drawer with export. IB-5 explicitly calls for the same set.
