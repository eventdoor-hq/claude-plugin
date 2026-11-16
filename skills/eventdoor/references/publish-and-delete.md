# Publish or delete with approval

You never publish or delete directly. You file a request; a person decides. Nothing changes until then, and a yes typed in the chat is never an approval.

## Ask

- **Publish**: `request_publish` with `what`:
  - `page`: a page's draft (`target` is its page id; pass the `expected_revision` you read),
  - `site`: the header, footer and theme draft (no target),
  - `broadcast`: make a broadcast public (`target` is its slug or id),
  - `collection_page`: turn on a collection's page.
- **Delete**: `request_delete` with `what`: `broadcast`, `video` (a replay's id), `clip`, `hub` (only an empty one), or `page_section` (`target` is the page id, with `section_id`). Organizations can't be deleted.

Dry-run the request first and show the user what it will do. Add a `note`: one sentence for the approver saying why.

## Tell the user

What the request will change, the approval link it gives, that an admin of the organization approves or rejects it on the Approvals page in the admin (the person who asked may approve their own), and that it expires after 72 hours if nobody decides. A deleted broadcast can be restored in the admin for 30 days, but not once its hub is deleted: a hub delete's dry run says how many such broadcasts it would make unrestorable, so tell the user.

## Confirming in the chat

Some organizations let a publish be confirmed in the chat instead (the **Publish** setting). Then call `confirm_change_request` with the request's `id`: the user's assistant app shows them a confirmation prompt that only they can answer. If they accept, it is published at once; if they decline, the request is rejected. If the app can't show the prompt, nothing is published and you get the approval link to give them. Deletes always wait for an admin.

## Follow up

`get_change_request` says where a request stands: pending, approved (an admin approved it and it is being applied, not yet live: check again shortly), applied, rejected and by whom, expired (nobody decided in time, or withdrawn because an admin turned its setting off: its error then names the setting and who; don't ask again while the setting is off), stale (what it changes moved since you asked, so nothing was applied: read it again and ask again) or failed. `list_change_requests` lists an organization's requests, with `status` to filter.

Invitations (`invite_member`) and paywall changes on published content are requests too, decided the same way.
