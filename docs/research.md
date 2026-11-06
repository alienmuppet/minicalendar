# MiniCalendar research

Research date: **6 November 2026**. External sources below were accessed on that
date. This is an evidence record for the [research brief](research-brief.md) and
[product plan](product-plan.md), not an implementation or release-readiness claim.

## Direction and evidence boundaries

The agreed direction is a personal and shared calendar for friends and small
groups. Bands, gigs and practices are important examples, not the exclusive
audience. The Svelte web app comes first, followed by dedicated iOS and Android
apps, all using `http_api`. External calendars are researched now and implemented
later. Both ongoing availability sharing and responses to proposed times belong
in the product direction. Sharing is explicit: becoming friends grants no access
to a calendar. These are user decisions, recorded in the
[research brief](research-brief.md), rather than conclusions from competitors.

Local evidence was inspected at these revisions:

| Repository | HEAD | Working-tree qualification |
| --- | --- | --- |
| `minicalendar` | `0e84b49` | Only the original README and project brief existed before this documentation work. |
| `minifast` | `daaa3ad` | Clean during inspection. |
| `minihaccp` | `5de27f7` | Existing changes in monitoring, plan UI, database, tests and documentation; findings describe the inspected working tree, not exclusively this commit. |
| `http_api` | `35b41b38` | Clean during inspection. |

Relative links into sibling repositories require the normal workspace checkout.
They identify inspected sources, not immutable remote snapshots. Runtime builds,
database deployments and signed mobile applications were not validated for this
research. Recheck affected contracts when implementation begins.

The [workspace README](../../README.md), [manifest](../../repos.json) and
[ignore rules](../../.gitignore) already place `minicalendar` in an independent
product repository. Its manifest status is `planned`. No new repository,
workspace registration or runtime provisioning is needed for this docs pass.

## Existing product ideas

The [app opportunities notes](../../docs/app-opportunities.md) propose a calendar
with responsibilities: who collects, brings, books or does something, with
acceptance and cover requests. They also discuss personal planning around shifts,
group trips, shared resources and leave/availability planning. These are product
hypotheses, not evidence of demand for minicalendar.

The direct connection is coordinating a plan and its participants. A rehearsal
could later include someone booking the room or bringing equipment. Resource
booking, employer leave policies and broad task management add different rules;
the current plan treats them as possible extensions rather than initial scope.
The same notes favour quick initial value, browser access for occasional users,
server-held records and understandable export. Those principles fit a personal
calendar that becomes more useful when selectively shared.

## What can be reused from the workspace

Here, **implemented** means a capability exists in inspected source;
**adaptable pattern** means application-specific behaviour offers a useful
example; **new work** means minicalendar must design and implement it. None of
these labels means a feature has been deployed for minicalendar.

| Area | Classification | Evidence and consequence |
| --- | --- | --- |
| HTTP, static web serving, SQL REST and built-in account/auth flows | Implemented platform capability | The [database contract](../../http_api/docs/database_contracts.md) assigns transport, exposure enforcement and auth flows to `http_api`, and domain rules to each application. |
| Svelte browser client | Adaptable pattern | MiniFast's [project instructions](../../minifast/AGENTS.md) designate `ViteSvelte` as production-track; MiniHACCP also has a [Svelte client](../../minihaccp/ViteSvelte/README.md). Neither is a calendar frontend package. |
| Dedicated mobile clients | Adaptable pattern | MiniFast contains a [SwiftUI application](../../minifast/iOS/minifast/minifast/minifastApp.swift), [iOS API service](../../minifast/iOS/minifast/minifast/Services/APIService.swift) and [Android Compose client](../../minifast/Android/minifast/README.md). These establish the family approach, not automatic cross-platform feature parity. |
| Tenant-scoped reads and permission checks | Adaptable pattern | MiniHACCP's [role lookup](../../minihaccp/Database/haccp/tenancy/org_member_role_fn.sql), [permission helper](../../minihaccp/Database/haccp/tenancy/org_member_can_fn.sql) and [member view](../../minihaccp/Database/haccp/tenancy/organisation_member_api_v.sql) demonstrate application-owned access decisions. Calendar friendship and sharing need their own rules. |
| Invitations and membership | Adaptable pattern, requiring review | MiniHACCP implements [invitation creation](../../minihaccp/Database/haccp/tenancy/organisation_invitation_create_api_sp.sql) and [acceptance](../../minihaccp/Database/haccp/tenancy/organisation_invitation_accept_api_sp.sql). It is an organisation workflow, not a reusable social graph. |
| Optimistic editing | Implemented contract with app adoption work | The [shared contract](../../http_api/docs/optimistic_concurrency.md) carries `row_version` and `expected_version`; application transactions own enforcement. |
| Repeating schedules | Adaptable domain pattern | MiniFast's [schedule table](../../minifast/Database/schedule/schedule.sql) and [occurrence view](../../minifast/Database/schedule/schedule_occurrence_v.sql) represent its scheduling rules. They are not a general timezone-aware event engine. |
| Calendar events, sharing grants, availability and proposals | New work | The inspected minicalendar baseline is a documentation scaffold; the [product plan](product-plan.md) describes intended capabilities. |
| Calendar reminders, mobile push and offline mutation reconciliation | New work | Existing email and concurrency contracts have narrower purposes, detailed below; their presence does not supply these behaviours. |

