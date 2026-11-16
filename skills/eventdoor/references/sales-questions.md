# Answer sales questions

Any member of an organization can read its sales; a platform admin can also read the whole platform at once by leaving `project` out.

**Say this with every sales answer:** the amounts are gross sales, what buyers paid Eventdoor for the content. They are not what the organization is owed, which is settled by invoice. Refunds and chargebacks are handled by Eventdoor; no tool refunds a sale, so send refund requests to Eventdoor.

- **Totals**: `get_sales_summary` for a `month`, or a `from` / `to` range of days (UTC; this month so far by default). Split it with `breakdown` (`hub`, `broadcast`, `product`, `day`, or `organization` for the whole platform) and compare with the period before with `compare_to_previous`. Amounts are per settlement currency; never add different currencies together.
- **Individual transactions**: `list_transactions`, filtered by `types`, `hub` (its id, or with a `project` its slug), `broadcast` or `product_id` (ids from the summary), 25 at a time with `cursor`. They never name the buyer.
- **One buyer**: only when the user gives you the buyer's email address, call `get_buyer_purchases` with it exactly as given. Never ask for an address to browse buyers, and never repeat the address in your answer. An address with no account and an account with no purchases get the same answer: say no purchases were found, not that the person doesn't exist.

The figures match the admin's Sales page for the same dates. There are no viewer numbers to report.
