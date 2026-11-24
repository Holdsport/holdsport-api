# Holdsport / SportMember API

The documentation of the Holdsport / SportMember v1 API now lives at https://api.holdsport.dk/docs.
Holdsport and SportMember are the same service under two names; one API serves both.

- Reference (browser): https://api.holdsport.dk/docs
- Markdown pages: https://api.holdsport.dk/docs/v1/index.md
- OpenAPI 3.1: [`openapi.yml`](openapi.yml) and [`openapi.json`](openapi.json) in this repository, or https://api.holdsport.dk/openapi/v1.json
- For AI coding agents: https://api.holdsport.dk/llms.txt

## Pages

- [Holdsport / SportMember API v1](https://api.holdsport.dk/docs/v1/index.md): Overview of the v1 REST API: base URL, conventions and where to find each topic.
- [Quick start](https://api.holdsport.dk/docs/v1/quick-start.md): Make your first calls with curl: list teams, read upcoming activities, attend one, and poll efficiently.
- [Authentication](https://api.holdsport.dk/docs/v1/authentication.md): HTTP Basic auth with a Holdsport or SportMember login, managed profiles (acting for a child), and what a 401 means.
- [Polling and caching](https://api.holdsport.dk/docs/v1/polling.md): Use ETag and If-None-Match to poll cheaply, what changes an ETag, and how often to poll.
- [Errors](https://api.holdsport.dk/docs/v1/errors.md): Every status code the API answers, what the body looks like, and what a client should do.
- [Rules for clients](https://api.holdsport.dk/docs/v1/rules-for-clients.md): The short list of rules every integration (and every AI agent writing one) should follow.
- [Teams](https://api.holdsport.dk/docs/v1/teams.md): List the teams the user is on or administers; the starting point for activities, members and notes.
- [Activities](https://api.holdsport.dk/docs/v1/activities.md): Read a team's upcoming activities, or one activity, with attendees, actions, comments and rides embedded.
- [Attendance](https://api.holdsport.dk/docs/v1/attendance.md): Answer an activity (attend, decline, available) by following its actions, list who attends and their guests, and answer for others as a coach.
- [Tasks](https://api.holdsport.dk/docs/v1/tasks.md): List an activity's tasks (bring cake, drive, wash shirts) and take one, or assign one as a coach.
- [Members](https://api.holdsport.dk/docs/v1/members.md): List a team's members or read one, with contact details where the club and member allow it, club fields and player colours.
- [Notes](https://api.holdsport.dk/docs/v1/notes.md): Read a team's notes (the team's pinned information, such as rules, addresses and documents).
- [User and profiles](https://api.holdsport.dk/docs/v1/user-and-profiles.md): Read the logged-in user's profile and list the managed profiles (children) the user can act as.
- [Removed endpoints and changes](https://api.holdsport.dk/docs/v1/removed.md): Endpoints the old documentation listed that no longer exist, corrections to the old documentation, recent behaviour changes, and endpoints added since.

This repository is a mirror and is updated from the Holdsport / SportMember source. See
[`CHANGELOG.md`](CHANGELOG.md) for endpoints added since and for what changed
compared with the earlier README.
