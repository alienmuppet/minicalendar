# MiniCalendar feature recommendations

Date: **6 November 2026**. Status: concrete recommendations for discussion, not an
approved implementation specification. The five choices in the
[research brief](research-brief.md) remain fixed: personal plus shared use; web
first followed by dedicated iOS and Android apps; external calendars later;
ongoing availability and candidate-time responses; explicit sharing with no
calendar access granted by friendship alone. All clients use `http_api`.

The recommendation is to make the first web release a complete, modest calendar
and planning product. Someone should be able to organise their week alone, then
invite friends and finish a shared plan without needing an external calendar or
a native app. The main promise is: **keep your own plans, share what helps, and
agree a time together**.

The [research findings](research.md) explain the evidence and platform gaps.
The [product plan](product-plan.md) remains the broader roadmap. This document
adds specific feature and interaction recommendations, including provisional
answers to its open recurrence and notification questions. No prospective-user
testing has been performed, and no pricing or market-demand conclusion is implied.

## Recommended first web release

These are ranked by the value they bring to the complete experience, not the
order in which database tables should be built. All nine belong in the proposed
first public web release; earlier private trials can exercise smaller portions.

| Rank | Feature | Recommended behaviour | Benefit |
| --- | --- | --- | --- |
| 1 | A useful personal calendar | Timed, all-day and overnight events; title, location, notes and busy/free setting; create, edit, cancel and duplicate. Week, simple month and agenda views with a jump-to-date control. | Useful before anyone else joins; accommodates ordinary appointments and personal practice. |
| 2 | Clear privacy and sharing | Private personal calendar initially. Explicit per-person or per-group grants for availability only or event details. A persistent summary states who can see each item. | People can coordinate without publishing unrelated appointments. |
| 3 | Declared availability | Mark available or unavailable periods, including simple weekly/fortnightly repeats. Choose an audience; display recorded conflicts separately. | Answers “when could we meet?” without requiring a poll for every idea. |
| 4 | Plans with candidate times | Pick people or a group, suggest two or more options, collect yes/maybe/no responses, show unanswered people, and choose a final time. | Replaces scattered replies with one understandable decision. |
| 5 | Confirmed events and attendance | Invite people directly to a fixed-time event or confirm a proposal. Record going/maybe/not going separately from candidate responses. | A popular time becomes a clear plan without assuming attendance. |
| 6 | Friends and private groups | Invite and accept connections; create a band or friend group; manage members and roles; leave or remove access. No public directory or contact-book upload initially. | Supports both occasional plans and recurring groups without turning into a social feed. |
| 7 | Changes people notice | An action inbox plus email invitations, confirmations, material changes and cancellations; optional event reminders. | A plan remains usable when someone is away from the app. |
| 8 | Simple recurrence | Weekly and fortnightly patterns, an optional end date, and changes/cancellation to one occurrence. A clear way to stop future occurrences. | Covers recurring rehearsals and regular personal commitments. |
| 9 | Dependable everyday operation | Responsive phone workflows, accessible controls, account recovery, visible save/error states, draft-preserving conflict handling and basic title/location search over permitted events. | Reduces the friction that otherwise sends people back to messages. |

Recommend one personal calendar per account initially, plus one shared calendar
per group. Invitations place the same shared event in each participant's view;
they do not create independent copies that can drift apart. Multiple personal
calendars, elaborate colour/category systems and custom fields can follow if
people need them. A small set of colours should identify calendars, not encode
attendance or privacy by colour alone.

The first release should use signed-in participants and online writes. Retain a
draft after a recoverable failure, clearly explain uncertain saves, and never
pretend offline edits have reached others. Guest responses and offline mutation
sync remain later decisions. Dedicated mobile apps remain planned; mobile web
makes the initial release usable while those clients are built.

## How sharing, availability and agreement should work

### Small, understandable roles

| Role or relationship | Recommended authority |
| --- | --- |
| Personal-calendar owner | Edit their own events and availability; grant and withdraw access. |
| Friend | Invite the person to plans; read only information explicitly shared with them. |
| Group owner | Manage the group and organisers; transfer ownership before leaving or close the group. |
| Group organiser | Manage group plans, events and membership; cannot edit members' personal calendars or answer for them. |
| Group member | Read the group's calendar, propose plans, and manage their own availability and responses. |
| Event invitee | Read and respond to that event; the invitation reveals no other calendar content. |

Recommend showing all group-calendar events to current group members, with the
attendance list selecting who is actually invited. Explain this before someone
posts an event. A plan intended for a subset should be a separate private plan
with selected invitees, rather than silently disappearing from a group calendar.
Group membership never shares a member's personal schedule back to the group.

Use two simple calendar-sharing choices: **Availability only** and **Event
details**. Event details means read access, not permission to edit. Availability
declarations have their own audience so someone can share “Tuesday evenings are
usually good” without sharing their calendar. A private event can still contribute
an anonymous busy interval where the owner has explicitly shared availability.

