# Tool reference

What each tool answers, and what the data does that you would not expect.
Every tool takes an account and a date range; `list_marketplaces` first, then
`set_context` if more than one marketplace is connected.

## Account

| Tool | Returns |
|---|---|
| `list_marketplaces` | The Amazon accounts and marketplaces this connection can read. Call it first and match on the account name — more than one TrackIQ connection can be active at once, with identical tool names behind them. |
| `set_context` | Pins the account and marketplace for the calls that follow. |
| `get_account_overview` | Spend, sales, orders and the headline ratios for the window, as one row. |

## Products and sales

| Tool | Returns |
|---|---|
| `get_product_performance` | Revenue, units, sessions, orders and conversion by ASIN. The source for titles: the advertising tools often return none. |
| `get_product_categories_performance` | The same roll-up by category rather than product. |
| `show_products` | Catalogue rows with images, for when a report needs them. |

**Watch for:** one ASIN can appear several times, once per SKU, including
merchant-fulfilled duplicates with zero revenue. Sum by ASIN before ranking.

## Sponsored Ads

| Tool | Returns |
|---|---|
| `get_campaigns` | Spend, sales, orders, ACOS and ROAS by campaign, with `portfolio_id` and `state` on every row. |
| `get_campaign_groups` | Budget groupings above campaigns. |
| `get_ad_groups` | The same metrics per ad group, with its campaign. |
| `get_product_ads` | One row per advertised product: ASIN, SKU, ad group, state, spend and sales. |
| `get_targets` | Keywords (`record_type='KEYWORD'`) or product, category and audience targets (`record_type='TARGET'`), with match type, bid and spend. |
| `get_search_terms` | What shoppers actually typed, with spend, sales and orders. |
| `get_portfolios` | Portfolio-level spend and sales. |

**Watch for:**

1. **Every one of these defaults to `state='enabled'`.** Pass `state='all'`
   if you want totals that reconcile to the console, because paused campaigns
   still spent money in the window.
2. **Enabled does not mean serving.** An enabled ad inside a paused campaign
   reports `enabled`. Treat a row as live only when the ad, its ad group and
   its campaign are all enabled — on a mature account a third of enabled ads
   fail that test.
3. **`limit` binds silently.** `get_targets`, `get_product_ads` and
   `get_search_terms` return exactly `limit` rows on any real account. Page
   with `offset` until a call returns fewer. Do not stop on `next_cursor`: it
   comes back null on full pages.
4. **The tail is long.** A month of Sponsored Products search terms can run
   past 4,000 rows, most under $3. Stop paging when the pulled spend
   reconciles to `get_campaigns` for the same window, and say what share you
   covered.
5. **`ad_type='all'` blends attribution windows** — Sponsored Products
   reports on 7 days, Brands and Display on 14. Spend has no window and adds
   safely; a blended ROAS does not mean much.

## DSP and Amazon Marketing Cloud

| Tool | Returns |
|---|---|
| `get_dsp_performance` | DSP by campaign, creative or audience: impressions, spend, sales, DPV, add-to-cart and new-to-brand. |
| `get_amc_ntb_purchases` | New-to-brand and repeat purchases by campaign, per month, across SP, SB, SD and DSP. |
| `get_amc_ntb_asins` | The same split by tracked ASIN. |
| `get_amc_time_to_conversion` | Purchases by time-since-first-ad bucket, from under a minute to 7+ days. |
| `get_amc_attribution_paths` | The sequences of ad touches that preceded purchases. |

**Watch for:**

1. **AMC is monthly and each month is its own cohort.** One call per month,
   and never add months: a customer can appear in several.
2. **AMC counts ad-exposed buyers**, not all customers. "Users" here means
   people who saw an ad and then bought.
3. **AMC campaign IDs are their own namespace** — small integers that never
   join to Sponsored Ads or DSP IDs. Join spend by exact campaign name.
4. **`get_dsp_performance` defaults to active campaigns.** Pass `state='all'`
   or a paused campaign's spend vanishes from the month.
5. **`get_amc_time_to_conversion` populates purchase counts only.** Sales,
   units and the new-to-brand columns come back zero; they are not zeros, they
   are unpopulated. Its `total_brand_purchases` counts any purchase from the
   brand after the ad, `purchases` only the advertised product.
6. **Numbers arrive as strings**, ASINs arrive lowercase, and titles are
   often null. Cast, uppercase, and take titles from
   `get_product_performance`.

## Search and rank

| Tool | Returns |
|---|---|
| `get_search_query_performance` | Your impressions, clicks and purchases against the whole market for a query, with brand share of each. |
| `get_search_query_cart_analysis` | The same funnel through add-to-cart. |
| `get_keyword_rank` | Daily organic and sponsored rank, and Amazon's Choice. |
| `get_bsr` | Daily Best Sellers Rank and price. |

**Watch for:** Search Query Performance is **weekly** — Sunday to Saturday —
and the tool pins to the latest week overlapping your dates. Call it once per
week to cover a month, and never average shares across weeks. Its purchase
share counts organic and paid together, so it says how much of a search the
brand already wins, not what it would win without ads. On a small brand a
week can carry single-digit purchases, where "100%" means almost nothing.

## Inventory and Vendor Central

| Tool | Returns |
|---|---|
| `get_inventory_snapshot` | On-hand, inbound and reserved units, with days of cover. |
| `get_vendor_product_sales` | Shipped and ordered revenue, units and margin. |
| `get_vendor_inventory_health` | Sell-through, ageing and unhealthy inventory. |
| `get_vendor_forecasting` | Amazon's own demand forecast. |

---

Every one of these traps is encoded in the
[TrackIQ skills](https://github.com/TrackIQ-HQ/amazon-seller-skills), so you
do not have to remember them.
