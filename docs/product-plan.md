# MiniCalendar product plan

Date: 6 November 2026. Status: initial feature and delivery proposal. The five
confirmed choices are recorded in the [research brief](research-brief.md);
implementation evidence and external references are in [research](research.md).
Everything described below is planned, not an implemented MiniCalendar feature.

The subsequent [feature recommendations](features.md) propose a more concrete
first web release, including provisional answers for recurrence and notifications.
[Interactive mockups](mockups/README.md) explore the screens with fictional data;
they do not implement the backend or establish approved release scope.

## Product intent

Provide a useful personal calendar and a clear way for friends and small groups
to agree plans. People should be able to share the availability needed for a
decision without exposing unrelated appointments. Bands arranging rehearsals or
gigs use the same foundation as friends arranging an evening together.

The central collaborative journey is:

**Propose times → collect responses → choose a time → confirm the event → respond
to attendance invitations → communicate changes.**

An event with an already fixed time can enter at confirmation/invitation. An
individual can use the calendar without entering this collaborative journey.

## Proposed initial capabilities

| Area | Proposed behaviour |
| --- | --- |
| Personal calendar | Create, edit, and cancel timed or all-day events; review calendar and upcoming-event views; use the core workflows on desktop and mobile browsers. |
| Connections | Send, accept, decline, or withdraw friend invitations; remove a connection. Connecting does not reveal either person's calendar. |
| Private groups | Invite members into a named planning context, such as a band or friend group; distinguish organisers from participants and support leaving/removal. |
| Sharing | Choose the audience and whether it can see availability or event details. Show what is shared and allow withdrawal. |
| Availability | Enter available/unavailable periods and inspect permitted conflicts in a bounded period. Preserve unknown time as a separate state. |
| Proposals | Suggest candidate dates/times and collect each invitee's yes/maybe/no response, with no response kept distinct. Compare responses without claiming agreement automatically. |
| Confirmed events | Select one proposed time or create a fixed-time event directly; invite attendees, record attendance responses, and show upcoming plans. |
| Changes | Make rescheduling and cancellation visible; identify attendance responses that need reconsidering after a material change. |

Recurrence and the minimum invitation/reminder delivery experience are required
design topics before setting release scope. They are not assumed to exist merely
because MiniFast has schedule tables or `http_api` has account email delivery.
The research document explains these gaps.

### Keep availability and commitment separate

Declared availability means a person has chosen to say that a period could work.
Declared unavailability means they have said it cannot. A recorded calendar
conflict is evidence of an overlapping commitment, subject to the event's eventual
busy/free semantics and the viewer's permission. Unknown time means there is not
enough shared information to decide.

Show declared preferences and conflicts distinctly when they disagree; do not
silently treat an explicit answer as permission to move another appointment. The
first implementation specification must settle overlap and precedence rules.

A candidate-time response applies to that proposal. An attendance response
applies to the confirmed event. Choosing a popular time must not silently book
every person who said it might work. Missing responses are neither acceptance
nor refusal. Suggestions can show a useful overlap without claiming that a person
whose calendar is empty is free.

## Conceptual relationships and permissions

These are domain distinctions, not a table schema or a requirement for one table
per concept.

| Concept | Responsibility |
| --- | --- |
| Account/person | Identifies the signed-in participant; the authenticated session determines the acting account. |
| Calendar | Organises events with an owner and explicit access rules. Personal content is private initially. |
| Friendship | An accepted connection between people; it is not a permission to read calendars. |
| Group and membership | A persistent context for shared planning with roles and membership lifecycle; it does not grant access to members' personal schedules. |
| Sharing permission | Records the audience, scope, and detail level the owner has chosen to reveal. |
| Availability declaration | A person's available/unavailable interval, separate from calendar events and visible only to its chosen audience. |
| Proposal and candidate time | A plan under discussion and its possible dates/times. |
| Candidate response | One participant's answer about one candidate time. |
| Event and attendance response | A scheduled plan and each invitee's current commitment to it. |
| Recurrence series and occurrence | Repeated intent and an individual instance, including a changed or cancelled occurrence when recurrence is introduced. |

