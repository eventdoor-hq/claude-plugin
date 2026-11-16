---
name: eventdoor
description: Run an Eventdoor live-event streaming site through the Eventdoor connector. Use whenever the user asks about or wants to change anything on Eventdoor - their organizations (projects), hubs, broadcasts and schedule, site pages, theme, header, footer and logos, collections, replays and the video library, tickets, plans and paywalls, sales, who changed what, inviting people, or publishing and deleting with approval. Also use for setting up a new customer organization, planning a season of broadcasts, building or styling a site from a brand, answering sales questions, or finding out why a broadcast has no replay.
---

# Eventdoor

Eventdoor runs live-event streaming sites. You work on them through the Eventdoor tools of the connected MCP server, acting as the signed-in person: you see and change only what they can in the Eventdoor admin.

## Beta

AI assistant access is in beta: the tools, what an assistant can read and change, and how it is set up may change as we improve it. To report a problem or share feedback, email support@eventdoor.com.

The first time you use an Eventdoor tool in a conversation, tell the user it is in beta and where to report problems. When a tool result carries a beta notice, include it in your answer.

## How Eventdoor is organized

- **Platform**: one customer's streaming service, for example a league's or a reseller's. One connection reaches every platform the person belongs to. Every tool except `list_platforms` acts on one platform, named in its `platform` argument; call `list_platforms` first when you don't know which one the user means, and ask when more than one could fit.
- **Organization**: what the tools call a **project**. It runs a site, hubs and broadcasts. Name one by its slug or its address (`https://<platform host>/org/<slug>`, or a link to one of its admin pages) in the `project` argument; `list_my_projects` gives both, and the person's role in each.
- **Hub**: an event, season or venue that broadcasts sit under, with dates and a time zone.
- **Broadcast**: one live stream with a scheduled start and end, under a hub. After it ends it may have a replay.
- **Collection**: a list of one kind of thing, such as teams, venues, seasons or videos.
- **Pages**: an organization's site and each hub's are built from sections. The site's theme (colors, corners, fonts), header, footer and logos are separate from the pages.
- **Products**: the platform's tickets (bought once) and subscription plans. A **paywall** on a hub, broadcast or collection names the products that unlock it.

## Drafts and live changes

- **Drafts**: page changes, the theme and the header, footer and logos land in a draft. Visitors see nothing until a person publishes it. Each result gives a preview link: pass it on.
- **Saved at once**: broadcasts, hubs, collections, tags and their items are saved as soon as you call the tool. A new broadcast is unlisted until it is published.
- **Revisions**: a change takes the `expected_revision` you last read (`get_page`, `get_broadcast`, `get_theme`, `get_site_chrome`, or the previous change's result). If it is refused because something moved, read it again and retry; never guess a revision.

## What the organization allows

An organization admin chooses, in Settings > Integrations, what assistants may do, one setting per kind of action: **Edit drafts**, **Change the schedule**, **Create things**, **Publish**, **Delete** and **Invite people**. Reading is always allowed. When a setting stops a change, the message names it: tell the user which setting it is and that an organization admin can change it there. Don't look for another tool to get around it.

## Rules

1. **Preview first.** Before a change, call the tool with `dry_run` set to true where it takes one, and show the user what would change. Otherwise say exactly what you will change. Wait for their go-ahead before the real call.
2. **Say what changed.** After a change, report what was saved, whether it is a draft or live, and the preview or admin link the result gives.
3. **Never ask for or repeat a stream key**, ingest address or playback link. The tools never return them; if the user pastes one, don't repeat it. For a stream key, send them to the broadcast's page in the admin.
4. **Explain approvals.** Publishing and deleting go through a request a person approves (see `references/publish-and-delete.md`). Say what the request will do, give the approval link, and say nothing changes until it is approved. A yes typed in the chat is not an approval.
5. **Buyers stay private.** Look a buyer up only by an email address the user gave you, and never repeat it. Sales figures are gross sales, not what an organization is owed; refunds and chargebacks are handled by Eventdoor, and no tool refunds a sale.
6. **Platform admins only** create organizations and change the product catalog. If the user isn't one, say so rather than trying.
7. **No viewer numbers.** The platform doesn't record them; say so instead of estimating.

## Recipes

Read the matching recipe before you start:

| The user wants to                                             | Read                                   |
| ------------------------------------------------------------- | -------------------------------------- |
| Set up a new customer organization and invite its people      | `references/set-up-an-organization.md` |
| Plan a season or a weekly schedule, or move broadcasts        | `references/plan-a-schedule.md`        |
| Build an organization's site in one go                        | `references/build-a-site.md`           |
| Style a site from a brand: colors, fonts, logos, menu, footer | `references/theme-from-a-brand.md`     |
| Sell tickets or plans, or put content behind a paywall        | `references/products-and-paywalls.md`  |
| Answer questions about sales                                  | `references/sales-questions.md`        |
| Find out why a broadcast has no replay                        | `references/missing-replay.md`         |
| Find out who changed something, and when                      | `references/who-changed-what.md`       |
| Publish or delete something                                   | `references/publish-and-delete.md`     |

For one page edit, read the page with `get_page`, then use `add_section`, `update_section`, `move_section`, `set_section_hidden` or `remove_section`; for more than two, put them in one `apply_page_changes` call. `list_section_types` and `describe_section_type` say what a section takes.

To cut a highlight (a new replay) or a clip from a broadcast's replay, ask the user for the start and end as times into the replay, as its player shows them (`1:02:30`). You can't watch the video, so never guess where a moment is. Call `create_highlight` or `create_clip` with `dry_run` set to true, show the user the times and length, then create it. Both are drafts viewers don't see until they are published. A refusal that gives the replay status means the broadcast has no recorded replay to cut: explain it as `references/missing-replay.md` does.
