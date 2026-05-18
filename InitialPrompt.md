# mini-calendar Project Brief

I am planning a new project internally called mini-calendar.

## Technical Direction

- The project should follow the same general architecture as minifast.
- It will use the existing httpapi server.
- It will have:
  - a Svelte web app,
  - an iOS app,
  - an Android app.
- The first implementation can focus on the database and web/API surface.
- Database components should be adapted from minifast where appropriate, especially account/auth/person-style multi-tenancy patterns.
- Manual entry is the MVP for readings. Sensor/device integration should be allowed for in the model but not implemented initially.
