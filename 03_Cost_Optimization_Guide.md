# 03 - Cost Optimization Guide

## Build World-Class Software for Free (or Almost Free)

> The best infrastructure is the one you do not pay for until
> your revenue justifies it. This guide maps every free and
> low-cost option so your project launches at dollar-zero.

---

## Table of Contents

1. [Cost Philosophy](#1-philosophy)
2. [Free Hosting and Compute](#2-hosting)
3. [Free Databases](#3-databases)
4. [Free CI/CD and DevOps](#4-cicd)
5. [Free Monitoring and Logging](#5-monitoring)
6. [CDN and P2P Strategies](#6-cdn-p2p)
7. [Open Source Stack Recommendations](#7-stack)
8. [Serverless - Pay Only for Usage](#8-serverless)
9. [Cost Monitoring and Alerts](#9-alerts)
10. [Cost Checklist](#10-checklist)

---

## 1. Cost Philosophy

### Zero-Cost Launch Principle
- Start with 100% free tier services.
- Migrate to paid ONLY at hard limits.
- Every paid service must justify cost with revenue or time saved.
- Prefer open-source self-hosted when you have the skill.

### Cost Tiers
    Tier 0: Free forever (hobby / MVP)
    Tier 1: Under $5/month (early traction)
    Tier 2: Under $25/month (growing)
    Tier 3: Under $100/month (scaling)
    Tier 4: Custom (enterprise - negotiate)

---

## 2. Free Hosting and Compute

### Static / Frontend

| Service | Free Tier | Best For |
|---------|-----------|----------|
| Cloudflare Pages | Unlimited sites, 500 builds/mo | Static, SSR |
| Vercel | 100GB BW, serverless functions | Next.js, React |
| Netlify | 100GB BW, 300 build min/mo | JAMstack |
| GitHub Pages | 1GB storage, 100GB BW/mo | Docs, portfolios |
| Surge.sh | Unlimited static sites | Prototypes |

### Backend / Full-Stack

| Service | Free Tier | Best For |
|---------|-----------|----------|
| Render | 750 hrs/mo, spins down | APIs |
| Railway | $5 credit/mo | Full-stack |
| Fly.io | 3 shared VMs, 160GB out | Edge deploy |
| Oracle Cloud | 4 ARM cores, 24GB RAM, ALWAYS free | VPS, anything |
| GCP Free | 1 e2-micro VM, ALWAYS free | Small APIs |
| AWS Free | 750 hrs t2/t3.micro, 12 months | Learning |

### Oracle Cloud: The Secret Weapon
Permanent free VPS (not a trial):
- 4 ARM Ampere A1 cores, 24 GB RAM
- 200 GB block storage, 10 TB outbound
- Use for: databases, Docker, VPN, game servers, anything.

---

## 3. Free Databases

| Service | Free Tier | Type |
|---------|-----------|------|
| Supabase | 500MB, 2 projects | PostgreSQL + Auth |
| Neon | 0.5GB, 191 compute hrs/mo | Serverless PG |
| PlanetScale | 5GB, 1B reads/mo | MySQL (Vitess) |
| Turso | 9GB, 500 DBs | Edge SQLite |
| MongoDB Atlas | 512MB | Document DB |
| Firebase Firestore | 1GB, 50K reads/day | Realtime Doc DB |
| Upstash Redis | 10K cmds/day, 256MB | Serverless Redis |
| Cloudflare D1 | 5GB, 5M reads/day | Edge SQLite |

### Self-Hosted (Free on Oracle VPS)
- PostgreSQL + pgBouncer
- MySQL / MariaDB
- SQLite (underrated for single-server)
- Redis / Valkey
- MinIO (S3-compatible storage)

---

## 4. Free CI/CD and DevOps

| Service | Free Tier |
|---------|-----------|
| GitHub Actions | 2000 min/mo (private), unlimited (public) |
| GitLab CI | 400 min/mo |
| CircleCI | 6000 min/mo |
| Drone CI | Self-hosted, unlimited |
| Docker Hub | 1 private, unlimited public |
| GHCR | Unlimited public, 2GB private |

### IaC (Free / Open Source)
- OpenTofu (Terraform fork, fully open source)
- Ansible (open source, agentless)
- Docker Compose (local and single-server)

---

## 5. Free Monitoring and Logging

| Service | Free Tier |
|---------|-----------|
| Grafana Cloud | 50GB logs, 10K metrics |
| UptimeRobot | 50 monitors, 5-min interval |
| Better Stack | 10 monitors, 3-min interval |
| Sentry | 5K errors/mo |
| PostHog | 1M events/mo |
| Umami | Self-hosted, unlimited |
| Plausible | Self-hosted, unlimited |

---

## 6. CDN and P2P Strategies

### Free CDNs

| Service | Free Tier |
|---------|-----------|
| Cloudflare | Unlimited BW, DDoS, DNS |
| jsDelivr | OSS CDN for npm/GitHub |
| Statically | CDN for GitHub repos |

### P2P / Decentralized (Zero Server Cost)

| Technology | Use Case |
|------------|----------|
| WebTorrent | Browser P2P file sharing |
| IPFS | Decentralized static hosting |
| WebRTC | P2P video/audio/data |
| Gun.js | Decentralized P2P database |
| libp2p | P2P networking layer |

### When P2P Works
- File sharing between users (no storage cost).
- Real-time communication (WebRTC).
- Content distribution with seeding.
- NOT for: sensitive data, guaranteed availability, SEO pages.

---

## 7. Open Source Stack Recommendations

### The Dollar-Zero Full Stack

    Frontend:    React / Svelte / Vue (free)
    Hosting:     Cloudflare Pages (free)
    Backend:     Node / Go / Python on Oracle VPS (free)
    Database:    Supabase PG (free) or self-hosted (free)
    Auth:        Supabase Auth / Lucia Auth (free / OSS)
    Storage:     Cloudflare R2 (free 10GB) / MinIO (free)
    CDN:         Cloudflare (free)
    Email:       Resend (free 3K/mo)
    Search:      Meilisearch self-hosted (free)
    Analytics:   Umami self-hosted (free)
    Monitoring:  UptimeRobot + Grafana Cloud (free)
    CI/CD:       GitHub Actions (free)
    DNS:         Cloudflare (free)
    SSL:         Let's Encrypt / Cloudflare (free)

### Total Monthly Cost: $0.00

---

## 8. Serverless

### Saves Money When
- Traffic is spiky (pay nothing idle).
- No server management desired.
- Functions under 15 minutes.

### Costs MORE When
- Sustained high traffic ($5 VPS wins).
- Long WebSocket connections.
- Heavy computation (per-ms billing).

### Free Tiers

| Service | Free Tier |
|---------|-----------|
| AWS Lambda | 1M requests, 400K GB-sec/mo |
| Cloudflare Workers | 100K requests/day |
| Vercel Functions | 100GB-hours/mo |
| Deno Deploy | 1M requests/mo |
| GCP Functions | 2M requests/mo |

---

## 9. Cost Monitoring and Alerts

1. Billing alerts at 50%, 80%, 100% on EVERY cloud account.
2. Review bills weekly for first 3 months.
3. Tag resources by project and environment.
4. Kill unused resources monthly.
5. Spot/preemptible instances for non-critical workloads (60-90% cheaper).

### Tools
- AWS Cost Explorer, GCP Billing, Azure Cost Management
- Kubecost (K8s), Infracost (IaC estimation in CI)

---

## 10. Cost Checklist

- [ ] Free tier covers current scale?
- [ ] Open-source self-hosted alternative considered?
- [ ] Oracle Cloud Free VPS considered?
- [ ] Compared 3+ alternatives?
- [ ] Cost proportional to revenue?
- [ ] Serverless for spiky workloads?
- [ ] Billing alerts set?
- [ ] Reserved/savings plans for predictable work?
- [ ] Unused resources removed this month?
- [ ] CDN is free (Cloudflare)?
- [ ] SSL is free (Let's Encrypt)?
- [ ] CI/CD within free limits?

---

> The most expensive infrastructure is the one you pay for
> before you have users. Launch free. Scale when you earn it.
