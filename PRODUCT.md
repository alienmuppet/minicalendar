# MiniCalendar product context

<!-- impeccable:product-schema 1 -->

## Platform

web

Responsive browser access is the first delivery phase. Dedicated iOS and Android
clients follow; the web prototype does not select their visual design.

## Stack

The confirmed production direction is Svelte with server-held data through
`http_api` and app-owned MySQL business rules. Review mockups use standalone
HTML/CSS/JavaScript with fictional in-memory data, following the workspace's
existing mockup convention. This is a prototyping choice, not a framework change.

## Users and purpose

Individuals organise their own calendar. Friends and small groups share selected
availability, propose times and confirm plans. Bands arranging rehearsals and gigs
are a key example, not a separate exclusive audience.

## Confirmed constraints

- Useful for personal use before any sharing.
- Both ongoing availability sharing and responses to candidate times.
- Friendship grants no calendar access; permissions are explicit.
- Availability, absence of a recorded conflict and attendance are distinct.
- Research external calendar connections now, implement later.

## Evidence on hand

[Research brief](docs/research-brief.md), [source research](docs/research.md) and
[product plan](docs/product-plan.md) record the agreed choices and evidence.
Any people, events, dates and responses in the mockups are fictional. There are
no validated customer findings or approved visual identity yet.

## Open decisions

Public name, pricing, detailed release scope, notification channels, recurrence
subset and guest participation remain open. Recommendations and visual concepts
are for user review. This context does not promote them to confirmed requirements.
