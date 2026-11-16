# Theme a site from a brand

The theme, header, footer and logos are drafts; visitors see nothing until a person publishes them. You must be an admin of the organization, and the **Edit drafts** setting must be on.

1. **Read.** `get_theme` gives the live and drafted theme, the platform's default, the ONLY values the theme accepts (accent colors, neutral bases, corner styles, fonts), and the `revision`. `get_site_chrome` gives the site name, menu, footer, social links and logos.
2. **Match the brand.** Pick the closest offered accent, base, radius, font and heading font for the brand's colors and type, and tell the user which you picked and why. Never send a color code: only the offered names are accepted. If the project's pages should show this theme instead of the platform's, `override` is true; the result says when they would still show the platform's.
3. **Draft the theme.** `set_theme` with `expected_revision` and only the settings that change; dry-run it first. A null returns a setting to the platform's default.
4. **Logos.** A logo or favicon must be in the project's media library. For an image on the web, call `import_image_from_url` with its public address (PNG, JPEG, WebP or GIF, up to 10 MB); it answers the file's id. Images from the user's computer can't be uploaded here: they add them in the admin's media library.
5. **Header and footer.** `update_site_chrome` with `expected_revision` (from `get_site_chrome` or the last change) and only what changes: `branding`, `logo`, `logo_dark`, `favicon`, `header` (site name, menu), `footer` (text, social links). Dry-run it first.
6. **Preview.** Each result has a preview link; give it to the user. To publish, `request_publish` with `what` set to `site` (`references/publish-and-delete.md`).

The platform's own theme, header, footer and logos can't be changed by an assistant.
