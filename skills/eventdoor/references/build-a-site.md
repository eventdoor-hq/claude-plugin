# Build a site with the planner

`plan_site` lays out an organization's home page, menu and footer from what it has (hubs, broadcasts, collections, tags) and what the user tells you. `apply_site_plan` builds it as drafts. You must be an admin of the organization; building needs **Edit drafts** on, and also **Create things** when the plan creates hubs or collections.

1. **Ask how it runs.** One event or an ongoing calendar (`runs`)? Does it run competitions with results, ending in a knockout round? Questions and answers for a FAQ? A call to action (title, button label, link)? Sponsors? A footer tagline and social links? Hubs or collections it still needs? Every answer is optional; don't invent any.
2. **Plan.** Call `plan_site` with the `project` and the `answers`, plus a `theme` from `get_theme`'s choices if the user wants one (see `references/theme-from-a-brand.md`). Nothing is saved.
3. **Show the plan**: the home page's sections in order with why each is there, the menu, the footer, and the hubs and collections it would create. Sections the platform has turned off are left out, and the plan says so. Change the answers and plan again until the user agrees.
4. **Build.** Call `apply_site_plan` with the `plan` exactly as `plan_site` gave it; dry-run it first if the user wants another check. It creates the hubs and collections, replaces the home page's draft sections (locked sections stay), drafts the menu, footer and theme, and answers one preview link. Give the user that link.
5. **If it refuses** because the project, its home page or its header and footer changed since the plan, call `plan_site` again and show the new plan. If it stopped partway, the result says what was made; the next plan uses it.
6. **Fine-tune** sections with the page tools (`get_page`, then `update_section` or `apply_page_changes`). Sports sections such as standings and results start empty: the user fills in their rows in the page editor.
7. **Publish** with two requests: the home page (`request_publish` with `what` set to `page`) and the header, footer and theme (`what` set to `site`). See `references/publish-and-delete.md`.
