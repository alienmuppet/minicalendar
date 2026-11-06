---
name: MiniCalendar exploratory mockups
description: Preview-local capture of three calendar layout alternatives; no production visual identity or winning layout selected.
colors:
  ink: "#202c40"
  muted: "#59677b"
  blue: "#3156a8"
  blue-deep: "#203c79"
  blue-soft: "#e9effb"
  ground: "#f6f8fb"
  line: "#dce2eb"
  white: "#fff"
  green: "#23614c"
  green-soft: "#e6f2e9"
  purple: "#66439b"
  purple-soft: "#f0eafa"
  amber: "#805318"
  amber-soft: "#faf0db"
  red: "#a53d42"
  red-soft: "#fbeaec"
  focus-ring: "#6186ce"
  rail: "#edf1f8"
  nav-text: "#4c5e7a"
  nav-selected: "#dce6f8"
  nav-selected-text: "#23437d"
  nav-hover: "#e0e8f5"
  field-border: "#bdc8d8"
  neutral-chip: "#eff1f5"
  event-personal: "#e7eefb"
  event-personal-text: "#2e4a80"
  availability-busy: "#e8ecf4"
  availability-busy-text: "#4b5e80"
  availability-unknown-border: "#cbd2dd"
  privacy-panel: "#f1f4fa"
typography:
  headline:
    fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'
    fontSize: "28px"
    fontWeight: 650
    lineHeight: 1.2
    letterSpacing: "-.025em"
  headline-phone:
    fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'
    fontSize: "25px"
    fontWeight: 650
    lineHeight: 1.2
    letterSpacing: "-.025em"
  section-title:
    fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'
    fontSize: "18px"
    lineHeight: 1.35
    letterSpacing: "-.015em"
  body:
    fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'
    fontSize: "14px"
    lineHeight: 1.5
  button:
    fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'
    fontSize: "14px"
    fontWeight: 550
    lineHeight: 1.5
  field:
    fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'
    fontSize: "12px"
    fontWeight: 550
    lineHeight: 1.5
  small:
    fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'
    fontSize: "12px"
    lineHeight: 1.5
  chip:
    fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'
    fontSize: "11px"
    fontWeight: 600
    lineHeight: 1.5
  calendar-title:
    fontFamily: '-apple-system, BlinkMacSystemFont, "Segoe UI", sans-serif'
    fontSize: "11px"
    fontWeight: 600
    lineHeight: 1.15
rounded:
  chip: "5px"
  cell: "6px"
  field: "7px"
  control: "8px"
  day: "10px"
  panel: "12px"
  dialog: "16px"
spacing:
  gap-xs: "5px"
  gap-sm: "8px"
  gap-md: "12px"
  gap-lg: "14px"
  inset-sm: "16px"
  inset-md: "20px"
  inset-panel: "22px"
  inset-lg: "24px"
  page-top: "28px"
  column: "30px"
components:
  button-primary:
    backgroundColor: "{colors.blue}"
    textColor: "{colors.white}"
    typography: "{typography.button}"
    rounded: "{rounded.control}"
    padding: "8px 14px"
  button-primary-hover:
    backgroundColor: "{colors.blue-deep}"
  button-secondary:
    backgroundColor: "{colors.white}"
    textColor: "{colors.ink}"
    typography: "{typography.button}"
    rounded: "{rounded.control}"
    padding: "8px 14px"
  button-secondary-hover:
    backgroundColor: "{colors.ground}"
  button-quiet:
    backgroundColor: "transparent"
    textColor: "{colors.ink}"
    typography: "{typography.button}"
    rounded: "{rounded.control}"
    padding: "8px 14px"
  button-quiet-hover:
    backgroundColor: "{colors.blue-soft}"
  field-text:
    backgroundColor: "{colors.white}"
    textColor: "{colors.ink}"
    typography: "{typography.field}"
    rounded: "{rounded.field}"
    padding: "10px 11px"
  nav-item:
    backgroundColor: "transparent"
    textColor: "{colors.nav-text}"
    rounded: "{rounded.control}"
    padding: "11px 12px"
  nav-item-selected:
    backgroundColor: "{colors.nav-selected}"
    textColor: "{colors.nav-selected-text}"
  chip-blue:
    backgroundColor: "{colors.blue-soft}"
    textColor: "{colors.blue-deep}"
    typography: "{typography.chip}"
    rounded: "{rounded.chip}"
    padding: "3px 7px"
  chip-green:
    backgroundColor: "{colors.green-soft}"
    textColor: "{colors.green}"
    typography: "{typography.chip}"
    rounded: "{rounded.chip}"
    padding: "3px 7px"
  chip-amber:
    backgroundColor: "{colors.amber-soft}"
    textColor: "{colors.amber}"
    typography: "{typography.chip}"
    rounded: "{rounded.chip}"
    padding: "3px 7px"
  privacy-panel:
    backgroundColor: "{colors.privacy-panel}"
    rounded: "{rounded.panel}"
    padding: "23px"
  calendar-event:
    backgroundColor: "{colors.event-personal}"
    textColor: "{colors.event-personal-text}"
    rounded: "{rounded.cell}"
    padding: "4px 6px"
  availability-available:
    backgroundColor: "{colors.green-soft}"
    textColor: "{colors.green}"
    rounded: "{rounded.cell}"
    height: "53px"
  availability-busy:
    backgroundColor: "{colors.availability-busy}"
    textColor: "{colors.availability-busy-text}"
    rounded: "{rounded.cell}"
    height: "53px"
  availability-unknown:
    backgroundColor: "{colors.white}"
    textColor: "{colors.muted}"
    rounded: "{rounded.cell}"
    height: "53px"
