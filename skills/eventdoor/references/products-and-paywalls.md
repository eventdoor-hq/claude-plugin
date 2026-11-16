# Set up products and paywalls

On a platform that doesn't sell content, the catalog tools aren't offered and the paywall tools say nothing can be put behind a paywall.

## The catalog (platform admins)

The tickets and plans belong to the platform: organizations put them on their content. Only a platform admin's assistant changes the catalog, and only while the platform's **Change the product catalog** setting is on.

- **Read**: `list_products`, or with `product_id` for one product and the content it is sold on.
- **Create**: `create_product` with `name`, `kind` (`ticket`, bought once, or `plan`, billed monthly), `price` in the currency's usual units as digits (such as "12.00", not cents) and `currency`; optionally `display_label`, `features`, and for a plan the plans it `includes`. Dry-run it and show the user what it will create. A name already in the catalog is refused.
- **Change**: `update_product`. A name, description, label or features change at once. A new price for a product that content sells or viewers subscribe to files a request a platform admin approves; viewers already subscribed keep their price.
- **Archive**: `archive_product` always asks for a platform admin's approval: the product comes off every paywall, and content it was the only ticket or plan on becomes free. Say so before you ask.
- **Plans that include plans**: `set_plan_includes` replaces the list; only plans can be included.

## Paywalls (organization admins)

1. **Read** with `get_paywall` (`type` is `hub`, `broadcast` or `collection`, and `target` its slug or id): its own tickets and plans, and the paywall that actually applies, which a broadcast can inherit from its hub or a collection.
2. **Pick products** from `list_products`: `tickets` are one-time products and `plans` are subscriptions.
3. **Dry-run** `set_paywall` (or `clear_paywall` to remove its own paywall) and tell the user what viewers will have to buy, and whether it needs approval.
4. **Apply.** Content viewers can't reach yet (a draft broadcast, a hub or collection whose page is off and whose broadcasts are all drafts) changes at once. Published content, which includes unlisted broadcasts and every new hub, files a request an organization admin approves; add a `note` and give the user the approval link.

Changing a paywall needs the organization's **Change the schedule** setting on. Prices are set in the catalog, not on the paywall.
