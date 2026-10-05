# Buy proxies: how to pick the right pool, what a fair price per GB looks like, and how to test one before you commit

Two people type "buy proxies" into Google and want opposite things. One is running a dozen social accounts and needs a static IP that stays put for months. The other is scraping price pages and needs a fresh residential IP on every request plus a bill that doesn't charge for bandwidth they never burned. Same search, incompatible products.

Most pages that answer this keyword hand you a vendor list and a headline rate. That's not the part that goes wrong. What goes wrong is buying the wrong proxy type, or buying the right type inside a billing model that expires the traffic you paid for. So this guide works through the decision in order, then puts real numbers behind it using DataImpulse, a pay-as-you-go provider whose residential traffic starts at $1/GB.

## The type you buy matters more than which brand you buy from

Every proxy you can purchase falls into four families. They differ in where the IP address comes from, which determines how sites treat traffic from it, and they differ in how you're billed, which determines what you actually spend.

| Proxy type | Where the IP comes from | Typical market pricing | What it handles |
| --- | --- | --- | --- |
| Residential | Real consumer connections at ISPs | ~$1–8/GB, billed by bandwidth | Protected sites, scraping, SERP tracking, ad verification |
| Mobile (4G/5G) | Mobile carrier networks | ~$2–15/GB, or per-IP monthly | The hardest targets, app and mobile-web data |
| Datacenter | Hosting providers | ~$0.50–3/GB, or a few dollars per IP/month | Fast, high-volume work on unprotected targets |
| ISP / static residential | Residential ranges hosted on datacenter hardware | ~$1.50–5 per IP/month | Long-lived accounts, sessions that must not rotate |

The pricing columns above are broad ranges drawn from published comparisons, not a single quote. The reason they're so wide is that a GB of residential traffic and a GB of datacenter traffic are not the same product, and neither is a rotating IP and a dedicated one.

Two practical consequences hide in that table:

**Rotating and static are different purchases.** If your workflow involves logging in, adding to a cart, then checking out, an IP that changes mid-session will break it. Sticky or static sessions exist for exactly this. If your workflow is a million independent page fetches, stickiness is wasted spend.

**Buying datacenter proxies for a protected target is the most expensive mistake in this category.** The IP is cheap because it's easy to identify. You'll pay $0.50/GB to get blocked, then pay again for residential proxies to do the job. The reverse error, buying residential for a static, unprotected workload, just costs more per GB than it needed to.

## What "fair" per GB actually means

Comparisons of proxy pricing tend to describe $3–8/GB as the going residential rate, with enterprise providers at the top of that band. Independent buyer's guides put fair residential pricing lower, around $1.75–3/GB, and treat anything past $7/GB as enterprise territory. Those are figures published by vendors and review sites with their own positions, so treat them as reference points rather than measurements.

What you can verify yourself, before paying anyone:

- **The unit.** Per GB and per IP per month are not comparable. A $0.90/GB rate on a plan with a 100 GB monthly minimum is a $90/month commitment.

- **Whether the traffic expires.** Most subscriptions reset the allowance at the end of the period. Bandwidth you didn't use isn't refunded and isn't carried over.

- **Which targeting features cost extra.** Country selection is included almost everywhere. City, state, ZIP, and ASN targeting frequently carry a surcharge, sometimes a doubling of the per-GB rate. This single line item can change your effective cost by 100%.

- **Concurrency limits.** If the plan caps simultaneous threads at 50 and your scraper wants 500, you'll be tuning retry logic instead of collecting data.

- **Whether you need a subscription at all.** If your workload is spiky, a recurring commitment means paying for capacity in the months you're idle.

That last point is where the billing model starts to matter more than the headline number.

## Where people buy proxies, and what each channel costs you

**Direct providers.** Companies that own or operate proxy infrastructure. You get a named company, a dashboard, documented IP types, an invoicing trail, and terms you can read. Slightly higher prices than the bottom of the market, and you're limited to their catalog.

**Cloud and software marketplaces.** Useful for discovery and comparison, and sometimes convenient if billing already flows through an existing account. You still have to validate IP quality and usage policies yourself.

**Resellers and aggregators.** One dashboard, many locations, often cheap entry bundles. Quality depends entirely on whoever supplied the IPs, which makes debugging failed requests harder, because you can't see the upstream pool.

**Build it yourself on a VPS.** Rent a small server, run a proxy daemon, done. Genuinely cost-effective if you need a handful of stable datacenter IPs and you're comfortable with network config and hardening.