---

# Design System: MiniCalendar exploratory mockups

## Overview

This is a **preview-local implementation record**, extracted from
[index.html](index.html) on 6 November 2026 and checked against the saved week
desktop screenshot. Frontmatter tokens describe this prototype only; the HTML
remains the implemented source. No winning layout, production palette, public
brand, logo or native-client design has been selected.

The current surface uses a cool pale navigation shell, white working space,
blue actions, lilac group events and ochre friend events. Compact system type,
date anchors and thin rules make dense schedules readable. Week, Agenda and
Planner are alternative structures with shared sample data and vocabulary.
Their provisional direction is recorded in the
[surface brief](../../.impeccable/surfaces/docs-mockups-index-html.md); durable
product constraints remain in [PRODUCT.md](../../PRODUCT.md).

**Key Characteristics:**

- Three unselected layouts for the same personal and shared planning product.
- Date-led working surfaces, thin dividers and compact system typography.
- Colour identifies context alongside explicit words for availability and state.
- Self-contained HTML, CSS and inline SVG with fictional, in-memory data.

## Colors

Frontmatter preserves the implemented colour values. The names describe local
roles rather than an approved brand palette; no additional tonal scale is implied.

### Primary

Blue identifies primary actions, selected dates, links and input carets. Blue-deep
supports action hover and selected text. Blue-soft supplies supporting surfaces
and status chips. Personal calendar events use a separate pale-blue pair.

### Secondary

Purple and purple-soft distinguish the band/group context. Amber and amber-soft
distinguish friend events and also appear with explicit “Maybe” or pending labels.
Context colours do not replace the written state.

### Tertiary

Green and green-soft mark declared availability, positive responses and success
messages. Red and red-soft accompany decline/error/destructive-action wording.
These are captured preview assignments, not a complete future status taxonomy.

### Neutral

White is the main working surface; ground and rail separate the page shell.
Ink, muted and line support text hierarchy and dividers. Navigation has dedicated
selected/hover pairs. A busy availability cell uses a cool filled pair; unknown
cells are white with a dashed border. The keyboard focus ring is shared across
buttons, links and form controls.

## Typography

One system sans-serif stack serves the entire prototype. No font download,
display-face pairing or custom font asset is present. The frontmatter contains
the main observed roles; supporting sizes remain in the source.

Page titles use a medium-heavy, tightly tracked headline. Section titles are
smaller and slightly tracked; body copy uses a relaxed line height. Most helper
text and controls are compact. Paragraphs are limited to 70 characters of width.
Dates and times use tabular numerals where the source applies them.

Calendar event titles are intentionally smaller than agenda event links; the
wide-screen rule increases event type. Short grid events truncate a single-line
title and open the full detail dialog. This is a density tradeoff in the preview,
not permission to hide essential event information from every view.

## Layout

Week and Planner use a 208px navigation rail. The normal main inset is
28px 30px with 100px bottom clearance for comparison controls. Week places a
seven-day grid beside a 230px upcoming/action column with a 25px gap; the grid has
a 45px time gutter and a 526px time surface representing the sample 08:00–22:00.
The current-time marker is illustrative, not a live clock.

Agenda moves navigation into a horizontal bar. Its main area centres around an
1170px reference width and places a 300px aside beside date-grouped events.
Planner uses a shared-evening matrix and a 300px upcoming column. The dedicated
plan, people and group screens use side columns of 260px, 280px and 260px
respectively. Forms normally use a 2:1:1 grid with 14px gaps.

