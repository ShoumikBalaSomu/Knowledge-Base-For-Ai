# 03 - Cost Optimization Guide

## Build Maximum Value at Minimum Cost

> "The best infrastructure is the one you do not have to pay for."

---

## Table of Contents

1. [Cost Philosophy](#1-cost-philosophy)
2. [Free Hosting and Infrastructure](#2-free-hosting-and-infrastructure)
3. [Free-Tier Cloud Services](#3-free-tier-cloud-services)
4. [P2P and Distributed Architecture](#4-p2p-and-distributed-architecture)
5. [Open-Source Toolchain](#5-open-source-toolchain)
6. [Serverless Architecture](#6-serverless-architecture)
7. [Database Cost Optimization](#7-database-cost-optimization)
8. [CI/CD on a Budget](#8-cicd-on-a-budget)
9. [Monitoring and Observability (Free)](#9-monitoring-and-observability-free)
10. [Domain and DNS (Low Cost)](#10-domain-and-dns-low-cost)
11. [Cost Optimization Checklist](#11-cost-optimization-checklist)

---

## 1. Cost Philosophy

### 1.1 The Zero-Cost Mindset

Before spending any money, ask:

1. Can this be done with free-tier services?
2. Can this be self-hosted on free infrastructure?
3. Can this be replaced with an open-source alternative?
4. Can this be eliminated entirely (do we really need it)?
5. Can this be shared with other projects (multi-tenancy)?

### 1.2 Cost Tiers

| Tier | Budget | Strategy |
|------|--------|----------|
| Zero | 0 USD/month | Free tiers only, open-source, self-hosted |
| Minimal | Under 5 USD/month | Free tiers + one paid service |
| Lean | 5-20 USD/month | Free tiers + strategic paid services |
| Growth | 20-100 USD/month | Paid services with free-tier fallbacks |
| Scale | 100+ USD/month | Optimized paid infrastructure |

### 1.3 Cost Tracking

- Set up billing alerts at 50%, 80%, 100% of budget
- Review cloud bills weekly during development
- Tag all resources by project and environment
- Use cost estimation tools before provisioning
- Calculate cost-per-user to understand unit economics

---

## 2. Free Hosting and Infrastructure

### 2.1 Static Site / Frontend Hosting (100% Free)

| Service | Free Tier | Best For |
|---------|-----------|----------|
| Cloudflare Pages | Unlimited sites, unlimited bandwidth, 500 builds/month | Static sites, SSR frameworks |
| Vercel | 100GB bandwidth, unlimited sites | Next.js, React, Svelte |
| Netlify | 100GB bandwidth, 300 build min/month | JAMstack, static sites |
| GitHub Pages | 1GB storage, 100GB bandwidth/month | Documentation, portfolios |
| GitLab Pages | Unlimited (self-hosted runner) | GitLab projects |
| Surge.sh | Unlimited sites | Quick prototyping |
| Render | 100GB bandwidth | Static sites + web services |

### 2.2 Backend / API Hosting (Free Tier)

| Service | Free Tier | Limitations |
|---------|-----------|-------------|
| Railway | 5 USD credit/month | Sleeps after inactivity |
| Render | 750 hours/month | Sleeps after 15 min idle |
| Fly.io | 3 shared VMs (256MB RAM) | Limited regions |
| Koyeb | 1 nano instance | 512MB RAM, 1 CPU |
| Oracle Cloud Free Tier | 2 AMD VMs + 4 ARM VMs (24GB RAM) | Always free, best value |
| Google Cloud Run | 2M requests/month | 512MB RAM, 1 CPU |
| AWS Lambda | 1M requests/month | 15 min max execution |
| Azure Functions | 1M requests/month | Consumption plan |
| Deno Deploy | 1M requests/month | Edge functions only |
| Val.town | Free tier | Server-side JavaScript |

### 2.3 Full VPS (Free)

| Provider | Free Tier | Specs |
|----------|-----------|-------|
| Oracle Cloud | Always Free | 4 ARM cores, 24GB RAM, 200GB storage |
| Google Cloud | 12 months | e2-micro, 30GB HDD |
| AWS | 12 months | t2.micro/t3.micro, 30GB EBS |
| Azure | 12 months | B1s, 30GB managed disk |
| Fly.io | Always Free | 3 shared VMs, 256MB each |

Oracle Cloud Always Free is the best free VPS offering available.

### 2.4 Container Hosting (Free)

| Service | Free Tier |
|---------|-----------|
| Docker Hub | 1 private repo, unlimited public |
| GitHub Container Registry | Unlimited (with GitHub free) |
| GitLab Container Registry | Unlimited (with GitLab free) |
| Quay.io | Unlimited public repos |

---

## 3. Free-Tier Cloud Services

### 3.1 Database (Free)

| Service | Free Tier | Type |
|---------|-----------|------|
| Supabase | 500MB, 2 projects | PostgreSQL + Auth + Storage |
| PlanetScale | 5GB, 1B row reads/month | MySQL (Vitess) |
| Neon | 0.5GB, autosuspend | PostgreSQL (serverless) |
| Turso | 9GB, 500 DBs | SQLite (edge) |
| MongoDB Atlas | 512MB cluster | Document DB |
| Firebase Firestore | 1GB, 50k reads/day | Document DB |
| Upstash Redis | 10k commands/day | Redis (serverless) |
| Upstash Kafka | 10k messages/day | Message queue |
| CockroachDB Serverless | 10GiB storage | Distributed SQL |
| Xata | 3GB, unlimited projects | PostgreSQL + search |

### 3.2 Authentication (Free)

| Service | Free Tier |
|---------|-----------|
| Supabase Auth | 50k MAU |
| Firebase Auth | 50k MAU (phone: 10k) |
| Clerk | 10k MAU |
| Auth0 | 7,500 MAU |
| Ory (self-hosted) | Unlimited (open-source) |
| Keycloak (self-hosted) | Unlimited (open-source) |
| SuperTokens (self-hosted) | Unlimited (open-source) |

### 3.3 Storage and CDN (Free)

| Service | Free Tier |
|---------|-----------|
| Cloudflare R2 | 10GB storage, 10M reads/month |
| Cloudflare CDN | Unlimited bandwidth |
| Backblaze B2 | 10GB storage, 1GB download/day |
| Firebase Storage | 5GB, 1GB/day download |
| Supabase Storage | 1GB |
| Imgur API | Unlimited image hosting |
| jsDelivr | Unlimited CDN for open-source |

### 3.4 Email (Free)

| Service | Free Tier |
|---------|-----------|
| Resend | 3,000 emails/month |
| Brevo (Sendinblue) | 300 emails/day |
| Mailgun | 1,000 emails/month (trial) |
| Gmail SMTP | 500 emails/day |
| AWS SES | 62,000 emails/month (from EC2) |

### 3.5 Search (Free)

| Service | Free Tier |
|---------|-----------|
| Meilisearch (self-hosted) | Unlimited (open-source) |
| Typesense (self-hosted) | Unlimited (open-source) |
| Algolia | 10k records, 10k searches/month |
| Elasticsearch (self-hosted) | Unlimited (open-source) |

---

## 4. P2P and Distributed Architecture

### 4.1 When to Use P2P

P2P architecture eliminates server costs entirely for:

- File sharing and distribution
- Real-time communication (chat, video)
- Content delivery (distributed CDN)
- Collaborative editing
- IoT device networks
- Blockchain and distributed ledgers

### 4.2 P2P Technologies

| Technology | Use Case | Library |
|-----------|----------|---------|
| WebRTC | Real-time audio/video/data | peerjs, simple-peer |
| WebTorrent | Browser torrent client | webtorrent |
| IPFS | Distributed file storage | js-ipfs, kubo |
| libp2p | P2P networking stack | js-libp2p, go-libp2p |
| BitTorrent | Large file distribution | libtorrent, WebTorrent |
| Matrix | Decentralized messaging | matrix-js-sdk |
| Nostr | Decentralized social | nostr-tools |
| Gun.js | P2P database | gun |
| Hypercore | Append-only logs | hypercore |
| Holepunch | NAT traversal | holepunch |

### 4.3 Hybrid Architecture (Best of Both Worlds)

Combine P2P with minimal server infrastructure:

1. Use a free signaling server (WebSocket on free tier)
2. Peers connect directly via WebRTC/libp2p
3. Use IPFS for content-addressed storage
4. Fall back to server relay when P2P fails
5. Use DHT for peer discovery (no central registry)

Cost: Near zero for any number of users (costs do not scale with users)

### 4.4 Torrent Technology for Distribution

For distributing large files (software, datasets, media):

- Create torrent files for releases
- Use WebTorrent for browser-based downloads
- Seed from free VPS (Oracle Cloud)
- Users seed to each other (reduces server load to zero)
- Magnet links for easy sharing
- Trackers: Use public trackers or DHT (trackerless)

---

## 5. Open-Source Toolchain

### 5.1 Development Tools (All Free)

| Category | Tool | Alternative |
|----------|------|-------------|
| Code Editor | VS Code | Neovim, Zed |
| Version Control | Git + GitHub | GitLab, Gitea (self-hosted) |
| Package Manager | npm/pnpm/yarn | pip, cargo, go mod |
| Container | Docker + Podman | LXC, Buildah |
| Orchestration | Kubernetes (k3s) | Docker Compose, Nomad |
| API Testing | Bruno, Hoppscotch | Insomnia, curl |
| Database GUI | DBeaver, pgAdmin | TablePlus (limited free) |
| Design | Figma (free tier) | Penpot (open-source) |
| Project Management | GitHub Projects | Plane, AppFlowy |
| Documentation | MkDocs, Docusaurus | GitBook (free tier) |
| Diagrams | Excalidraw, draw.io | Mermaid.js |

### 5.2 Self-Hosted Alternatives to Paid Services

| Paid Service | Free Self-Hosted Alternative |
|-------------|------------------------------|
| Jira | Plane, OpenProject, Taiga |
| Slack | Mattermost, Rocket.Chat, Zulip |
| GitHub Copilot | Continue.dev + local LLM (Ollama) |
| Vercel Analytics | Umami, Plausible (self-hosted) |
| Sentry | GlitchTip, self-hosted Sentry |
| Datadog | Grafana + Prometheus + Loki |
| Auth0 | Keycloak, Ory, SuperTokens |
| Algolia | Meilisearch, Typesense |
| Twilio | FreeSWITCH, Asterisk |
| Stripe (for OSS) | LemonSqueezy, Paddle |

### 5.3 AI Tools (Free)

| Tool | Free Tier | Use |
|------|-----------|-----|
| Ollama | Unlimited (local) | Run LLMs locally |
| Hugging Face | Unlimited inference API | ML models |
| Google AI Studio | 15 RPM free | Gemini API |
| Groq | Free tier | Fast LLM inference |
| Together AI | Free credits | Open model inference |
| GitHub Copilot | Free for students/OSS | Code completion |

---

## 6. Serverless Architecture

### 6.1 When Serverless Saves Money

Serverless is cost-effective when:

- Traffic is unpredictable or spiky
- You have idle periods (no pay for idle)
- You are starting out (zero upfront cost)
- You want to avoid server management
- Workloads are event-driven

### 6.2 Serverless Stack (Zero Cost)

| Layer | Service | Free Tier |
|-------|---------|-----------|
| Functions | Cloudflare Workers | 100k requests/day |
| Functions | Deno Deploy | 1M requests/month |
| Functions | Vercel Functions | 100GB-hours/month |
| Database | Turso / Neon | Generous free tier |
| Cache | Upstash Redis | 10k commands/day |
| Queue | Upstash Kafka | 10k messages/day |
| Storage | Cloudflare R2 | 10GB |
| Auth | Supabase Auth | 50k MAU |
| Cron | GitHub Actions | 2000 min/month |

### 6.3 Edge Computing (Free)

Run code at the edge, close to users, for free:

- Cloudflare Workers: 100k requests/day free
- Deno Deploy: 1M requests/month free
- Vercel Edge Functions: Included in free tier
- Fastly Compute: Free trial credits

Benefits: Lower latency, no server management, auto-scaling, zero idle cost

---

## 7. Database Cost Optimization

### 7.1 Choose the Right Database

| Use Case | Best Free Option | Why |
|----------|-----------------|-----|
| Relational data | Supabase (PostgreSQL) | 500MB free, auth included |
| Document store | MongoDB Atlas | 512MB free cluster |
| Key-value cache | Upstash Redis | Serverless, per-request pricing |
| Time-series | InfluxDB Cloud | 30-day retention free |
| Search engine | Meilisearch (self-hosted) | Unlimited, open-source |
| Embedded/local | SQLite / Turso | Zero infrastructure cost |
| Graph data | Neo4j Aura | 200k nodes free |
| Vector/AI | Qdrant Cloud | 1GB free |

### 7.2 Database Optimization Tips

- Index properly (analyze slow queries)
- Use connection pooling (PgBouncer, Supavisor)
- Cache frequent queries (Redis, in-memory)
- Archive old data to cold storage
- Use read replicas for heavy read workloads
- Implement query result caching at application level
- Use pagination (never SELECT all)
- Denormalize where reads vastly outnumber writes

---

## 8. CI/CD on a Budget

### 8.1 Free CI/CD Options

| Service | Free Tier | Best For |
|---------|-----------|----------|
| GitHub Actions | 2000 min/month (Linux) | GitHub repos |
| GitLab CI | 400 min/month (shared runners) | GitLab repos |
| CircleCI | 6000 min/month | Complex pipelines |
| Drone CI | Unlimited (self-hosted) | Self-hosted, Docker-native |
| Woodpecker CI | Unlimited (self-hosted) | Lightweight, self-hosted |
| Act | Unlimited (local) | Local testing of GH Actions |

### 8.2 Optimize CI/CD Costs

- Cache dependencies between runs
- Use smaller container images for build
- Run tests in parallel
- Skip CI for documentation-only changes
- Use self-hosted runners on free VPS (Oracle Cloud)
- Limit build matrix to necessary combinations
- Use conditional steps (only deploy on main branch)

---

## 9. Monitoring and Observability (Free)

### 9.1 Free Monitoring Stack

| Layer | Tool | Free Tier |
|-------|------|-----------|
| Uptime | UptimeRobot | 50 monitors, 5-min interval |
| Uptime | Better Stack | 10 monitors free |
| APM | Grafana Cloud | 10k series, 50GB logs |
| Error Tracking | Sentry | 5k errors/month |
| Error Tracking | GlitchTip (self-hosted) | Unlimited |
| Analytics | Umami (self-hosted) | Unlimited |
| Analytics | Plausible (self-hosted) | Unlimited |
| Logging | Grafana Loki | 50GB/month (Grafana Cloud) |
| Metrics | Prometheus + Grafana | Unlimited (self-hosted) |
| Status Page | Instatus | 1 page free |

### 9.2 Self-Hosted Monitoring (Free VPS)

On Oracle Cloud free tier (4 ARM cores, 24GB RAM):

- Prometheus (metrics collection)
- Grafana (dashboards)
- Loki (log aggregation)
- Alertmanager (alerting)
- Node Exporter (system metrics)
- cAdvisor (container metrics)

Total cost: 0 USD/month

---

## 10. Domain and DNS (Low Cost)

### 10.1 Affordable Domain Registrars

| Registrar | Cheapest TLD | Price |
|-----------|-------------|-------|
| Cloudflare Registrar | .com | Around 10 USD/year (at-cost) |
| Porkbun | .com | Around 9 USD/year |
| Namecheap | .com | Around 9 USD/year (first year) |
| Cloudflare | .dev | Around 12 USD/year |
| Freenom | .tk, .ml, .ga | FREE (limited) |
| is-a.dev | .is-a.dev subdomain | FREE (for developers) |
| js.org | .js.org subdomain | FREE (for JS projects) |

### 10.2 Free DNS and SSL

- Cloudflare DNS: Free, fastest global DNS
- Let us Encrypt: Free SSL certificates (auto-renewal)
- Caddy: Automatic HTTPS (built-in Let us Encrypt)
- certbot: Free certificate management

### 10.3 Free Subdomain Options

For projects that do not need a custom domain:

- username.github.io (GitHub Pages)
- project.vercel.app (Vercel)
- project.netlify.app (Netlify)
- project.pages.dev (Cloudflare Pages)
- project.fly.dev (Fly.io)
- project.up.railway.app (Railway)

---

## 11. Cost Optimization Checklist

### Architecture Decisions
- Chose serverless/static where possible
- Used P2P for file distribution
- Selected free-tier services for all components
- Designed for horizontal scaling (add free instances)
- Implemented caching to reduce API calls
- Used CDN for all static assets

### Development
- Used open-source tools exclusively
- Self-hosted alternatives for paid services
- Local development with Docker (no cloud costs)
- Used free AI tools (Ollama, Hugging Face)
- Automated everything (reduce human time cost)

### Deployment
- Static hosting on Cloudflare Pages (free)
- API on Cloudflare Workers / Deno Deploy (free)
- Database on Supabase / Turso (free)
- Auth on Supabase Auth (free)
- Storage on Cloudflare R2 (free)
- CI/CD on GitHub Actions (free)
- Monitoring on UptimeRobot + Sentry (free)
- SSL via Cloudflare / Let us Encrypt (free)

### Ongoing
- Review cloud bills monthly
- Right-size resources quarterly
- Remove unused resources immediately
- Use auto-scaling to match demand
- Cache aggressively to reduce compute
- Monitor cost-per-user metric

---

## Cost Comparison: Traditional vs Optimized

| Component | Traditional Cost | Optimized Cost | Savings |
|-----------|-----------------|----------------|---------|
| Hosting (VPS) | 20-80 USD/month | 0 USD (Cloudflare/Oracle) | 100% |
| Database | 25-150 USD/month | 0 USD (Supabase/Turso) | 100% |
| CDN | 10-50 USD/month | 0 USD (Cloudflare) | 100% |
| SSL Certificate | 0-200 USD/year | 0 USD (Let us Encrypt) | 100% |
| Email Service | 15-50 USD/month | 0 USD (Resend free) | 100% |
| Monitoring | 20-100 USD/month | 0 USD (self-hosted) | 100% |
| CI/CD | 10-50 USD/month | 0 USD (GitHub Actions) | 100% |
| Auth Service | 25-100 USD/month | 0 USD (Supabase Auth) | 100% |
| Total (startup) | 125-680 USD/month | 0 USD/month | 100% |

---

## References

- Cloudflare Pages: https://pages.cloudflare.com/
- Oracle Cloud Free Tier: https://www.oracle.com/cloud/free/
- Supabase: https://supabase.com/
- Vercel: https://vercel.com/
- Fly.io: https://fly.io/
- Free for Dev: https://free-for.dev/
- Awesome Self-Hosted: https://github.com/awesome-selfhosted/awesome-selfhosted

---

*Last Updated: August 2026*
*Version: 2.0.0*
*Author: Shoumik Bala Somu*
