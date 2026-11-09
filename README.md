# Van Log

A single web page (`index.html`) for keeping track of every van in the DPD franchise: leases, mileage, MOTs, services, insurance, tyres, batteries, drivers, issues and repairs. It is in the same style as the Driver Pay Log, the DPD P&L Tracker, the EV Charging Log and the Damages & Claims Log, and its downloads go straight into the P&L.

The page is published as a claude.ai Artifact, which keeps the log in its own database and stores photos and invoices with it. If you open `index.html` straight from this repo instead, it saves to that browser only and can't upload files (links still work).

## First-time setup (FDs, drivers & rules tab)

1. **FDs:** FD number/name, email and depot (Raunds / Glenfield by default), as in the P&L Tracker. Each van runs on an FD, so its costs land on that FD in the P&L.
2. **Drivers:** the same names as in the Driver Pay Log and the Damages & Claims log.
3. **Rules:** first day of a 4-week pay period (2 Nov 2026, the same as the other trackers), depots, how many days' warning (30), how many miles before a service to warn (1,000), when an issue counts as "not looked at" (3 days) and when to ask for a new mileage reading (14 days).
4. **Claims:** in the Damages & Claims log, *All claims → All → Download CSV*, then *Import claims CSV* here. Each claim shows on its van's page and can be linked to a repair.

Then add each van under **Vans → Add a van**.

## What is recorded per van

- Reg, make/model, fuel, first registration date, VIN, depot, FD
- Status: on the road / off road / in repair / off fleet, since when, and a note
- Owned or leased. Leased: lease company, monthly cost, start and end dates, annual mileage allowance, mileage at lease start, excess mileage charge, and whether maintenance is included
- Assigned driver, with a full history of who has driven it and when
- Mileage readings (bulk entry on the **Mileage** tab; mileage on events counts too)
- Insurance provider, policy number, renewal date, annual premium; breakdown cover; road tax due date
- MOT due date. Left blank, the first MOT is worked out as 3 years from first registration
- Last service (date and mileage), next service due (date and/or mileage), service interval
- Tyres: last change date and notes
- Battery health %, real-world range and notes (electric and hybrid vans)
- Documents and photos: V5, lease agreement, insurance certificate, MOT certificates, photos

## Events

Date, type (service / repair / breakdown / tyres / MOT / other), description, garage, mileage, cost, who paid (the business, lease company, warranty or insurance), invoice number and whether it's paid, days off road, invoices and photos, and the related claim from the Damages & Claims log (or its DPD ref).

Logging an event also updates the van: an MOT sets the next MOT date, a service sets the last and next service (filled in from the van's service interval), tyres set the tyre change date and notes, and you can change the van's status (e.g. back on the road). Ticking an open issue marks it fixed by this event.

## Issues

Anything a driver reports: damage, warning lights, tyres, screenwash and top-ups, bulbs, brakes, wipers, charging, doors, cleaning. Quick buttons fill in the common ones. Each has an urgency (unsafe / fix soon / minor), photos, a DPD claim ref for damage, and progress (reported → booked in → fixed). An unsafe issue marks the van off road. Issues still "Reported" after 3 days are flagged as not looked at.

## Alerts

30 days before (and after) any MOT, service, insurance renewal, road tax or lease end; a service coming up by mileage (using the van's recent miles per day); a leased van on track to go over its mileage allowance, with the likely excess charge; unsafe issues and issues not looked at; and vans with no recent mileage reading.

## Lease mileage

Allowance over the lease = annual allowance × lease length. The van's pace is miles used since the lease started ÷ days since then. Projected mileage at lease end = used so far + pace × days left. If that's over the allowance the van is flagged, with the excess × the pence-per-mile charge.

## Views

- **Dashboard:** for all vans, a depot, an FD or one van, with costs for a pay period, the last 12 months or all time. Tiles for vans on the road, overdue, due soon, open issues, maintenance cost, days off road, vans over lease pace and unpaid invoices. Alerts, open issues, by van and by depot. Fleet report CSV.
- **Vans:** the fleet list, and each van's own page with its alerts, key dates, insurance, lease and mileage meter, tyres and battery, issues, event log, driver history, mileage readings, damage claims and documents.
- **Log an event**, **Issues**, **Mileage**.
- **Costs & P&L:** per 4-week pay period, by van (split by event type), by FD, every event, and a 13-period trend.
- **All events:** search, filter, edit, delete, CSV, and each event with its invoices and photos.

## Feeding the P&L

On *Costs & P&L*:

- **Download for P&L:** one line per FD per day with the van maintenance the business paid. Costs paid by the lease company, warranty or insurance are left out. Damage costs aren't included: they reach the P&L from the Damages & Claims log, so nothing is counted twice.
- **Download van hire & insurance:** each FD's lease cost and insurance per 4 weeks (monthly × 12 ÷ 13, annual premium ÷ 13) for the P&L's *Wages, van & insurance* tab.
- **Copy summary:** a short text summary of the pay period and anything due.
