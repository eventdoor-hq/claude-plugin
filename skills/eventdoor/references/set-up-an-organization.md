# Set up a new organization

For a platform admin setting up a customer. Only a platform admin can create an organization, and only while the platform's setting for assistants to create organizations is on (the platform's Integrations page in the admin). Nothing deletes an organization, so get the name right first.

1. **Collect** the organization's name and a one-line description, and who should be invited, with each person's role (member or admin).
2. **Dry run.** Call `create_organization` with `name`, `description` and `dry_run` set to true. Show the user the name and the web address it would get, and whether the name is taken. If it is taken, ask for another name; don't add a suffix on your own.
3. **Create.** Make up a new `client_request_id` (letters, digits, `.`, `_`, `:` or `-`, up to 64) and call `create_organization` with it. If the call fails partway (setting up storage or live streaming can), call again with the SAME name and the SAME `client_request_id`: it finishes that organization instead of making a second one. Never reuse an id for a different organization; an id someone else already used is refused, so make up a new one.
4. **Hubs, collections and tags.** With the user, create what the organization runs: `create_hub` (name, dates, `timezone`), `create_collection` (a `type` such as team or venue) and `add_collection_items`, `create_tag`. Dry-run each first. A name already in use is refused with the one that has it: use that one.
5. **Invite people.** For each person, call `invite_member` with `email`, `role` and a `note` for the approver. It files a request, not an invitation: no email is sent until an admin of the organization approves it on its Approvals page. Give the user each request's approval link. Don't repeat the addresses back in your summary.
6. **Next:** build the site (`references/build-a-site.md`) and its schedule (`references/plan-a-schedule.md`).

The new organization starts with the platform's default assistant settings. If a later step is refused by one, tell the user which setting it names: an organization admin turns it on in Settings > Integrations.
