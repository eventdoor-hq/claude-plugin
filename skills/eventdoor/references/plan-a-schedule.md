# Plan a season schedule

Broadcast changes are saved at once (they are not drafts), so preview everything. Creating needs the organization's **Create things** setting on; changing existing broadcasts needs **Change the schedule**. You must be an admin of the organization.

## Read what exists

- `list_hubs` for the hubs and their time zones. A season usually gets its own hub: create it with `create_hub` (dry run first) if it doesn't exist.
- `list_broadcasts` with `hub`, `state` (`upcoming`, `live`, `past`) or a `from` / `to` start range. Pass `cursor` for the next page. Each broadcast shows its time in its own time zone, its visibility and its `revision`.

## A weekly series

1. Collect the hub, a title, the `days`, the local start `time` (24-hour, in the hub's time zone), `duration_minutes`, and either a `count` or an `until` date. `first_date` sets the earliest day; `number_titles` adds " #1", " #2" and so on.
2. Call `create_broadcast_series` with `dry_run` set to true and show the user every date and time it lists. Check daylight-saving weeks with them.
3. Only after they agree, call it again without `dry_run`. At most 26 per call; for a longer season, make several calls. Each broadcast is an ordinary one you can change on its own; nothing is stored as a series.
4. If it stops partway, the result says which were created. Don't re-run the whole series: create the rest from where it stopped.

One-off games use `create_broadcast` (dry run first). New broadcasts are unlisted: publishing them is a request (`references/publish-and-delete.md`).

## Moving broadcasts

- **One broadcast**: `get_broadcast`, then `update_broadcast` with its `revision` as `expected_revision`, and only the fields that change (`title`, `description`, `starts_at`, `ends_at`, `tag_ids`, `collection_items`; `hub` only for an uploaded video).
- **Several at once** (a rain delay, a shifted kickoff): `reschedule_broadcasts` with up to 50 `broadcasts`, either one `shift_minutes` for all or a new `starts_at` each, and each one's `revision` from your last read as its `expected_revision`. Dry-run it and show the new times. All of them move, or none does; a refusal lists every problem, and if anyone changed one since you read it, nothing moves: read them again and retry with their new revisions.

The admin's schedule rules apply: a start can't be in the past, the end comes after the start, and broadcasts sharing a stream key can't overlap. Times you send are ISO 8601 with an offset.

No tool ends a broadcast, changes who can see it, or rotates its stream key: those stay in the admin.
