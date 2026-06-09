# Inspection & MOT Planner

A single, self-contained offline HTML tool that projects each bus's future **42-day
preventative-maintenance cycle** and pulls a recurring **inspection** to land a few days
before its **MOT** — so one visit covers both the routine inspection and the MOT prep,
with scope to fix anything found before the certificate expires.

## Use
1. Open `inspection-mot-planner.html` in any modern browser (works fully offline — the
   `.xlsx` reader is bundled in).
2. Upload the two spreadsheets:
   - **Current Service sheet** — the `Sheet1` export (Equipment, Sequence, PM Due, …).
   - **Fleet & MOT list** — Fleet Number, Depot, MOT Next Due, …
   (Both `.xlsx`; `.csv` also accepted.)
3. Set the global options and the per-depot MOT days / weekly capacity, then **Generate plan**.
4. Drill **Depots → bus → plan**. Export the plan to **CSV** or **Print/PDF**.

## How it plans
- The 48-step 42-day service sequence (`A B A C A B A <year-end>` per year, years 1–6 ending
  D E F E D G) is hardcoded and wraps 480→10. Each step is an inspection **plus** the rotating service.
- Each bus is anchored to its next-due open work order (or projected from its last completed
  service) and stepped forward every 42 days.
- For each MOT, the latest inspection in the months before expiry is **nudged ±3 days** so an
  allowed depot MOT day lands `days-before-test` after it, before expiry and within weekly capacity.
- Non-working days (configurable Mon–Sun) and UK (England & Wales) bank holidays (toggle) are
  excluded. Buses that can't be aligned (e.g. overdue) are flagged rather than forced.