| Observed breakpoint | Behaviour |
| --- | --- |
| At least 1600px | Main inset becomes 36px 40px; Week's aside grows to 270px, its gap to 35px and time grid to 600px; event type grows. |
| At most 1200px | Rail narrows to 185px. Week's aside moves below the grid; most other side columns narrow. |
| At most 900px | Rail becomes 72px with icon navigation. Plan, Planner, People and Group stack; Planner's upcoming aside hides. Agenda retains top navigation and becomes one main column. |
| At most 600px | All variants use a full-width header and labelled navigation; main inset is 23px 17px. Week replaces the time grid with a day strip and agenda. Candidate-response tables become stacked cards. Forms use two columns with the first field spanning both. |
| At most 360px | People rows stack into one column; the sharing field and direct row action indent 37px. The sharing field remains at most 230px wide. |

The availability matrix retains horizontal scrolling in a labelled, focusable
region, including on phones; it is a different surface from the candidate poll.
Do not describe the entire mobile experience as a scaled-down desktop grid.

## Elevation & Depth

Working surfaces are flat, grouped by a border or pale fill. Main panels and
events have no standing shadow. Elevation is reserved for the event dialog,
temporary feedback and the fixed comparison switcher. Exact shadows are recorded
in the sidecar: the shared dialog/toast shadow and the switcher's smaller shadow.
The dialog backdrop dims the underlying page.

Toast feedback fades with a 160ms ease-out opacity transition. An arrival
animation is declared for a new-event preview class, but that class is not
currently attached by the rendered template. Reduced-motion CSS disables
animations and transitions. There is no perpetual animation or animated page
navigation in this capture.

## Shapes

Soft rectangular controls and panels share the compact radius scale in the
frontmatter. Chips are smaller; fields, controls and cells have their own nearby
steps. Avatars and the current date are circular. The event dialog has the largest
standard corner treatment. A dashed outline gives unknown availability a
different silhouette from filled cells.

Calendar cells are clipped by their parent grid. Short event titles can truncate,
while the detail dialog exposes the event name and context. Phone candidate cards
have their own full-width action rather than a tiny table button.

## Components

### Buttons and navigation

Primary buttons use blue with white text; secondary buttons are white with a
thin border; quiet buttons have a transparent fill. All share an 8px corner and
normal minimum height of 39px. Compact buttons reduce padding and text size.
Disabled controls use reduced opacity and a not-allowed pointer.

Navigation uses a pale selected fill and stronger text, plus `aria-current` on
the active page. Calendar filters and comparison-layout controls expose pressed
state. The focus-visible outline is 3px with a 3px offset. These are observed
behaviours, not evidence of a complete accessibility audit.

Availability edits restore focus to the changed cell; confirming a time moves
focus to View in calendar; reopening the plan focuses the visible reply control.

### Fields and status chips

Form fields have visible labels, a white fill, a restrained border and a 40px
minimum height. The search field instead uses the ground fill with an inline
search icon. Inputs inherit the font of their label/container. Errors appear as
text with an alert role; native date/time/select controls retain browser behaviour.

Status chips are small text spans with colour and wording together. “Yes”, “No”,
“Maybe”, “No reply”, “Time chosen” and attendance states remain distinct. Chips
are not all interactive, and the sidecar must not invent hover behaviour for
static status text.

### Calendar events and availability cells

Grid events are native buttons with a time, title and—where space permits—state.
They open a labelled native dialog; agenda rows offer a roomier event link.
The three calendar context colours are preserved across these representations.

Availability cells use green available, cool busy and dashed unknown/not-shared
states. Only the sample user's row is interactive. The prototype currently groups
unknown and not-shared presentation; the product specification distinguishes the
concepts. A yes answer to a candidate time does not visually become accepted
attendance for every invitee.

### Privacy preview and review tooling

People shows a sharing select beside each friend and a pale preview of what that
person can see. Its wording, hidden details and stop-sharing action are as
important as the panel styling. Accepting a friendship keeps calendar access off.

The dark floating layout switcher and top fictional-data notice are review tools.
They are not proposed production navigation. Toasts describe in-memory changes;
no email is sent and refreshing resets the sample. Sidecar snippets demonstrate
appearance only and do not carry the application's event handlers.

## Do's and Don'ts

### Do:

- **Do** use this capture to reproduce and compare the current prototype locally.
- **Do** preserve labelled availability, privacy and attendance states alongside colour.
- **Do** retain visible focus, readable phone alternatives and the fictional-data notice.
- **Do** consult the HTML and surface brief when a component or layout changes.

### Don't:

- **Don't** treat these tokens or any of the three layouts as an approved production identity.
- **Don't** turn an empty calendar into declared availability or a candidate reply into attendance.
- **Don't** promote the comparison switcher or sample group into the production feature set.
- **Don't** invent new fonts, imagery, colour ramps or interaction states from this capture.
