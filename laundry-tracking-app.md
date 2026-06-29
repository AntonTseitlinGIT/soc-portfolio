# Case Study: Workwear/Laundry Tracking Application

## Context

A laundry service handles workwear for multiple client companies: tracking
which items belong to which employee, at which company/department, and
whether each item is currently issued to an employee or sitting in the
warehouse. This was previously tracked manually, which made it hard to answer
basic questions like "how many jackets does company X currently have out?"

## Task

Build a desktop application to track workwear items end-to-end — from
intake to issuance to an employee, through wash cycles, to eventual
replacement/disposal — across multiple client companies and departments,
with hardware support for fast item identification.

## My Role & Approach

I designed and built the application solo, as a layered desktop app (Python,
Tkinter UI) with a clear separation between the UI, business logic, data
access, and hardware layers — so the hardware integration and the database
layer can both change independently of the screens that use them.

**Hardware integration** — integrated an RFID reader (UHFReader09/YPD-RU5102)
for tagging and scanning individual clothing items, plus barcode utilities
and label printing, so items can be identified without manual lookup. The
RFID connection is managed as a long-lived resource with automatic
reconnection handling, since the app needs to stay usable through reader
disconnects during a shift.

**Core tracking** — clothing items are modeled per employee, per company,
per department, with a current status (issued vs. in warehouse). The main
dashboard gives a drill-down view: totals by company → department → clothing
type, broken down into issued vs. warehouse counts.

**Employee & company management** — CRUD for companies, departments,
positions, and employees, with filtering (by company, department, surname)
and a per-employee "card" view showing their current clothing assignments.
Deletion is guarded — an employee can't be deleted while they still have
items checked out, to avoid silently losing track of issued stock.

**Movement & history tracking** — a dedicated flow for registering
movements (issuance, returns, exchanges) and a full issue-history view for
auditing what happened to a given item or employee over time.

**Reporting & labels** — report generation for stock/issuance summaries, and
a label-printing flow for physically tagging items.

**Data safety** — automatic and manual backup/restore of the local database,
since this is a single-machine desktop tool with no separate backend to fall
back on.

## Tech Stack

Python · Tkinter (desktop UI) · local relational database (SQLite) · RFID
hardware integration (UHFReader09 / YPD-RU5102 SDK) · barcode/label printing

## Results

- Replaced manual tracking of workwear issuance with a structured,
  queryable system broken down by company, department, employee, and item
  type
- Added RFID-based item identification to speed up day-to-day scanning
  versus manual lookup
- Built in safeguards (can't delete an employee with outstanding items;
  automatic backups) to protect against data loss in a single-machine,
  no-backend environment
- Gave staff a single dashboard view of issued vs. warehouse stock per
  company/department, replacing ad-hoc manual counting

## What I'd highlight from this project

This is the project closest to OT/embedded-style work: integrating directly
with a hardware reader over its vendor SDK, handling disconnects/reconnects
gracefully, and designing the data layer so the rest of the app doesn't care
whether an item was scanned via RFID or entered manually.
