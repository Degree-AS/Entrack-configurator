# Entrack Machine Configurator – clickable prototype (phase 1)

A single-file HTML prototype of a seller-facing excavator configurator and quote tool for Entrack (Kobelco dealer). It shows the intended UX and pricing logic. It is a demo: there is no backend, no ERP integration, and all data is illustrative.

Project context: the Notion pages "Short project description" (technical brief) and "Insight workshop 30.9.26", plus the internal meeting notes.

## How to open

Double-click `entrack-konfigurator.html`. It runs in any modern browser, with no install or server. Everything it needs is inside the file (three.js and product photos are embedded, so the file is about 1.2 MB).

If you serve it through a local web server and don't see recent changes, force-reload the page (Ctrl+F5).

## What the prototype shows

Four steps: **1 Machine → 2 Equipment → 3 Customer → 4 Quote**, with a live price summary on the right (bottom bar on mobile).

- Machine selection (6 Kobelco models, SK75 is "most sold"), stock status, and "most sold" presets.
- Options filtered by machine compatibility (weight class, coupler), grouped as Hurtigliste, Fabrikkvalg (KOB-), Ekstra opsjoner, Brukt utstyr. Dependencies are added automatically (tiltrotator adds prep kit and hydraulics).
- Visual configuration: product photos with overlays for SK75 (tiltrotator in yellow or red, beacon bar, work lights placed by tap and drag, night mode), and a procedural 3D model for the other machines.
- Pricing engine: currency conversion, import add-on, labour hours, reserve, commission, target net DG, rounding, and a seller price override (`Overstyr pris`).
- Quote document: web view, print to PDF, customer link, versions, and statuses.
- Admin panel `Kalkylegrunnlag` for FX rates, hourly rate, margins, and the approval threshold.

## Added in this round of changes

**Roles and approval**
- Role switcher in the header (Selger / Leder), demo only.
- A seller doesn't see `Kalkylegrunnlag`, the price breakdown, or gross DG, and sees only their own quotes. A leder sees everything.
- Saving a quote with net DG below the threshold sets it to `Til godkjenning`. The customer link and PDF stay locked until the leder approves it.
- Statuses move forward only: Utkast → Sendt, Godkjent → Sendt, Sendt → Akseptert / Avslått (with a reason). `Godkjent` and `Avvist` are set only by the leder, with buttons, on quotes waiting for approval.
- Step 4 shows the saved quote's status and a message that matches it.

**Product search and linking (step 2, "Finn produkt")**
- Search by item number or name over 16 invented products.
- "Husk koblingen" saves a link between a product and one machine or a whole weight class, so the product then appears in the normal option lists. Saved links can be removed.
- The empty search shows example products not yet available for the machine, and "Sist brukt" items taken from the seller's saved quotes.

**Templates**
- "Lagre som mal" at the bottom of step 2 saves machine, options, lights, and search-added items.
- Templates are listed in step 1 with live prices. A leder can share a template with all sellers.

**Quote numbering**
- Sequential per year: `T-2026-1001`, `T-2026-1002`, and so on. The final number is assigned at first save, and new versions keep it.

## Where the data is stored

Only in the browser's `localStorage`. Quotes, templates, saved product links, price parameters, and the chosen role exist only on that device and browser. Clearing site data removes them, and a different browser or iPad starts empty. Unsaved work is not restored after a page refresh (it returns to step 1).

The keys are `entrack-konfig-tilbud-v1`, `entrack-konfig-params-v1`, `entrack-maler-v1`, `entrack-relasjoner-v1`, and `entrack-role`.

## Known limitations

- Demo data only: machines, options, prices, FX rates, sellers, and the 16 search products are invented and hard-coded.
- No server: sequential numbers can collide between devices, and the customer link carries the whole quote inside the URL (no expiry, no revoke).
- No accept/decline buttons for the customer in the link view. The brief places those in phase 2.
- Nothing stops a seller from adding a product that doesn't fit the machine, beyond the weight range. A confirmation step and leder-only class-wide links were discussed and postponed.
- Not tested on iPad layout or dark mode.
- The ready-made "most sold" presets can't be edited yet.

## Open questions for Entrack

- Who approves quotes below the margin threshold, and is the 8% threshold right?
- Are the import add-on, reserve, and commission percentages correct, and does the base machine price come from the price/discount matrix or a fixed price?
- Should sellers see the price breakdown, or only the net DG?
- Who may create product links between machines and products?
- Is the customer accept/decline in phase 1 or phase 2?
- Does Entrack have its own quote numbering scheme?

## Other files in this folder

`patch1.py` to `patch8.py` are one-time scripts used to apply the changes above to the original prototype. They are not needed to run the prototype and can be deleted. The original, unmodified prototype is in the Downloads folder.
