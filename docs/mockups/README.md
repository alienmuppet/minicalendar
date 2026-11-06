# MiniCalendar interface concepts

Date: 6 November 2026. Three interactive layout options, using fictional people
and events. These are local review prototypes, not production application code.

## Open the mockups

From the `miniproject` workspace root:

```sh
./prototyping/minicalendar/start.sh
```

Open <http://127.0.0.1:5176/mockups/>. Keep the terminal open; stop with Ctrl+C.
The launcher needs Python 3 and serves this repository's `docs` directory.

For VS Code connected to the development machine remotely, forward **5176** in
the Ports panel and choose **Open in Browser**. Use the panel's forwarded address
if it assigns a different local port, appending `/mockups/`. A localhost link
refers to the computer running your browser, so forwarding is needed when that is
not the development machine.

Alternatively, open [index.html](index.html) directly in a browser. The file is
self-contained: no dependencies, network access, account, or backend is needed.
You can copy it to another computer for review. Editor previews may not run its
JavaScript. From the `minicalendar` repository, a standalone server command is:

```sh
python3 -m http.server 5176 --bind 127.0.0.1 --directory docs
```

## Compare the three layouts

The floating bottom bar is review tooling, not part of the proposed app. Switch
layouts there or with the left/right arrow keys outside editable controls. The
selected layout is stored in the URL. Switching layouts returns to its home view.

| Layout | Main difference | Useful question |
| --- | --- | --- |
| [Week](index.html?variant=week#calendar) | Side navigation, seven-day time grid, and an adjacent view of today's events and open plans. On phones, the grid becomes a selected-day agenda. | Is the familiar week grid the best starting point? |
| [Agenda](index.html?variant=agenda#calendar) | Top navigation, date strip, and a chronological list, with shared planning beside it. | Is an ordered list more useful day to day than seeing every hour? |
| [Planner](index.html?variant=planner#calendar) | Shared evening availability leads, with an open plan and upcoming personal events alongside. | Should agreeing plans be prominent enough to be the home screen? |

All three share one provisional blue, white, lilac and ochre visual vocabulary.
Calendar colour identifies context; text also identifies privacy and attendance.
The [design reference](DESIGN.md) records this first pass for continued review;
it does not establish a final public brand.

## Things to try

1. Open an event to see its time, audience and attendance. Reply to **Sunday
   rehearsal** and see the status change; cancel a sample event to see its state.
2. Use **New event**, add a timed event, and see it in the chosen week. The small
   creation form supports same-day timed events; all-day, overnight and recurrence
   remain proposed production features.
3. Open [Find a time](index.html?variant=week#plan). Change your candidate replies,
   add a time, and choose an option. The result shows attendance still pending;
   **View in calendar** goes to the new event. Reopening removes that sample event.
4. Compare the phone planning screen: candidate times become stacked sections
   with each person's response visible.
5. In Planner, change your sample availability cells. Other people's unshared
   periods remain labelled **Not shared**, rather than being assumed free.
6. Open [People](index.html?variant=week#people). Change what Maya can see between
   **Nothing**, **Availability only** and **Event details**. The preview shows the
   difference. **Stop sharing** removes access without removing the connection.
7. Accept Erin's connection request and see that no calendar access is granted.
   Search for a friend, including a name with no matches.
8. Open [My group](index.html?variant=week#group). See the band's upcoming events,
   reply to a rehearsal, and open the rehearsal-planning example.

The current example date is fixed at **Friday, 6 November 2026**; the first week
is 2–8 November. The planning examples cover 10–15 November. “Today” refers to
that fictional date whenever you open the mockup. The small sidebar month is
orientation only. Week arrows, the agenda date strip, and event creation operate
on the sample calendar.

## What this can and cannot demonstrate

The [feature proposal](../features.md) covers the recommended product. The mockup
implements selected interactions to make those recommendations easier to judge.
There is one active sample proposal, which can be explored as a dinner or band
rehearsal; it is not a multi-proposal management system.

All changes live in memory and reset when the page reloads. Invitations and
sharing edits are simulations; nobody is contacted. There is no production auth,
API, persistence, server-enforced permission model, reminder delivery, recurrence
engine, provider sync, or offline-write queue. The privacy preview demonstrates
the proposed experience, not an access-control security test. Opening a static
file offline does not establish offline support for the future application.

Month view, comprehensive search, account setup, notification inbox, recurring
events and production error recovery are described in the proposal but are not
implemented here. Choose the useful ideas, then implement them properly against
the application contracts after reviewing the feature scope.

## Browser captures and verification

These screenshots are browser renders of the local HTML, not generated design
images. Desktop viewport: 1440 × 1000; phone: 390 × 844. Full-page image heights
can exceed the viewport. The [browser review record](screenshots/review.json)
records viewport checks, exercised flows and actual browser errors/network calls.
Capture provenance is the accompanying review record and this local source file.

| View | Desktop | Phone |
| --- | --- | --- |
| Week | [View](screenshots/week-desktop.png) | [View](screenshots/week-mobile.png) |
| Agenda | [View](screenshots/agenda-desktop.png) | [View](screenshots/agenda-mobile.png) |
| Planner | [View](screenshots/planner-desktop.png) | [View](screenshots/planner-mobile.png) |
| Find a time | [View](screenshots/plan-desktop.png) | [View](screenshots/plan-mobile.png) |
| People and sharing | [View](screenshots/people-desktop.png) | [View](screenshots/people-mobile.png) |
| My group | [View](screenshots/group-desktop.png) | [View](screenshots/group-mobile.png) |

## Questions to ponder

- Which home view feels like somewhere you would start each day?
- Is the distinction between sharing availability and answering a plan clear?
- Is choosing a time and then confirming attendance helpful, or too much work?
- Can you tell what each friend can see, and how to withdraw it?
- Which proposed features would you want immediately, and which could wait?
- What would make this worthwhile before connecting an existing calendar?
