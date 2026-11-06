# MiniCalendar

MiniCalendar is a planned personal calendar with optional sharing among friends
and small groups. People can organise their own time, choose who can see their
availability, propose times together, and confirm plans. Friends arranging an
evening out and bands organising rehearsals or gigs are example uses of the same
core product.

The delivery direction is a responsive Svelte web app first, followed by dedicated
iOS and Android apps. Application data lives on the server and is accessed through
the shared `http_api` runtime, following MiniFast and MiniHACCP's architecture.
Connecting as friends does not automatically grant calendar access.

Status: **research and interface exploration, 6 November 2026**. A sample-data
browser prototype explores the experience. Production application code, database
schema, and calendar APIs have not been implemented. `minicalendar`
is the working repository name; public branding and pricing remain undecided.

## Documents

1. [Research brief](docs/research-brief.md): confirmed requirements, audiences,
   example journeys, and research boundaries.
2. [Research findings](docs/research.md): inspected platform capabilities,
   adaptable application patterns, official product comparisons, calendar
   semantics, and integration options.
3. [Product plan](docs/product-plan.md): proposed features, relationships,
   permissions, delivery stages, acceptance scenarios, and remaining decisions.
4. [Feature recommendations](docs/features.md): a concrete proposed first web
   release, priorities, recurrence and notification recommendations, and journeys.
5. [Interactive web mockups](docs/mockups/README.md): three layouts to compare,
   planning and privacy interactions, and desktop/phone screenshots.

Start with the feature recommendations and interactive mockups for discussion.
Recommendations in these
documents are distinct from confirmed requirements and a future implementation
specification. External calendar connections are being researched now for later
implementation.

From the parent `miniproject` workspace, start the preview with:

```sh
./prototyping/minicalendar/start.sh
```

Open <http://127.0.0.1:5176/mockups/>. For a remote VS Code session, forward port
**5176** and use its forwarded address. The [preview guide](docs/mockups/README.md)
also explains direct-file access and the sample interactions.

## Workspace

This is an independent product repository in the [Mini workspace](../README.md),
beside `http_api`, `minifast`, and `minihaccp`. It is already registered as planned
in the [workspace manifest](../repos.json).

Links into sibling repositories are source evidence and assume this workspace
layout. They do not make those applications packaged dependencies. MiniCalendar
will own its application database, business rules, clients, and deployment
configuration while using the shared runtime.