**Free proxy lists.** Scraped from wherever, run by people who won't tell you who they are, frequently misconfigured, and you have no idea what gets logged. Fine for a five-minute experiment. Not something to route production traffic through.

One more channel worth naming directly: providers that resell someone else's pool. It's not dishonest, but it does explain why two vendors with similar marketing can deliver visibly different success rates. DataImpulse, for its part, states that it operates its own pool and does not resell other providers' IPs, which is the kind of claim worth testing against your own targets rather than taking on faith.

## The expiry question: subscriptions versus per-GB

Here's the arithmetic that catches people out.

Say you run price monitoring. Q4 is heavy, around 150 GB. February is quiet, maybe 30 GB. A monthly subscription sized for the busy quarter bills you at the busy-quarter rate all year, and the unused bandwidth in February evaporates at the reset. A pay-as-you-go model with non-expiring traffic bills 150 GB in Q4 and 30 GB in February, and the leftover from a paused project stays in the account.

That difference isn't a marketing angle, it's a structural one. It matters most for seasonal e-commerce monitoring, short SEO sprints, and ML dataset collection that runs hot for two weeks and then stops dead. If your traffic is a flat, predictable line every month, a subscription can work out fine, and sometimes cheaper. Most teams don't have a flat line.

## Where DataImpulse fits

DataImpulse is a proxy provider built around exactly that pay-as-you-go structure. The numbers:

- **Pool and coverage:** 90M+ IPs across 195+ countries, described by the company as ethically sourced and first-party.

- **Rate card:** residential from $1/GB, datacenter from $0.50/GB, mobile from $2/GB, premium residential from $5/GB.

- **Minimum purchase:** $5. No subscription required.

- **Traffic expiry:** none. Unused GBs stay in your account.

- **Protocols:** HTTP, HTTPS, SOCKS5.

- **Sessions:** rotating endpoints on ports 823 (HTTP/HTTPS) and 824 (SOCKS5); sticky sessions on ports 10000–20000, configurable from 1 to 120 minutes, defaulting to 30.

- **Concurrency:** up to 2,000 simultaneous threads out of the box, scalable on request.

- **Targeting:** country selection included; state, city, ZIP, and ASN filters on residential traffic are billed at double the standard per-GB rate.

- **Compliance:** GDPR-aligned sourcing and ISO certification, per the company.

- **Support:** 24/7 human support rather than automated triage.

- **Published figures:** 99.51% success rate, and a 4.8/5 rating on G2 as cited in its own listings.

Two honest caveats before the pricing tables. First, the 2× surcharge on advanced residential targeting is real money, and it's the kind of line item most comparisons bury in a footnote. Second, DataImpulse sells four proxy types and ISP/static residential isn't one of them. If your project needs a dedicated IP that never changes, look at a provider that sells static residential or ISP proxies instead.

