# Changelog

## Added

- **24 November 2026:** `GET /v1/teams/{team_id}/sub_teams` lists a team's player colours with their members (see
  "Player colours" in [Members](https://api.holdsport.dk/docs/v1/members.md)). No existing response changed.
- **24 November 2026:** `GET /v1/activities/{activity_id}/guests` lists the guests members bring to an activity
  (see "Guests" in [Attendance](https://api.holdsport.dk/docs/v1/attendance.md)). No existing response changed.

## Corrections to the old documentation

The old README and `openapi.yml` (OpenAPI 3.0) described an older version of the API. The current documentation
describes what the API actually returns. The main differences:

- **Authentication** is now documented in the spec (`basicAuth`), including managed profiles.
- **Operations added to the spec:** `GET /v1/user`, `GET /v1/profiles` and the attendance writes
  (`POST /v1/activities/{activity_id}/activities_users`, and `PUT`, `PATCH` and `DELETE` on
  `/v1/activities/{activity_id}/activities_users/{id}`, where `{id}` is the id of the member's answer). Every
  operation has an `operationId`, examples and the error responses that apply to it.
- **Activity `status` is an integer** (`0`–`5`), not a string such as `"tilmeldt"`. The translated text is in
  `activities_users[].status`; use `status_code`.
- **`actions` is an array of objects** such as
  `{"activities_user": {"user_id": 700001, "picked": 1, "joined_status": 1, "name": "Attend"}}`, not of strings.
  Labels such as "Tilmeld" are translated.
- **`action_method` can be `GET`** for payment activities, with an absolute sign-in URL as `action_path`.
- **`endtime` and `pickup_time` can be `""`**; `pickup_time` is free text.
- **Fields the old spec left out:** `club` (a string `"true"`/`"false"`), `department`, `registration_type`,
  `activities_users`, `comments`, `max_attendees`, `no_rsvp_count`, `no_rsvp`, `ride`, `ride_comment`, `rides`,
  `show_ride_button`, `event_type`, `event_type_id`, and `activities_coaches` (only when present).
- **Members** have `id, firstname, lastname, role, member_number, birthday, addresses[], profile_picture_path,
  club_fields`; the old flat `name`/`email`/`mobile`/`address` shape is gone. `members/{id}` answers `{}` for a user
  who is not on the team.
- **Team `role`** can be `null` for teams the user only administers.
- **Notes** have exactly `title, body, created_at, created_by, attachment_path`.
- **Profiles:** an empty `address` is `""`, not `" "`.
- **Errors:** `401` (two kinds), `404`, `406`, `422` and `500` are documented with their real bodies.
- The `rides`, `comments` and `activities_coaches` write endpoints were removed, and `PUT`/`PATCH /v1/user`
  (profile updates) are being retired: they answer `404` once the old implementation is switched off. See
  [Removed endpoints and changes](https://api.holdsport.dk/docs/v1/removed.md).
- Examples are valid JSON (the old ones had trailing commas and missing commas).
