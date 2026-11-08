# Cheap Ubuntu VPS: How Little Can You Pay, What Will 1 vCPU Handle, and Why the Renewal Price Decides (Full Plan Table)

Right now the advertised entry price for a cheap Ubuntu VPS runs from $2.99/mo at Cloudfanatic to $6.49/mo at Hostinger, with Arct Cloud at $3.89 and ColossusCloud at $5.00. SpinServers' smallest KVM plan — 2 vCPU, 2 GB DDR4, 40 GB RAID-10 SSD, 4 TB of monthly transfer on a 1 Gbps port — is listed at $12/mo on monthly billing with no setup fee. That's roughly double the headline numbers, and for most people searching this term it's the more useful place to start, because the sub-$7 tier is usually a 24-month prepayment whose renewal rate runs 70% to more than double the sale price.

The rest of this page covers the full SpinServers KVM lineup, the cash difference between prepaying and paying monthly, three ways providers count bandwidth, and one default setting on SpinServers that rules it out for mail servers.

> **Quick pick.** Most readers should start with the **Simple Application Server, 2 vCPU / 2 GB**: 40 GB RAID-10 SSD, 4 TB/month on a 1 Gbps port, 1 IPv4 and 1 IPv6 address, $12/mo billed monthly with no setup fee. It runs a blog, a five-container Docker stack, a WireGuard endpoint or a CI runner, and you can walk away after one month. 👉 check the Simple 2 vCPU plan and today's price

## The full SpinServers KVM VPS lineup

SpinServers splits its VPS range into two families. Simple Application Servers cover websites, dev environments and everyday apps. Advanced plans add cores and RAM for heavier builds. Everything is Intel vCPU with DDR4 RAM on RAID-10 SSD.

