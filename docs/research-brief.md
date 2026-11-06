# MiniCalendar research brief

Date: 6 November 2026. Status: agreed direction and initial research foundation,
not a release specification.

## Confirmed requirements

The user selected five product and delivery choices:

1. **Personal plus shared:** the app must be useful for an individual's calendar,
   with optional collaboration among friends and small groups. Bands are a key
   example, not the exclusive audience.
2. **Web first, native next:** establish a responsive Svelte web app and shared API
   first, then dedicated iOS and Android apps. Mobile browser access is part of
   the web phase, not a replacement for the intended native clients.
3. **External calendars later:** research Apple, Google, and Microsoft calendar
   connections now and plan their implementation for a later phase.
4. **Both availability approaches:** support ongoing sharing of available/busy
   periods and responses to specific proposed times, followed by confirmation.
5. **Explicit sharing:** friendship alone grants no calendar access. People
   choose who sees availability and who sees event details.

The fixed technical foundation is server-held data accessed through `http_api`,
following the approach of MiniFast and MiniHACCP. Their current implementations
must be inspected before describing something as reusable.

The current task creates documentation in the existing independent `minicalendar`
repository. It is already registered in the [workspace manifest](../../repos.json)
and excluded from the parent repository by its [ignore rules](../../.gitignore).
There is no need to recreate or register it again.

## Purpose and success criteria

The documentation should let the next planning session determine a complete first
release and turn it into an implementation specification. It should explain:

- What one person can do before inviting anyone else.
- How friends and groups go from uncertain availability to an agreed plan.
- Which information participants can see, and how they withdraw access.
- What already exists in the platform, what needs adaptation, and what is new.
- Which calendar, notification, and integration questions affect release scope.

The product hypothesis is an approachable calendar that makes shared planning
useful without requiring people to expose their private schedules. Demand,
willingness to pay, and a sustainable acquisition channel are not established by
the presence of comparison products.

## Audiences and example journeys

### Organising a personal week

1. Add appointments, an all-day commitment, and time reserved for a personal
   activity.
2. Review the week and upcoming events on a larger screen.
3. Check today's plans and change an event from a phone browser.
4. Optionally mark periods available for social plans and choose an audience.

Success means the calendar is useful without friends, groups, or an external
calendar connection. An empty period remains unknown unless the person explicitly
declares availability; the interface can separately show recorded conflicts.

### Arranging an evening with friends

1. Send and accept a friend invitation; personal calendars remain private.
2. Share selected availability, or answer a plan's proposed times without opening
   the rest of the calendar.
3. Suggest two or three evenings and collect individual responses.
4. Choose one time, confirm the event, and make each attendee's response visible
   to the appropriate participants.
5. If the time changes, communicate the change and obtain a current attendance
   response where needed.

Success means people can reach an agreed plan through the mobile web app while
controlling what they disclose. A positive availability response does not itself
mean they have accepted the final event.

### Scheduling a band rehearsal or gig

1. Create a private band group and invite its members.
2. Members share relevant available/unavailable periods or answer candidate times.
3. The organiser compares responses and confirms a rehearsal. A gig with a fixed
   date can go directly to an event invitation rather than requiring a poll.
4. Members see the upcoming event, its location, and their attendance status.
5. A changed rehearsal, cancelled gig, or unanswered invitation remains visible
   and understandable. Recurring rehearsals require explicit recurrence rules.

Success means the group has one understandable schedule. Booking rooms, bringing
equipment, and arranging transport are compatible later responsibilities;
setlists, ticketing, payments, and venue management are separate product areas.

## Cues from existing workspace research

The [app opportunities document](../../docs/app-opportunities.md) supplies adjacent
ideas rather than an automatic feature backlog:

| Existing idea | Relevance to MiniCalendar |
| --- | --- |
| Calendar with responsibilities | Later assignments for collecting, bringing, booking, or arranging cover, with acceptance rather than assumed commitment. |
| Group trips and weekends | Another small-group scheduling example; itineraries, bookings, and packing lists need separate justification. |
| Realistic weekly planning | Personal usefulness and a clear view of time already committed; a task-estimation system is not assumed. |
| Planning around rotating shifts | Availability can depend on repeating patterns and exceptions. Shift-rota generation remains a possible extension. |
| Learning and practice plans | Personal practice sessions and group rehearsals fit the calendar; learning-progress tracking is separate. |
| Shared resource booking | A possible later direction for rooms or studios; resource reservations and booking guarantees are distinct from inviting people. |

The portfolio's approachable, affordable-product philosophy is useful context.
`minicalendar` does not settle public naming, the charging model, or target markets.

## Boundaries and evidence standard

The initial stage produced this brief, [research findings](research.md), and the
[product plan](product-plan.md), plus the repository overview. The subsequent
[feature proposal](features.md) and [browser mockups](mockups/README.md) develop
recommendations for review using fictional in-memory data. Production application
code, schemas, exact API contracts, hosting, billing, and app-store releases
remain later work.

Use primary sources: current local implementation, platform contracts, official
product documentation, provider documentation, and calendar standards. Cite facts
near their claims and record inspection dates. Distinguish implemented code,
adaptable patterns, and new work; source inspection does not prove deployment or
passing runtime tests.

Label recommendations separately from the five confirmed choices. Online-first
operation and manual entry are initial recommendations. Pricing, branding,
anonymous participation, notification channels, detailed recurrence scope, and
release timing remain unresolved. Researching an integration does not promise
provider parity or a particular implementation date.

Use a small number of prospective personal users, friend groups, and bands to
test the three journeys. Observe where they fall back to messages, whether manual
availability remains accurate, and whether they understand each sharing choice.
Record these as proposed validation activities, not completed user research.
