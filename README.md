# Amazon MCP Server — TrackIQ

**Connect Claude, ChatGPT or Cursor to your live Amazon data through one MCP
server.** Retail sales, profitability, Sponsored Ads, Amazon DSP, Amazon
Marketing Cloud, Search Query Performance, organic rank, Best Sellers Rank,
inventory and competitor tracking — read through a single connection, in the
assistant you already use.

[**Get access →**](https://l.trackiq.com) · $69/month, no other fees ·
[30 ready-made skills](https://github.com/TrackIQ-HQ/amazon-seller-skills) ·
[Full product detail](https://l.trackiq.com)

[![TrackIQ MCP — connect your AI assistant to Amazon data. Works with Claude, ChatGPT and Cursor.](.github/trackiq-mcp-banner.png)](https://l.trackiq.com)

---

## What is an Amazon MCP server?

The [Model Context Protocol](https://modelcontextprotocol.io) is an open
standard that lets an AI assistant call external tools. An **Amazon MCP
server** is the piece in the middle: it holds the connection to your Amazon
accounts and exposes them as tools the assistant can call, so you can ask a
question in plain language and get an answer computed from your own numbers
rather than a guess.

Amazon publishes its own MCP server for the **Ads API**. TrackIQ covers the
whole business instead of one API: Seller Central and Vendor Central
alongside Sponsored Ads, DSP, AMC, Brand Analytics, organic rank and
competitor data, normalised so one question can cross all of them.

Without it, an assistant can talk about Amazon advertising in general. With
it, it can tell you which of your campaigns wasted money last week.

## Quick start

```bash
claude mcp add trackiq "https://trackiq.com/mcp"
claude mcp list          # trackiq · connected
```

Authorise Amazon through OAuth when prompted — TrackIQ never sees your
password; Amazon issues a scoped token directly. Then ask:

```
Which campaigns spent more than $500 last month with no sales?
```

Claude.ai, ChatGPT and Cursor connect the same server as a custom
integration. [Setup for each client →](docs/setup.md)

## What it connects

| Area | What you can read |
|---|---|
| **Retail sales** | Revenue, units, sessions and conversion, by product or by day |
| **Profitability** | True P&L after fees, refunds, COGS and ad spend |
| **Sponsored Ads** | Products, Brands, Display and Video — campaigns, ad groups, targets, search terms, placements |
| **Amazon DSP** | Campaigns, creatives, audiences, video and viewability |
| **Amazon Marketing Cloud** | New-to-brand customers, attribution paths and time to conversion |
| **Search Query Performance** | Your share of searches, clicks, carts and purchases against the market |
| **Organic rank** | Daily keyword rank, sponsored rank and Amazon's Choice |
| **Best Sellers Rank** | Daily BSR and price history |
| **Inventory** | Stock levels, inbound units and out-of-stock alerts |
| **Promotions** | Promo and coupon cost, inside the P&L |
| **Competitors** | Rank, BSR and price for competitor ASINs |
| **Vendor Central** | Shipped revenue, margin, returns and demand forecasts |

Beyond reading, the MCP can act: create campaigns, add keywords and
negatives, and change bids, budgets and placements. Available fields and
actions depend on the Amazon accounts you connect and the integrations you
enable.

## The tools

Grouped by what they answer. Names are what your client will list once the
server is connected.

| Group | Tools |
|---|---|
| **Account** | `list_marketplaces`, `set_context`, `get_account_overview` |
| **Products & sales** | `get_product_performance`, `get_product_categories_performance`, `show_products` |
| **Sponsored Ads** | `get_campaigns`, `get_campaign_groups`, `get_ad_groups`, `get_product_ads`, `get_targets`, `get_search_terms`, `get_portfolios` |
| **DSP & AMC** | `get_dsp_performance`, `get_amc_ntb_purchases`, `get_amc_ntb_asins`, `get_amc_time_to_conversion`, `get_amc_attribution_paths` |
| **Search & rank** | `get_search_query_performance`, `get_search_query_cart_analysis`, `get_keyword_rank`, `get_bsr` |
| **Inventory** | `get_inventory_snapshot` |
| **Vendor Central** | `get_vendor_product_sales`, `get_vendor_inventory_health`, `get_vendor_forecasting` |

[**Tool reference, with the traps in the data →**](docs/tools.md) — what each
one returns, and the things that bite: tools that default to enabled-only,
AMC months that must never be summed, reports that truncate silently at
`limit`.

## Example questions

```
Where did my Sponsored Products budget go last month, and what did it buy?
Which products bring in customers who have never bought from us before?
Which keywords am I bidding on from three campaigns at once?
How long do shoppers take between the first ad and the purchase?
Which ASINs sell well but have no ad behind them?
Which of my ASINs will stock out before the next shipment lands?
```

[More worked examples, with the shape of the answer →](docs/examples.md)

## 30 skills, ready to run

A skill is a folder of instructions your assistant loads when it is relevant —
what to pull, how to judge it, what a good report looks like. TrackIQ
publishes 30 of them for this MCP, covering Sponsored Ads, AMC & DSP, search,
listings, inventory and reporting.

```
/plugin marketplace add TrackIQ-HQ/amazon-seller-skills
```

[**Browse the catalog →**](https://github.com/TrackIQ-HQ/amazon-seller-skills)
· [Skill pages →](https://trackiq.com/skills)

## Access

One plan at **$69/month**: every tool and all 30 skills, with no per-seat or
usage fee. You bring your own Amazon account and your own assistant
subscription — TrackIQ charges for data access, not for AI usage.

[**Start here →**](https://l.trackiq.com)

## Questions people ask

**Does Amazon have an official MCP server?** Amazon offers one for the Ads
API. It covers advertising only. TrackIQ spans Seller Central, Vendor
Central, DSP, AMC, Brand Analytics, rank and competitors through one
connection.

**Which assistants work?** Anything that speaks MCP. Claude Code, Claude
desktop, Claude.ai, ChatGPT and Cursor are the ones we document.

**Is my data safe?** Authorisation is OAuth 2.0 against Amazon. TrackIQ never
receives your Amazon password, and the token is scoped to the accounts you
authorise. [Security →](https://trackiq.com/mcp-security)

**How fresh is it?** Amazon's reporting pipelines settle over hours, not
seconds, so figures for today keep moving. Judge a day once it is complete.

**Can it change my campaigns?** Yes — write actions cover campaign creation,
keywords and negatives, bids, budgets and placements. Ask your assistant to
confirm before it writes.

**Does it replace my dashboards?** It replaces the part where you export a
CSV to answer one question. Ask instead.

---

TrackIQ · [trackiq.com](https://trackiq.com) ·
[MCP](https://l.trackiq.com) ·
[Skills](https://github.com/TrackIQ-HQ/amazon-seller-skills) · MIT licensed
documentation