| Plan | vCPU / RAM | Storage | Transfer | Price (USD/mo) | Order |
| --- | --- | --- | --- | --- | --- |
| Simple Application Server | 2 vCPU / 2 GB | 40 GB RAID-10 SSD | 4 TB @ 1 Gbps | $12 | [ order the 2 vCPU plan](https://bit.ly/Spinservers) |
| Simple Application Server | 4 vCPU / 4 GB | 80 GB RAID-10 SSD | 8 TB @ 1 Gbps | $29 | [ order the 4 vCPU plan](https://bit.ly/Spinservers) |
| Simple Application Server | 6 vCPU / 8 GB | 120 GB RAID-10 SSD | 8 TB @ 1 Gbps | $39 | [ order the 6 vCPU plan](https://bit.ly/Spinservers) |
| Simple Application Server | 8 vCPU / 8 GB | 160 GB RAID-10 SSD | 10 TB @ 1 Gbps | rate at checkout | [ order the 8 vCPU plan](https://bit.ly/Spinservers) |
| Advanced Application Server | 12 vCPU / 12 GB | 160 GB RAID-10 SSD | 10 TB @ 1 Gbps | rate at checkout | [ order the 12 vCPU plan](https://bit.ly/Spinservers) |
| Advanced Application Server | 16 vCPU / 16 GB | 320 GB RAID-10 SSD | 15 TB @ 1 Gbps | from $74 | [ order the 16 vCPU plan](https://bit.ly/Spinservers) |

Every plan ships with 1 IPv4 and 1 IPv6 address and a 1 Gbps network port. The 8 and 12 vCPU tiers don't print a monthly rate on the product overview; the order page quotes them. Treat the figures above as the listed monthly rates and confirm the number on the checkout screen, which is what actually bills you.

Two notes on positioning. SpinServers' main business is bare metal, listed from $79/mo on month-to-month terms, and the VPS line is the budget entry into the same network. It also means the VPS ceiling here is 16 vCPU. If you need more than that, you're shopping for a dedicated box, not a VPS.

## What 2 GB of RAM actually buys you in 2026

A minimal Ubuntu 26.04 install idles around 600–900 MB with systemd, sshd and journald running. Docker adds roughly 100 MB for the daemon, and each container lands between 50 and 300 MB depending on what's inside. On a 2 GB plan that leaves comfortable room for a reverse proxy plus two or three lightweight services.

It gets tight the moment you add a database. PostgreSQL with default settings wants 1 GB of shared buffers to behave, and MySQL is not gentler. A stack of Nginx, an app server, Postgres and Redis on 2 GB means swapping under load. The $29 tier with 4 GB removes that worry for the price of a couple of coffees; the 6 vCPU / 8 GB tier at $39 is where you stop thinking about memory at all.

Disk matters less than people expect. Ubuntu takes 6–8 GB, so the 40 GB entry plan leaves around 30 GB for code, logs and a database. That's plenty for a site, thin for a media library or a build cache.

## The sticker price and the first invoice are different numbers

Hostinger's KVM 1 shows **$6.49/mo**, marked down from $19.49. That is the 24-month rate: today you pay **$155.76** for two years, and the plan renews at $11.99/mo for the same term. The second 24-month cycle costs about $287.76, so four years of KVM 1 comes to roughly **$443.52** — an average of $9.24/mo rather than $6.49. KVM 2 follows the same shape: $210.96 up front, renewing at $14.99/mo.

Now compare cash outlay. $155.76 today against $12 for the first month at SpinServers. If the project dies in month four, the prepaid provider has been holding $155.76 of your money since day one, while the monthly plan has cost you $48 and stops the moment you cancel.

Over a full two years the prepaid plan still wins on absolute price: $155.76 against $288 for the equivalent monthly spend. That's a real advantage, and if you are certain the box will be running in month 20, take it. The catch is the certainty, plus the fact that the renewal rate — not the sale rate — is what you'll pay for as long as you stay.

👉 see SpinServers' month-to-month VPS options if you'd rather not prepay two years

## 4 TB, 15 TB, "unmetered": three different promises

SpinServers meters transfer and states the allowance plainly: 4 TB, 8 TB, 10 TB or 15 TB per month depending on plan, on a 1 Gbps port. Other providers describe similar allowances in ways that behave very differently.

**Hard quota plus port speed.** Hostinger gives 4 TB / 8 TB / 16 TB / 32 TB per month on a 1 Gbps port across its KVM tiers. SpinServers sits in the same model. You know exactly where the ceiling is, and when you hit it, traffic stops or gets throttled.

**Egress only.** Arct Cloud counts outbound traffic against the plan and leaves inbound free. If you run a mirror, a download host or anything that receives large uploads, this changes the arithmetic in your favour.

**Unmetered fair share.** Cloudfanatic advertises unmetered bandwidth on 1–10 Gbit/s ports. "Unmetered" here means no published cap and no overage bill, subject to fair-use throttling. There's no number to plan against.

Port speed is the number people misread. A 15 TB monthly allowance works out to about 46 Mbps sustained around the clock; 4 TB is roughly 12 Mbps. A 1 Gbps port will never be your bottleneck on any of these plans — the monthly quota is. By the same logic, a 10 Gbit/s port on an unmetered plan doesn't mean you get 10 Gbit/s for a month; it means the provider can burst you when the network is quiet.

## Backups are where cheap plans quietly get expensive

Arct Cloud charges **$0.04 per GB per month** for snapshots you keep until you delete them, and **20% of the server's monthly price** to switch on automatic daily backups. On an $8.89 plan that's about $1.78/mo, which is fair; on a $15.89 plan it's $3.18. Snapshots are Linux-only and available in selected locations.

Cloudfanatic includes free backups and free snapshots on its plans. Hostinger bundles weekly backups and a real-time snapshot with every KVM tier, plus a 30-day money-back window.

The SpinServers KVM spec sheet doesn't list a backup or snapshot add-on, so budget for your own. A nightly `restic` or `borg` job to S3-compatible object storage costs a few dollars a month and survives the provider going down, which a same-host snapshot does not. If you'd rather not run backup tooling at all, that's a reason to weigh the bundled-backup providers more heavily.

## Port 25 is closed by default on every SpinServers VPS

This one is stated on the product page and it's easy to miss. SpinServers blocks port 25 (SMTP) on all virtual private servers to limit IP abuse. You can request it be opened via a support ticket with a justification, and the company reserves the right to refuse for any reason.

Practical consequence: you cannot run a mail server out of the box, and you shouldn't assume the ticket will be approved. For a web host, a VPN endpoint, a CI runner or a Docker host, this is a sensible default that keeps your IP off spam blocklists before you've even logged in.

## Pick Ubuntu 26.04, or 24.04 if something pins you there

Ubuntu 26.04 LTS gets standard security updates until **May 2031**. 24.04 LTS runs to **May 2029**, and 22.04 LTS ends in **May 2027**. A cheap VPS is usually a long-lived box, so starting on 22.04 in late 2026 buys you eighteen months before another migration.

Deploy 26.04 unless a control panel, a pinned kernel module or a vendor package hasn't caught up. When the time comes to move, a fresh install with a data migration beats `do-release-upgrade` on a production box — an in-place release upgrade can leave you debugging a half-migrated system at 2 a.m. with no snapshot to roll back to.

## Refund windows and what leaving costs

Hostinger offers 30 days, ColossusCloud 14 days, Cloudfanatic 7 days. Arct Cloud's page doesn't state a window.

The refund period matters in proportion to what you've prepaid. On a two-year term, 30 days is the window in which you can still recover $155.76. On a monthly plan your exit cost is a single billing cycle by design, which is why SpinServers' VPS pages can get away with not advertising a money-back guarantee: monthly billing with no setup fee caps the downside at one month's charge.

👉 compare the KVM VPS tiers before you commit to a billing term

## Match the plan to the job

- **Static site, blog, small WordPress install:** the 2 vCPU / 2 GB at $12. Nginx or Caddy plus PHP-FPM plus MariaDB fits, and 4 TB handles a few hundred thousand page views.
- **Docker host with 4–6 containers including Postgres:** 4 vCPU / 4 GB at $29. The extra RAM is what stops the OOM killer from visiting.
- **WireGuard or VPN endpoint for a household:** 2 vCPU / 2 GB is more than enough CPU; watch the transfer allowance instead. 4 TB is roughly 130 GB a day, which is a lot of streaming but not infinite.
- **CI runner or build box:** cores and disk speed drive this. The 6 vCPU / 8 GB at $39 with 120 GB of RAID-10 SSD is the sensible floor; the 16 vCPU tier at $74 if your builds are parallel.
- **Small production database:** 8 GB of RAM minimum, so the $39 tier or the 12 vCPU one. Test your working set before you commit to a plan with a metered disk.
- **Mail server:** not here, not until port 25 has been opened in writing.
- **Anything needing more than 16 vCPU:** the VPS line ends there; bare metal starts at $79/mo.

## Before you order

Two things to confirm on the checkout screen. First, the billing period behind the price you're looking at — a monthly rate and a 24-month prepaid rate can differ by a factor of two, and the renewal terms matter more than the introductory one. Second, the cancellation route and any refund window, because that is your only real protection if the network or the disk performance doesn't suit you.

If you want a Ubuntu box running this week without tying up two years of cash, the 2 vCPU Simple plan at $12/mo is the shortest path: no setup fee, no contract, and one month's exposure if it doesn't work out.

👉 open the SpinServers KVM VPS page and confirm the current rate for the 2 vCPU plan
