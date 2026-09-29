# Example questions

What to ask once the MCP is connected, which tools answer it, and what comes
back. Each of these has a [skill](https://github.com/TrackIQ-HQ/amazon-seller-skills)
behind it that turns the answer into a finished report.

## Where the ad money went

> Where did my Sponsored Products budget go last month, and what did it buy?

`get_campaigns` and `get_search_terms` over the month, with `state='all'` so
paused campaigns still count. You get spend and sales by campaign, then the
queries underneath them — including the ones that spent without converting.

## Which products recruit new customers

> Which products bring in customers who have never bought from us before?

`get_amc_ntb_asins`, one call per month, against `get_product_ads` for spend.
New-to-brand share by product, next to the share of budget each one takes.
The gap between the two is the interesting part: the product that starts the
most customer relationships is rarely the one with the most spend behind it.

## Whether brand search is flattering the account

> What does my advertising return once I take out people searching my brand?

`get_search_terms` for Sponsored Products and Brands separately, split into
branded, competitor, product-targeting and generic. Generic ROAS is the
number that says whether ads are finding new demand; the blended figure on
the dashboard includes people who already knew you.

## Campaigns bidding against each other

> Which keywords am I bidding on from more than one campaign?

`get_targets` with `record_type='KEYWORD'` joined to `get_product_ads` by ad
group. The same keyword, same match type, same product, in two live ad groups
means two of your own bids in one auction.

## How long shoppers take

> How long do shoppers take between the first ad and the purchase?

`get_amc_time_to_conversion` by position, one call per month. Buckets from
under a minute to 7+ days. The share landing after a week is the share your
7-day Sponsored Products report cannot see — and it sets how far ahead of a
sales event upper-funnel spend should start.

## Products selling with no ad

> Which ASINs sell well but have no ad behind them?

`get_product_performance` against `get_product_ads`, keeping only ads that
are live all the way up to the campaign. Check stock before advertising any
of them — a product with nothing to sell should stay dark.

## Stock about to run out

> Which ASINs run out before the next shipment lands?

`get_inventory_snapshot` with recent sales velocity from
`get_product_performance`. Days of cover per ASIN, and what the stockout
would cost at the current run rate.

## Rank, and whether it holds

> Did last month's spend move organic rank, and did it stay moved?

`get_keyword_rank` daily, next to spend from `get_campaigns`. Rank that falls
back the week spend stops was rented, not earned.

---

[Tool reference →](tools.md) · [Setup →](setup.md) ·
[The 30 skills →](https://github.com/TrackIQ-HQ/amazon-seller-skills)
