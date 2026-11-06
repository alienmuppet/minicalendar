# MiniCalendar project brief

Clarified 6 November 2026. The maintained requirements and proposal are in the
[research brief](docs/research-brief.md) and [product plan](docs/product-plan.md).

## Product direction

- A personal calendar with optional sharing among friends and small groups.
- People can share availability and respond to proposed times, then confirm
  plans together. Social plans, band rehearsals, and gigs are example workflows.
- Connecting as friends grants no calendar access. Each person explicitly
  chooses who can see availability or event details.
- Research connections to existing external calendars now, with implementation
  in a later phase. Manual event and availability entry is the initial proposal.

## Technical direction

- Follow the general architecture of MiniFast and MiniHACCP using the existing
  `http_api` server and server-held application data.
- Build the database/API and responsive Svelte web experience first, followed by
  dedicated iOS and Android apps.
- Adopt the current shared authentication contract and assess the existing apps'
  account, membership, invitation, and concurrency patterns for adaptation.
  Calendar-specific data and business rules belong in MiniCalendar.
- Establish the research and planning documents before implementing application
  code, schemas, or deployment configuration.