Before saving a permission, show a plain preview: “Sam will see busy times and
the availability you share with Sam. Sam will not see appointment names.” Provide
a **See what Sam sees** preview and a **Manage access** list. Previewing privacy
is a useful interface feature; actual enforcement must also happen on the server.

Removing a friend should offer to remove direct sharing grants in the same flow,
with the safe default selected. Explain any remaining shared-group access.
Removing a group member withdraws group access, while separately granted personal
access must be shown and managed explicitly. A block should prevent new direct
invitations and direct access; any common-group implications need clear treatment
before implementation. Revocation cannot erase information already exported or
remembered by another person.

### Never turn missing information into a promise

| What the app knows | Recommended presentation |
| --- | --- |
| Explicit available interval | “Available”, with its shared audience visible to the owner. |
| Explicit unavailable interval | “Unavailable”; the reason is optional and private unless deliberately shared. |
| Busy event overlaps | “Busy”; reveal event details only if that viewer has permission. |
| No declaration or recorded conflict | “Unknown”, not “Free”. |
| Availability has not been shared | “Not shared”, not a supposedly empty calendar. |
| An available declaration overlaps a known conflict | Show the conflict and flag the disagreement; do not silently erase either record. |

For automatic suggestions, recommend using only intervals explicitly declared
available and free of known shared conflicts. Unknown or unshared periods should
remain possible candidate times, but should not be advertised as a mutual free
slot. The organiser can always ask people directly through a proposal.

When replying yes despite a personal conflict, warn the responding person and
allow a deliberate answer. Do not reveal that private conflict to the organiser
through a warning badge or tooltip. A candidate reply is about this proposed
activity; it neither changes the calendar nor grants ongoing access.

### One clear planning sequence

1. **Draft:** enter a title, invitees, a duration and candidate dates/times.
   Two or three options are a useful starting point, not a hard limit.
2. **Waiting for replies:** invitees answer yes/maybe/no for each option and may
   leave one short note. Show their last saved response and unanswered options.
3. **Choose a time:** the organiser compares counts and individual answers.
   Highlight the strongest response, but do not decide automatically or hide
   people who cannot attend. Choosing a time closes the alternative options.
4. **Confirm:** create the event once and send attendance invitations. Retain the
   proposal's responses as context; start attendance as awaiting reply.
5. **Attend or change:** participants answer going/maybe/not going. A later date,
   time, duration or venue change marks existing answers as needing confirmation.
   Minor note edits appear in activity without resetting attendance.

A fixed-date gig enters at step 4. Cancelling keeps a clearly labelled cancelled
record and notifies invitees. Closed proposals remain readable to their
participants, so the final time and decision are easy to understand.

## Provisional recurrence and notification choices

These recommendations make the proposed first release concrete. They need review
before becoming data/API contracts; neither is inherited ready-made from the
existing schedule tables or account-email worker.

### Repeat the common patterns first

Support weekly and fortnightly repeats at the same local time and named timezone,
with an optional end date. Apply the same limited pattern vocabulary to events
and availability declarations, while keeping them separate concepts. Changing a
device timezone changes the view, not the intended timezone of a band rehearsal.

Allow **This occurrence** edits and cancellation. Provide **Stop repeating after
this date**. For a wholesale change to a series' regular time, recommend stopping
the old series and creating a replacement in the first release; offer a guided
copy so users do not retype its details. This is a deliberate initial boundary.
Advanced “this and all following” editing, monthly rules, rotating shifts and
arbitrary recurrence expressions can follow.

Keep attendance attached to an occurrence. Creating a series sends one series
notice rather than an email for every future date; each occurrence still offers
its own attendance response. Do not assume someone has accepted every future
rehearsal. The prototype should test whether this is manageable or whether bulk
responses are important enough to expand scope.