### Runtime and database ownership

The current adapter supports MySQL. Minicalendar should own its schema, public
views/routines, business validation, seed data and deployment scripts, following
the [database contract](../../http_api/docs/database_contracts.md). The same
runtime binary supports separate app processes selected by project config;
[ADR-0001](../../http_api/docs/adr/0001-single-project-per-process.md) explicitly
chooses one project per process rather than routing several apps inside one.

Public SQL REST reads conventionally use `*_api_v`; mutations use `*_api_sp`
through `PUT`. Exposure manifests and database grants govern access. GET procedure
rowsets need a separately reviewed exact allowlist; naming a procedure with the
suffix alone does not expose it. Permission filtering belongs in server-side
application objects, not just the UI. See the
[API surface contract](../../http_api/docs/database_contracts.md#generic-sql-rest-contract).

The current account model has three per-app runtime logins—query, call and
auth—and two locked owners for business and credential objects. Grants go
directly to these accounts; runtime logins do not have base-table rights.
Minicalendar must follow this current five-account design, not older shared-role
examples. See [ADR-0011](../../http_api/docs/adr/0011-database-logins-and-owners.md).

Auth SQL now has a canonical source in
[`http_api/database/auth`](../../http_api/database/auth/README.md), with generated
copies in each application. The
[generator](../../http_api/scripts/generate_app_auth.py) currently lists only
MiniFast and MiniHACCP. The [shared-source test](../../http_api/testing/test_shared_database_sources.py),
[SQL wrapper](../../http_api/scripts/run_mysql_script.sh) and
[development-login provisioner](../../http_api/scripts/provision-dev-db-logins.sh)
also contain two-app assumptions. Adding minicalendar later requires coherent
onboarding of these tools and tests, not hand-copying generated auth files.

A distinct `minicalendar-session` cookie is a proposed application setting,
following the app-specific names in the
[MiniFast](../../http_api/config/projects/minifast/httpapi.ini) and
[MiniHACCP](../../http_api/config/projects/minihaccp/httpapi.ini) configurations.
No minicalendar runtime config or authentication provisioning is introduced by
this research.

Session handling is also an adaptation task. MiniFast's
[web session module](../../minifast/shared/auth-session.js),
[iOS service](../../minifast/iOS/minifast/minifast/Services/APIService.swift), and
[Android behaviour](../../minifast/Android/minifast/README.md), together with
[MiniHACCP's browser API module](../../minihaccp/ViteSvelte/src/lib/api.js), provide
examples of coordinated cookie/CSRF handling, server-directed renewal and explicit
uncertain session states. Preserve the current contract across clients rather
than copying an older fixed renewal interval or assuming failed requests imply
sign-out. These are application implementations, not a shared calendar client SDK.

### Invitations need adaptation, not copying

MiniHACCP stores an invitation token and queues a message containing its link.
Its creation procedure takes `invite_url_base` as an argument; the browser
supplies that value. Acceptance requires a logged-in account with a matching
email. These are observed behaviours in the
[creation](../../minihaccp/Database/haccp/tenancy/organisation_invitation_create_api_sp.sql),
[acceptance](../../minihaccp/Database/haccp/tenancy/organisation_invitation_accept_api_sp.sql)
and [browser](../../minihaccp/ViteSvelte/src/App.svelte) sources.

The [email-worker contract](../../http_api/docs/account_email_worker.md#application-invitations)
explicitly treats that invitation message as a plaintext exception, and records
token hashing/encryption as future per-app work. A calendar design should review
token generation, storage, expiry, revocation and trusted invitation-link origins
before adopting the pattern. This document does not settle their wire formats.
Friend requests, calendar access and group membership must remain distinct even
if their user interfaces share an invitation mechanism.

### Concurrency, notifications and recurrence limits

MiniFast and MiniHACCP implement versioned editing, with stale writes rejected
and client drafts preserved. The shared contract explicitly excludes a generic
edit coordinator, operation receipts and automatic mutation retry. A lost
response therefore does not establish whether a save committed. Calendar clients
must retain that distinction; an offline write queue would need additional
reconciliation design. See [shared optimistic editing](../../http_api/docs/optimistic_concurrency.md),
[MiniFast adoption](../../minifast/docs/optimistic_concurrency.md) and
[MiniHACCP adoption](../../minihaccp/docs/optimistic_concurrency.md).

The [account email worker](../../http_api/docs/account_email_worker.md) is a
separate process consuming committed jobs, with claiming, retry and terminal
states. Its [queue schema](../../http_api/database/auth/account_email_queue.sql)
and [worker](../../http_api/scripts/account_email_worker.py) accept defined
message kinds and reject unknown ones. Calendar invitations, rescheduling notices
and reminders are not available simply by inserting a new kind. The queue is a
possible delivery pattern; scheduling, payload policy, cancellation and delivery
channels remain calendar design work. Email, push and in-app notices are distinct
choices, still open in the [product plan](product-plan.md).

MiniFast schedules combine recurrence metadata with daily/weekly/monthly/yearly
children and generated occurrences. The inspected
[schedule](../../minifast/Database/schedule/schedule.sql),
[daily-time child](../../minifast/Database/schedule/schedule_daily_time.sql) and
[occurrence view](../../minifast/Database/schedule/schedule_occurrence_v.sql) do not
provide event timezone identity or per-occurrence exceptions. This is useful
domain modelling precedent, not a ready-made calendar recurrence implementation.
No general calendar recurrence, mobile-push or offline-sync subsystem was
established by the inspected runtime contracts and sources.

## Product comparisons

These first-party pages establish advertised behaviour. They do not establish
customer satisfaction, willingness to pay or an unmet market. The recommendations
below are our interpretation, not claims made by those products.

| Product | Observed behaviour | Relevance |
| --- | --- | --- |
| Howbout | Event details can be visible to all friends, selected close friends, or nobody; other friends can see a busy indication under the close-friends setting. Controls apply to events, synced calendars or defaults. [Privacy help](https://howbout.app/get-help/who-see-calendar/) | Availability disclosure and detail disclosure are different permissions. Its default shares details with friends; minicalendar's agreed default requires explicit access instead. |
| TimeTree | Shared calendars can be created on iOS, Android and web. [Creation help](https://support.timetreeapp.com/hc/en-us/articles/204121559-How-to-create-a-new-calendar) | A personal calendar plus named shared calendars is an understandable cross-platform model. |
| TimeTree | Mobile can display external device calendars; web cannot display those device calendars. [Combined-calendar help](https://support.timetreeapp.com/hc/en-us/articles/115000030881-View-multiple-calendars-at-the-same-time), updated 19 June 2026 | Device access does not by itself supply equivalent server or browser availability. |
| BandHelper | Separates unconfirmed events, member responses, candidate date/time options and final confirmation; supports rehearsal/show categories and reminders. [Scheduling tutorial](https://www.bandhelper.com/tutorials/scheduling_events.html) | Propose, respond, choose and confirm is a useful general workflow, including for bands. Alternative dates for one plan differ from a repeating series. |

Recommendation: validate a complete planning loop with friends and a band before
adding specialist band administration. Test whether participants understand what
others can see, whether they can answer quickly, and whether a chosen time stays
clear after changes. Comparing feature lists cannot answer those questions.

## Calendar semantics to design deliberately

[RFC 5545](https://datatracker.ietf.org/doc/html/rfc5545) defines iCalendar data,
not a hosted sync service. Relevant rules are:

- Date-only values are distinct from timed values; event starts are inclusive
  and ends are non-inclusive (§3.6.1).
- A timezone reference preserves local recurrence intent through offset changes;
  floating time has different meaning (§3.3.5, §3.8.5.3).
- Recurrence rules, inclusion/exclusion dates and occurrence identifiers support
  series and exceptions (§3.8.4.4, §3.8.5).
- Recurrence-generated invalid dates or nonexistent local times are skipped;
  explicitly supplied date-times have separate ambiguity/gap interpretation
  rules (§3.3.10 versus §3.3.5).

Implementation implications: distinguish all-day dates from instants, retain an
event's named timezone where needed, and separate a series from individual
occurrences. Test weekly local-time practices across daylight-saving changes,
overnight gigs, adjacent intervals and cancelled occurrences. Detailed supported
recurrence rules, editing semantics and the implementation library remain open;
do not claim full iCalendar compatibility from a few repeat controls.

The product also needs distinctions that a date/time format cannot decide:

| Concept | Intended meaning |
| --- | --- |
| Declared availability | A person explicitly shares times they are willing to consider. |
| Declared unavailability | A person explicitly says a period does not work, independently of recorded events. |
| Recorded conflict | A calendar event overlaps a candidate time under the product's chosen busy/free rules. |
| Unknown | There is insufficient shared or current information; absence of a conflict is not agreement. |
| Candidate response | A person's answer about one proposed option. |
| Attendance agreement | A response to the actual chosen event; being available is not a commitment to attend. |

These are proposed product semantics, carried into the
[product plan](product-plan.md), rather than a database schema. Friendship,
membership, access grants and event participation must likewise remain distinct.

## External calendars: separate capabilities

External-calendar implementation is deferred. Research should distinguish an
export or system-calendar handoff, device-calendar access, provider free/busy
queries, importing events and two-way synchronisation. Each has different
permission, freshness and update implications.

### Google Calendar

[Freebusy query](https://developers.google.com/workspace/calendar/api/v3/reference/freebusy/query)
returns busy intervals for requested calendars and accepts dedicated free/busy
OAuth scopes. This offers a possible conflict signal without copying event
descriptions. A failed or inaccessible calendar must not be interpreted as free.

[Incremental event sync](https://developers.google.com/workspace/calendar/api/guides/sync)
uses stored sync tokens, includes deletions, supports paginated changes and
requires a fresh full sync when a token becomes invalid (`410`).
[Change notifications](https://developers.google.com/workspace/calendar/api/guides/push)
use HTTPS webhook channels, require renewal and can be dropped. They signal
resource changes; they are not end-user event reminders. Importing events
therefore needs durable sync state and recovery, beyond making a calendar query.

### Apple calendars

[EventKit access](https://developer.apple.com/documentation/eventkit/accessing-the-event-store)
is access to the device event store. Apple's
[access-level explanation](https://developer.apple.com/videos/play/wwdc2023/10052/)
describes no access, write-only access and full access, with no read-only level;
reading events requires full access. EventKitUI can present a user-mediated event
editor without granting the app that broad access.

Implication: “add this event to Calendar” and “read my calendars to find
conflicts” are materially different features. A device integration is not proof
of a server-side iCloud connector or browser access to the same information.
Any later server-held projection needs explicit sharing and freshness design;
this research does not select an iCloud cloud-integration route.

### Android calendars

The [Calendar Provider](https://developer.android.com/identity/providers/calendar-provider)
supports access to calendars, events, attendees and reminders with appropriate
permissions. Calendar intents can send users to the calendar application for
common event operations without requesting those provider permissions.

Implication: a system-calendar handoff can be a smaller integration than reading
and uploading device calendar data. Neither automatically supplies provider
cloud access or a browser-visible conflict feed.

### Microsoft calendars

Microsoft Graph's [getSchedule](https://learn.microsoft.com/en-us/graph/api/calendar-getschedule?view=graph-rest-1.0)
provides free/busy information, but its delegated permission table excludes
personal Microsoft accounts. Work/school support must not be presented as
universal Outlook consumer support. Consumer event access and its permissions
need separate research if this integration is prioritised.

Recommendation: keep minicalendar-owned records authoritative for the initial
product. Later investigate export/system handoff and a bounded read-only conflict
connection before two-way editing. Record source and freshness when imported
data affects availability; unavailable or stale sources should remain visible
limitations rather than implying a person is free.

## Questions for implementation research

- Define the first recurrence subset and series/occurrence editing behaviour,
  using explicit daylight-saving and exception examples.
- Specify access grants, revocation and invitation handling, including how
  cached data and exported copies differ from future server access.
- Select reminder/update channels and their delivery/cancellation guarantees;
  do not infer them from the existing auth email worker.
- Decide guest participation, offline behaviour and external-provider order
  from actual participant needs. These are still open choices.
- Validate the personal-calendar and group-planning journeys before pricing,
  public branding or specialist extensions are settled.

These questions refine later implementation. They do not block creating the
documentation foundation or change the five confirmed product decisions.
