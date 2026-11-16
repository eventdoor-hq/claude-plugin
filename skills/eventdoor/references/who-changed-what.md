# Audit who changed something

`list_activity` lists every change to an organization, newest first: who made it, when, to what, and whether it came through an AI assistant. Only an admin of the organization or a platform admin can read it.

1. **Narrow it** to what the user asks about: `kinds` (such as `page`, `broadcast`, `hub`, `collection`, `siteConfig`, `contentGate`, `invitation`), a `from` / `to` range, `via` (`assistant` for changes made through an AI assistant, `credential` for a scoped API credential, `direct` for changes a person made themselves), or `person` with the profile id of someone in an earlier result.
2. **Page back** with `cursor`, 25 at a time, until you reach the time in question; say how far back you looked.
3. **Answer** with who, when (in the user's time zone if you know it), what changed (the field names the result gives) and the link to the thing. When a change carries no name for the person, say so; don't guess who it was.

Other histories:

- A page's published versions and who published each: `list_page_versions`. `restore_page_version` brings one back as the draft (a draft change; dry-run first).
- A publish, delete, paywall or invitation request and who decided it: `list_change_requests` and `get_change_request`.