👉 [Check DataImpulse's current residential and datacenter rates](https://bit.ly/dataimPulse)

## DataImpulse pricing, product by product

The dashboard works by topping up a balance and selecting how many GB you want, so the tiers below are volume bundles rather than named subscription packages. Rates are the advertised per-GB figures.

### Residential proxies

| Tier | Traffic | Price | Effective rate | Notes |
| --- | --- | --- | --- | --- |
| Entry | 5 GB | $5 | $1.00/GB | $5 minimum; traffic never expires |
| Mid | 50 GB | $50 | $1.00/GB | Country targeting included |
| Large | 100 GB | $100 | $1.00/GB | Same pool, larger balance |
| Volume | 1 TB | $800 | $0.80/GB | Discounted volume tier |
| Custom | 5 TB+ | Custom | From $0.70/GB | Negotiated with support |

👉 [Start with a $5 residential top-up](https://bit.ly/dataimPulse)

### Datacenter proxies

| Tier | Traffic | Price | Effective rate | Notes |
| --- | --- | --- | --- | --- |
| Entry | 10 GB | $5 | $0.50/GB | Randomized subnet access |
| Mid | 100 GB | $50 | $0.50/GB | 99.9% uptime claim |
| Large | 500 GB | $250 | $0.50/GB | Best for sustained crawls |
| Volume | 1 TB | $450 | $0.45/GB | Discounted volume tier |
| Custom | 5 TB+ | From $2,250 | Custom | Negotiated with support |

### Mobile proxies

| Tier | Traffic | Price | Effective rate | Notes |
| --- | --- | --- | --- | --- |
| Entry | 2.5 GB | $5 | $2.00/GB | 4G/5G/LTE carrier IPs |
| Mid | 25 GB | $50 | $2.00/GB | Rotating and sticky sessions |
| Volume | 1 TB | $1,600 | $1.60/GB | Discounted volume tier |
| Custom | 5 TB+ | From $8,000 | Custom | Negotiated with support |

### Premium residential proxies

| Tier | Traffic | Price | Effective rate | Notes |
| --- | --- | --- | --- | --- |
| Entry | 1 GB | $5 | $5.00/GB | Dedicated account manager |
| Mid | 10 GB | $50 | $5.00/GB | All targeting options without the 2× residential surcharge |
| Custom | 5 TB+ | From $20,000 | Custom | Negotiated with support |

Bundle sizes and the per-GB blend inside each tier do get adjusted as product lines change, so before a large top-up it's worth confirming the current figures in your own dashboard rather than relying on any third-party table, including this one.

👉 [Compare all four proxy types in the DataImpulse dashboard](https://bit.ly/dataimPulse)

## Before you pay: an afternoon of testing

A short pilot costs $5 and tells you more than any comparison table. The sequence that actually surfaces problems:

1. **Write down acceptance criteria first.** "Each request must return the expected country, complete three consecutive fetches without a transport error, and stay under two seconds median latency." Vague goals produce vague tests.

2. **Buy the smallest bundle of the type you'll actually run.** Entry tiers exist for this.

3. **Plug the proxy into your real tool**, not a ping test. Scrapy, Selenium, Puppeteer, Playwright, an anti-detect browser, whatever your pipeline uses. Configuration problems only appear in the real client.

4. **Log success rate, block rate, CAPTCHA frequency, and latency** across the regions you care about, over at least a few thousand requests. A 96% success rate at trial volume doesn't tell you what happens at production volume.

5. **Check geo-accuracy specifically.** If you're targeting a city but traffic exits in a different one, your localized data is quietly wrong, which is worse than an obvious error.

6. **Watch the targeting surcharge in the billing panel**, not just the rate card. This is where the 2× advanced-targeting multiplier shows up in practice.

7. **Only then scale.** And scale in steps, re-running the same checks.

DataImpulse's $5 entry point and non-expiring traffic make this cheap: if the pilot fails, the remaining balance still sits in your account for the next attempt instead of expiring.

👉 [Run the test with a $5 DataImpulse balance](https://bit.ly/dataimPulse)

## Red flags worth walking away from

- Rates far below the market floor with no explanation of where the IPs come from.

- No named company, no published terms, no address.

- "Unlimited bandwidth" on a price that can't cover the bandwidth.

- Sales confined to a forum thread or a chat-only channel, with no invoicing option.

- A rate card that doesn't say whether traffic expires, or which targeting filters cost extra.

- Trial volume that performs beautifully and production volume that doesn't, with no channel to escalate to.

## Questions that come up before buying

**Is one proxy type enough?** For a single project, usually yes. Agencies and data teams often split loads: residential for protected targets, datacenter for cheap high-speed fetches, mobile only where carrier IPs are genuinely required. Routing each job to the cheapest tier that works is the single biggest cost lever you control.

**Do I need SOCKS5?** Only if your client needs it. Some automation stacks and non-HTTP traffic benefit; browsers and standard HTTP libraries are fine on HTTP/HTTPS. DataImpulse supports both, on separate rotating ports.

**What happens to unused traffic?** At DataImpulse it stays in your account indefinitely. That's the feature that makes the $5 entry point worth trying rather than a sunk cost.

**How many concurrent requests can I run?** DataImpulse allows up to 2,000 threads by default and will scale that on request. If your pipeline is unusually parallel, confirm the current ceiling before you design around it.

**Is buying proxies legal?** Buying and using them is, in itself, a contractual matter between you and the provider. What you do through them is governed by the target site's terms, applicable data protection law, and your own contracts. A proxy changes your routing; it doesn't grant permission.

---

If you take one thing from this: the decision isn't which brand, it's which pool, which billing model, and whether the traffic you're paying for survives the quarter. Test with the smallest bundle available, measure against your real targets, and let the numbers decide. If a $5 pay-as-you-go balance with non-expiring traffic fits that test, DataImpulse is a reasonable place to run it.

👉 [Buy proxies from DataImpulse starting at $1/GB](https://bit.ly/dataimPulse)
