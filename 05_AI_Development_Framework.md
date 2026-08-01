# 05 - AI Development Framework

## The Complete Lifecycle: From Idea to Production to Iteration

> This is the master document. It ties together security (01),
> design (02), cost (03), and platform (04) into a single
> step-by-step framework that any developer or AI agent can
> follow to build ANY project at its absolute peak.

---

## Table of Contents

1. [Framework Overview](#1-framework-overview)
2. [Phase 1 - Discover and Define](#2-phase-1)
3. [Phase 2 - Architect](#3-phase-2)
4. [Phase 3 - Design](#4-phase-3)
5. [Phase 4 - Build](#5-phase-4)
6. [Phase 5 - Test](#6-phase-5)
7. [Phase 6 - Deploy](#7-phase-6)
8. [Phase 7 - Monitor and Iterate](#8-phase-7)
9. [AI Agent Instructions](#9-ai-agent-instructions)
10. [Project Master Checklist](#10-project-master-checklist)

---

## 1. Framework Overview

    +----------+     +----------+     +--------+     +-------+
    | DISCOVER | --> | ARCHITECT| --> | DESIGN | --> | BUILD |
    +----------+     +----------+     +--------+     +-------+
                                                         |
    +----------+     +----------+     +--------+         |
    | ITERATE  | <-- | MONITOR  | <-- | DEPLOY | <-- TEST|
    +----------+     +----------+     +--------+     +---+

Every phase has:
- INPUT: What you need before starting.
- ACTIONS: What to do.
- OUTPUT: What you produce.
- GATES: Criteria to pass before moving to next phase.

---

## 2. Phase 1 - Discover and Define

### INPUT
- Stakeholder requirements (or your own problem statement).
- Target users and their pain points.
- Competitor analysis (minimum 3 competitors).

### ACTIONS
1. Write a one-sentence problem statement.
2. List the top 5 user stories:
   "As a [user type], I want [action] so that [benefit]."
3. Define MVP scope: the SMALLEST thing that delivers value.
4. Identify risks: technical, legal, financial, security.
5. Choose your tech stack (refer to Guide 03 for free options).
6. Define success metrics (KPIs).

### OUTPUT
- Project brief (1 page).
- User stories (5-15 for MVP).
- Tech stack decision document.
- Risk register.

### GATES
- [ ] Problem statement is clear and validated.
- [ ] MVP scope is achievable in 2-4 weeks.
- [ ] Tech stack is chosen and justified.
- [ ] Legal review: no IP conflicts, license compliance checked.

---

## 3. Phase 2 - Architect

### INPUT
- Project brief and user stories from Phase 1.

### ACTIONS
1. Draw system architecture diagram (C4 model).
2. Define data model (ERD or document schema).
3. Design API contracts (OpenAPI spec or tRPC router).
4. Apply security architecture (refer to Guide 01):
   - Threat model (STRIDE) on every component.
   - Define auth flows.
   - Plan encryption at rest and in transit.
   - Secrets management strategy.
5. Plan infrastructure (refer to Guide 03):
   - Free-tier services first.
   - CI/CD pipeline.
   - Monitoring and logging.
6. Define folder structure and coding conventions.

### OUTPUT
- Architecture diagram.
- Data model / schema.
- API specification.
- Security design document.
- Infrastructure plan.

### GATES
- [ ] Architecture reviewed against STRIDE threat model.
- [ ] No secrets in architecture.
- [ ] API contracts defined and type-safe.
- [ ] Infrastructure cost is $0 at MVP stage.
- [ ] Scaling path identified.

---

## 4. Phase 3 - Design

### INPUT
- Architecture and user stories.

### ACTIONS (refer to Guide 02)
1. Wireframes for every screen (low-fidelity first).
2. Design tokens (colors, typography, spacing).
3. Component library (buttons, inputs, cards, modals, nav).
4. High-fidelity mockups for key flows.
5. Accessibility from the start:
   - Contrast ratios verified.
   - Keyboard navigation planned.
   - Screen reader annotations.
6. Empty states, error states, loading states.
7. Micro-interactions and transitions.
8. Responsive layouts: 320px, 768px, 1024px, 1440px.

### OUTPUT
- Wireframes (all screens).
- Design system (tokens + components).
- High-fidelity mockups.
- Accessibility annotations.

### GATES
- [ ] All screens have wireframes.
- [ ] Design tokens documented.
- [ ] Contrast ratios pass WCAG AA.
- [ ] Keyboard flow tested.
- [ ] Empty, error, loading states designed.
- [ ] Responsive breakpoints defined.

---

## 5. Phase 4 - Build

### INPUT
- Architecture, API spec, designs.

### ACTIONS
1. Set up repository:
   - README.md, .gitignore, pre-commit hooks (linter, gitleaks).
   - CI pipeline: lint, test, build, security scan.
2. Implement in order:
   a. Data models and migrations.
   b. API endpoints (with input validation).
   c. Authentication and authorization.
   d. Core business logic.
   e. UI components.
   f. Page composition and routing.
   g. Micro-interactions and polish.
3. Security during build (Guide 01):
   - Parameterized queries everywhere.
   - Input validation on every endpoint.
   - Rate limiting on public endpoints.
   - Security headers configured.
   - gitleaks on every commit.
4. Code quality:
   - Unit tests for business logic (>80% coverage).
   - Integration tests for API endpoints.
   - Linting and formatting enforced in CI.

### OUTPUT
- Working application code.
- Test suite.
- CI/CD pipeline.

### GATES
- [ ] All CI checks pass.
- [ ] Test coverage > 80% on business logic.
- [ ] gitleaks scan clean.
- [ ] Dependency scan clean.
- [ ] API matches spec.
- [ ] UI matches designs.

---

## 6. Phase 5 - Test

### INPUT
- Built application.

### ACTIONS
1. Unit tests: business logic, utilities, validators.
2. Integration tests: API endpoints, database operations.
3. E2E tests: critical user flows (Playwright / Cypress).
4. Security testing:
   - OWASP ZAP automated scan.
   - Manual: SQLi, XSS, CSRF, IDOR on every input.
   - Auth bypass attempts.
   - Authorization: access other users' data.
5. Performance testing:
   - Lighthouse: 90+ all categories.
   - Load testing: k6 (100 concurrent users).
6. Accessibility testing:
   - axe DevTools scan.
   - Keyboard-only navigation.
   - Screen reader test.
7. Cross-platform testing (Guide 04):
   - Web: Chrome, Firefox, Safari, Edge.
   - Mobile: Android, iOS.
   - Desktop: Windows, Linux.

### OUTPUT
- Test reports.
- Bug list with severity.
- Performance benchmarks.
- Accessibility audit.

### GATES
- [ ] Zero critical/high bugs.
- [ ] OWASP ZAP: no high-risk findings.
- [ ] Lighthouse: 90+ all categories.
- [ ] All E2E tests pass.
- [ ] p95 response < 500ms at 100 users.
- [ ] Zero WCAG AA violations.

---

## 7. Phase 6 - Deploy

### INPUT
- Tested application.

### ACTIONS
1. Infrastructure (Guide 03):
   - Provision free-tier services.
   - DNS (Cloudflare). SSL (Let's Encrypt).
   - Secrets via manager.
2. Deployment:
   - Web: Cloudflare Pages / Vercel.
   - API: Render / Fly.io / Oracle VPS.
   - DB: Supabase / Neon / self-hosted.
3. Post-deploy:
   - Smoke test all flows.
   - Verify monitoring and alerts.
   - Verify backups.
   - Check error tracking.
4. Distribution (Guide 04):
   - Android: Play Store.
   - Windows: MSIX + GitHub Releases.
   - Linux: Flathub + Snap + GitHub Releases.

### OUTPUT
- Live production application.
- Monitoring dashboards.
- Backup schedule.

### GATES
- [ ] Smoke test passed.
- [ ] Monitoring alerts configured.
- [ ] Backups verified.
- [ ] SSL valid and auto-renewing.
- [ ] Cost within budget.

---

## 8. Phase 7 - Monitor and Iterate

### INPUT
- Live application with monitoring.

### ACTIONS
1. Monitor daily: errors, uptime, response times, analytics.
2. Collect feedback: in-app form, store reviews, support tickets.
3. Iterate weekly: top 3 complaints, top 3 errors, ship fixes.
4. Iterate monthly: security updates, cost review, performance review.
5. Iterate quarterly: full security audit, accessibility audit, user research.

### OUTPUT
- Weekly changelog.
- Monthly security and cost report.
- Quarterly audit reports.

### GATES (ongoing)
- [ ] Uptime > 99.5% monthly.
- [ ] Zero unresolved critical bugs.
- [ ] Dependencies updated within 7 days of patch.
- [ ] Feedback reviewed weekly.
- [ ] Cost reviewed monthly.

---

## 9. AI Agent Instructions

### System Prompt for AI Coding Assistants

    ROLE: You are a senior staff engineer building a production-grade system.

    RULES:
    1. Before writing code, read all 5 knowledge base files.
    2. Apply Guide 01 (Security) to EVERY line of code.
       - No hardcoded secrets. Parameterized queries. Input validation.
    3. Apply Guide 02 (UI/UX) to EVERY user-facing element.
       - WCAG AA. Keyboard navigable. Responsive. All states designed.
    4. Apply Guide 03 (Cost) to EVERY infrastructure decision.
       - Free tier first. Justify any paid service.
    5. Apply Guide 04 (Platform) for multi-target builds.
       - Native UX per platform. Shared logic, native UI.
    6. Follow Guide 05 phase by phase. Do not skip gates.
    7. Write tests alongside code. Not after. Now.
    8. Explain decisions. Cite the guide and section.

### Debugging Protocol

1. Reproduce: write a failing test first.
2. Diagnose: read error, trace stack, check logs.
3. Root cause: find WHY, not just WHAT.
4. Fix: minimal change resolving root cause.
5. Verify: failing test passes. Full suite green.
6. Prevent: add test or lint rule so bug class cannot recur.

### Code Review Protocol

1. Security: injection, auth bypass, secret exposure?
2. Correctness: edge cases, nulls, errors handled?
3. Performance: N+1 queries, unnecessary loops, memory leaks?
4. Readability: understandable in 5 minutes?
5. Tests: coverage for this code? Edge cases?
6. Accessibility: keyboard-accessible? Screen-reader friendly?

---

## 10. Project Master Checklist

### Security (Guide 01)
- [ ] STRIDE threat model completed
- [ ] Zero secrets in source code
- [ ] TLS 1.3 enforced
- [ ] MFA available
- [ ] OWASP Top 10 mitigated
- [ ] Dependencies scanned
- [ ] Incident response plan documented

### Design (Guide 02)
- [ ] WCAG 2.2 AA compliant
- [ ] Responsive: 320px to 1440px
- [ ] Dark mode supported
- [ ] All states designed (loading, error, empty)
- [ ] Micro-interactions implemented
- [ ] Feedback mechanism integrated

### Cost (Guide 03)
- [ ] All services on free tier (or justified)
- [ ] Billing alerts configured
- [ ] No unused resources
- [ ] CDN and SSL are free

### Platform (Guide 04)
- [ ] Web: PWA, Lighthouse 90+
- [ ] Android: Play Store (if applicable)
- [ ] Windows: MSIX (if applicable)
- [ ] Linux: AppImage + Flatpak (if applicable)
- [ ] Auto-update in place

### Process (Guide 05)
- [ ] All 7 phases completed
- [ ] All phase gates passed
- [ ] CI/CD automated
- [ ] Monitoring active
- [ ] Backups verified
- [ ] Documentation complete

---

> A project is never truly "done."
> But with this framework, it is always in a shippable state.
> Ship early. Ship often. Improve forever.