Test all-day dates, overnight events, daylight-saving transitions and exception
identity before release. An ordinary weekly 19:00 rehearsal should stay at 19:00
local time. Gap/fold handling requires a defined policy and tests rather than a
UI-only assumption; see [calendar semantics research](research.md#calendar-semantics-to-design-deliberately).

### Reach people before native apps exist

Recommend **an in-app action inbox and email** for the first web release. Browser
push is optional later; native push belongs with the dedicated clients. The inbox
should remain the reliable place to find pending actions even when an email is
delayed, filtered or disabled.

| Trigger | Initial recommendation |
| --- | --- |
| Friend/group invitation | Email with a link to review and accept; show pending requests in the inbox. |
| Candidate-time request | One email when sent; the inbox shows the outstanding response. |
| Confirmed event | Email the final time and provide an attendance-response link. |
| Changed time/venue or cancellation | Notify affected invitees promptly and highlight the current state in the inbox. |
| Someone responds | Update the plan/inbox; avoid an email to everyone for every answer. |
| Unanswered requests | Organiser may remind only unanswered people, at most once per day; no repeated automatic chasing initially. |
| Upcoming event | Per-user opt-in email reminder: off, one hour, or one day before a saved/accepted event; one reminder per occurrence. |

Give users notification preferences without hiding pending requests. Keep private
notes out of emails and link to the authorised event page. Cancel or reschedule
pending reminders when an event changes. Delivery retries must not recreate an
event, reset a response or send obsolete reminder content. Operational delivery
failures need visibility; a sent email is not evidence someone read it.

## Screens and journeys to review

The mockups use fictional data and offer three ways to organise the same product.
They are alternatives for discussion, not three applications to build.

| Screen | Main question and action | Preview |
| --- | --- | --- |
| Calendar | “What does my week look like?” Review personal/shared events and add an event or availability. | [Week-first calendar](mockups/index.html?variant=week#calendar) |
| Agenda | “What is next, and what needs me?” Read an ordered list with clear dates and pending responses. | [Agenda-first calendar](mockups/index.html?variant=agenda#calendar) |
| Plan | “Which time works?” Compare candidates, answer, choose a time and inspect attendance. | [Planning workspace](mockups/index.html?variant=planner#plan) |
| People and sharing | “Who can see what?” Manage friends, sharing levels and privacy previews. | [People](mockups/index.html?variant=week#people) |
| Group | “What is happening with our band or friends?” See upcoming events, open plans and members. | [Group](mockups/index.html?variant=week#group) |

Event detail and quick creation can open as an accessible side panel on a larger
screen and a full-screen view on a phone. Settings should contain timezone,
notification preferences and account controls. The action inbox needs a consistent
entry from every screen; a badge should count unresolved actions rather than
every historical notification.

**First run:** create an account, confirm the suggested timezone, then land on an
empty personal calendar with **Add your first event**. After that save, offer
**Mark when you're available** and **Invite a friend** as optional next actions.
Explain sharing at the moment the user chooses an audience. Do not make an
external-calendar connection, group creation or friend invitation mandatory.

**Desktop:** default to the week view with a visible agenda alternative. Support
click-to-create, explicit date/time fields and keyboard interaction; drag editing
is an enhancement, not the only way to change an event. A planning view can show
people and candidate times together. Keep a readable list alternative for dense
comparisons and assistive technology.

**Phone browser:** default to a readable agenda or selected-day list, with a date
strip and access to month/week navigation. Make answering a proposal or attendance
invitation a short flow from its link. Use stacked candidate cards instead of
requiring horizontal scrolling across a desktop matrix. Keep save/cancel and the
current sharing audience visible while editing.

### Two example plans

**Friends:** Alex adds a private appointment and shares only availability with
Sam and Jo. Alex proposes dinner on Tuesday or Thursday. Sam says Thursday works;
Jo marks both options maybe and adds “I finish work at six.” Alex confirms
Thursday at 19:00. Both receive attendance invitations. Jo's eventual going
response is a new commitment, not something inferred from the earlier maybe.

**Band:** North Line has a group calendar and weekly Thursday practices. A member
marks one Thursday unavailable without publishing the reason. The organiser
proposes Tuesday and Wednesday for that occurrence, confirms Wednesday, and the
affected attendance replies need renewal. A separate fixed-date gig goes straight
to invitations. Booking the rehearsal room can be recorded in notes for now;
formal responsibility assignment is a later feature.

## Next additions and what to validate

| Priority after the initial web release | Reason to consider it |
| --- | --- |
| Dedicated iOS and Android clients | A confirmed delivery goal: quick daily access, native interactions and carefully selected push/device integration. |
| Event responsibilities | Who books, brings or drives, with explicit acceptance and requests for cover; keep this separate from attendance. |
| One external-calendar integration at a time | Reduce manual conflicts once the provider, permissions and freshness requirements are settled. Start with export/handoff or read-only access before two-way editing. |
| Low-friction guest responses | Test whether account creation prevents occasional participants from replying before accepting the extra identity/link-revocation work. |
| Richer recurrence and availability patterns | Add monthly rules, bulk occurrence responses or shift patterns when the simple patterns demonstrably fail real use. |

Further first-party evidence checked **6 November 2026**: Spond separates
[availability requests](https://help.spond.com/app/en/articles/158923-availability-requests)
from subsequent event invitations, supporting the distinction between availability
and attendance. Its [event tasks](https://help.spond.com/app/en/articles/140050-tasks-in-events)
can await acceptance or be offered to volunteers, a useful reference for later
responsibilities. Doodle's [group polls](https://doodle.com/en/product/polls/)
allow responses without an account, making participation friction worth testing.
These are comparison behaviours, not evidence that their exact defaults suit
MiniCalendar or a reason to overturn the agreed privacy model.

The mockups can test which home view makes sense, whether the planning steps are
clear, whether unknown time is understood, and whether people can predict what a
friend sees. Ask someone to find an upcoming rehearsal, answer an invitation and
withdraw a sharing permission without coaching. Compare desktop and phone widths.

A mockup cannot prove server permission enforcement, account isolation, email
delivery, durable concurrent replies, recurrence correctness or safe save recovery.
Those require implementation and behavioural tests. The visual prototypes may
show only selected controls/states; missing interactions are not working features.
Before implementation, use review feedback to settle recurrence boundaries,
notification defaults, role powers and the initial screen structure, then produce
the precise data/API and operational specification.