### Sharing rules to preserve

- Calendar access requires an explicit permission; adding a friend is insufficient.
  An event invitation reveals the necessary details of that event, not the rest
  of its organiser's calendar.
- Availability-only access must not return event titles, locations, notes, or
  attendee lists. Enforce this in server responses, not just by hiding UI fields.
- A group must explain which shared content joining grants access to. Joining
  does not publish the member's personal calendar to the group.
- Removing a sharing permission or leaving a group removes access supplied by
  that permission or membership. Unrelated permissions must be evaluated
  separately; the UI should make any remaining access understandable.
- Participants control their own availability and responses. An organiser's
  authority to manage an event is distinct from authority to answer for others.
- Invite expiry, revocation, declined/unanswered invitations, and group removal
  need defined outcomes. The eventual specification must also settle blocking,
  last-organiser departure, and the visibility of historical shared events.

Use explicit, understandable sharing summaries in the future UI. The research
should validate whether people can predict what a particular friend or group can
see before enabling a permission.

## Architecture and future interfaces

Follow the inspected application/platform boundary described in
[research](research.md). MiniCalendar owns its MySQL schema, migrations, scoped
views and stored procedures, business rules, grants, client applications, and
deployment configuration. `http_api` supplies the shared runtime and
authentication contracts. Use a separate MiniCalendar application configuration
and process; groups are application data, not separate runtime projects.

The planned clients are Svelte/Vite web, then SwiftUI iOS and Kotlin/Jetpack
Compose Android, following the existing MiniFast examples. Adopt the current
session/CSRF lifecycle and an application-specific cookie such as
`minicalendar-session`. The existing auth generator and onboarding scripts require
coordinated changes before a new app can use them; documentation creation does not
perform that onboarding.

The subsequent build specification should define these API capabilities:

- Bounded, authorised calendar/event reads and availability comparisons.
- Event creation, editing, cancellation, and eventually recurrence exceptions.
- Friend/group invitations, membership changes, and sharing permissions.
- Availability declarations, proposals, candidate responses, confirmation, and
  attendance responses.

Specify exact schemas, names, payloads, date-range limits, and transactions during
that work. Use the existing SQL exposure and database permission conventions;
derive identity from the authenticated session. Version-check editable resources
and preserve independent participant responses. A whole calendar should not be
one edit lock shared by unrelated responses.

Recommend online-first writes initially. A concurrent edit should preserve the
user's draft and offer reconciliation. A lost response may hide a committed write;
do not automatically replay it. Offline editing and safe mutation reconciliation
need their own design, not just a local queue.

## Delivery stages

| Stage | Deliverable and exit evidence |
| --- | --- |
| 1. Personal calendar and permissions foundation | Establish app/database/auth integration, timed/all-day events, responsive calendar/agenda views, and server-enforced ownership/sharing rules. Demonstrate a useful personal week and prove that another account cannot read private events. |
| 2. Shared planning | Add connections, private groups, explicit availability sharing, proposed times, individual responses, and confirmed/cancelled events. Demonstrate a complete friend or band workflow from a mobile browser, including invitations and changes. |
| 3. Native clients and notification improvements | Deliver dedicated iOS and Android experiences against the same contracts. Select mobile notification/device integration work based on the agreed reminder experience and validate it on actual target platforms. |
| 4. External connections and selected extensions | Implement a chosen calendar connection after resolving direction, permissions, freshness, and revocation. Evaluate event responsibilities and other extensions using observed need. |

Stages 1 and 2 together describe the proposed first collaborative product. Stage 1
alone can support personal-use trials. No release date, app-store readiness, or
full native/web feature parity is implied by this sequence.

