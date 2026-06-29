# Case Study: Internal B2B Client Portal (SUPON Kielce)

## Context

SUPON Kielce supplies workwear, PPE, and fire-safety equipment to B2B
clients (companies that in turn distribute it internally to their own
employees/branches). Before this project, client-facing operations — orders,
complaints, document handovers — were handled manually/offline.

## Task

Build an internal web platform with two sides: an **admin panel** for SUPON
staff to manage clients, orders, and support tickets, and a **client panel**
where client companies can place orders, manage their own employees/branches,
raise tickets, and pull reports — without going through SUPON staff for every
interaction.

## My Role & Approach

I designed and built the platform as a single full-stack Next.js application
with two route groups (admin / client) sharing one codebase, backed by a
relational data model in PostgreSQL via Prisma.

**Access control** — four roles (branch head, client head, SUPON manager,
SUPON admin) with role-based routing: each role is auto-redirected to its own
panel and permission set after login, so admin and client users never see
each other's screens or data.

**Order management** — a full order lifecycle (draft → in progress →
partially/fully sent → delivered/approved/cancelled), with a guided
"new order" flow on the client side and order tracking on both sides.

**Ticketing/complaints** — a support-ticket system (new → in progress →
resolved → closed) for complaints, exchanges, and general requests, with
threaded messages and internal-only notes visible only to SUPON staff.

**Personnel & PPE tracking** — CRUD for client companies' own employees
across branches, including PPE sizing per employee and configurable PPE usage
limits per client/category/time period — so clients can track who's already
received what, within their allotted quota.

**Reporting & documents** — dashboards with KPIs (order volume, ticket
status, etc.) visualized with charts, plus PDF and Excel report export, and
a document model for delivery/handover paperwork (WZ documents) tied to
orders.

**Catalog** — a shared product catalog (categorized by PPE type) that both
admin and client sides read from, with client-specific product associations.

## Tech Stack

Next.js (React) · TypeScript · Prisma ORM · PostgreSQL (Supabase) ·
NextAuth (credentials-based auth, JWT sessions) · Recharts (dashboards) ·
PDF generation for reports · Excel export

## Results

- Replaced manual/offline order and complaint handling with a self-service
  client portal, split cleanly between an admin and a client experience on
  one shared codebase
- Modeled the full client → branch → employee/order/ticket relationship
  structure, including PPE issuance limits per client and category
- Delivered end-to-end workflows for order lifecycle and ticket lifecycle,
  each with explicit status tracking
- Added PDF/Excel reporting so clients can self-serve their own order and
  usage history instead of requesting it from SUPON staff

## What I'd highlight from this project

Designing the data model and permission system so that two very different
audiences (internal staff vs. external client users) share one application
safely — without leaking cross-client or cross-role data — is the part most
relevant to security-adjacent roles: access control design, role separation,
and reasoning about who can see and do what.