Before fixing that first release, settle:

- **Recurrence:** the supported patterns, time-zone behaviour, and editing or
  cancellation of one occurrence versus a series. Weekly/fortnightly rehearsals
  are a useful starting case to evaluate; the detailed subset remains open.
- **Invitations and reminders:** how someone receives a friend/group/event invite,
  learns that a time changed, and sees an unanswered request. Compare in-app
  activity, email, and browser notifications; native push is a later channel.
  Do not postpone a workable invitation/change experience until native apps exist.
- **Participation:** signed-in participants are the planning default. Evaluate
  anonymous or account-light responses separately, including what an invite link
  reveals and how it can be withdrawn.

### Later candidates

Event responsibilities are the closest extension from the opportunities document:
who books the room, brings equipment, or arranges transport, with acceptance and
cover requests. They remain distinct from attendance.

Other candidates include repeating availability/shift patterns, trip planning,
personal practice scheduling, and room/resource booking. A resource reservation
may require guaranteed exclusivity, which an ordinary shared event does not
provide. Band repertoire, ticketing, payments, chat, and broader project/task
management are not initial feature commitments.

For external calendars, compare simple event export/add-to-calendar, read-only
availability or event import, and two-way synchronisation separately. Device-only
calendar access does not itself make those events available to the web app or
other members. Provider capabilities and permissions differ; see
[integration research](research.md).

## Future acceptance scenarios

These are inputs to the later implementation/test specification, not tests already
run or evidence that MiniCalendar works.

| Scenario | Expected outcome |
| --- | --- |
| Personal use | A person records and reviews their week without inviting anyone or connecting an external calendar. |
| Mobile web planning | Friends complete invitation, availability response, confirmation, and attendance response from phone browsers. |
| Private by default | Accepting a friendship or joining a group does not expose personal events or availability without the relevant permission. |
| Availability-only reader | API results reveal only the authorised scheduling information, with no private title, notes, location, or attendee metadata. |
| Access withdrawal | Revoked permissions stop further access through that grant; leaving/removal from a group stops group-derived access while unrelated personal events remain intact. |
| Unknown availability | Empty calendars, missing responses, and later stale imports are not presented as confirmed availability or attendance. |
| Independent replies | Two members responding concurrently retain their own answers without overwriting each other. |
| Fixed-time gig | An organiser invites people to an already dated event without creating an artificial poll. |
| Changed or cancelled event | Participants can identify the current event state and whether their attendance response needs renewing. |
| Daylight-saving change | A recurring Europe/London rehearsal intended for 19:00 remains at 19:00 local time across clock changes. Gap/fold times have an explicitly tested policy. |
| All-day and overnight events | Date-only events retain their dates in another time zone; an overnight gig appears consistently across the date boundary; adjacent timed events follow the chosen end-boundary semantics. |
| Recurrence exception | Editing or cancelling one occurrence affects that occurrence without silently changing the remaining series. |
| Concurrent or uncertain save | Stale edits preserve drafts and report conflicts; a lost response does not trigger blind replay or falsely imply the save failed. |
| Reminder correctness | Rescheduling/cancellation suppresses obsolete pending reminders; delivery retries and preferences follow the selected channel contract. |

## Decisions still open

The next implementation-planning pass must choose exact recurrence scope,
availability overlap rules, group/event permissions, invitation lifecycle,
material-change handling, notification channels, and anonymous participation.
It must translate the capabilities above into concrete data/API contracts and
operational requirements, including backup/restore and reminder failure visibility.

Pricing, public branding, first target markets, and release timing are product
decisions still to be made. External provider order and sync direction remain
open. Online-first operation, manual entry, and signed-in participation are
recommendations for planning, not additional user-confirmed requirements.

Validate the proposed journeys with prospective users before expanding scope.
Particularly test whether ongoing availability is kept current, whether people
understand the sharing levels, and whether the workflow reduces repeated chasing.
