# 01 - Cybersecurity Guide

## The Assume-Breach Security Playbook

> If you build software assuming no one will ever attack it,
> you have already lost. This guide makes sure that even if
> everything goes wrong, the damage is contained.

---

## Table of Contents

1. [Core Principles](#1-core-principles)
2. [Threat Modeling](#2-threat-modeling)
3. [Authentication and Authorization](#3-authentication-and-authorization)
4. [Encryption - Classical and Quantum-Resistant](#4-encryption)
5. [Secrets Management](#5-secrets-management)
6. [OWASP Top 10 - 2025 Defense](#6-owasp-top-10)
7. [Supply Chain Security](#7-supply-chain-security)
8. [Infrastructure Hardening](#8-infrastructure-hardening)
9. [Incident Response](#9-incident-response)
10. [Security Checklist](#10-security-checklist)

---

## 1. Core Principles

### Zero Trust Architecture
- Never trust, always verify. Every request is authenticated.
- No implicit trust based on network location.
- Micro-segmentation: each service has its own security boundary.
- Least privilege: every identity gets ONLY the permissions it needs.

### Defense in Depth

    Layer 1: Network (firewalls, WAF, DDoS protection)
    Layer 2: Application (input validation, auth, rate limiting)
    Layer 3: Data (encryption at rest, tokenization, masking)
    Layer 4: Infrastructure (OS hardening, container isolation)
    Layer 5: Monitoring (SIEM, anomaly detection, alerting)

### Assume Breach
- Design so a compromised component cannot compromise everything.
- Encrypt data so even if the server is stolen, data is unreadable.
- Rotate keys frequently. Limit blast radius.

---

## 2. Threat Modeling

Use STRIDE for every feature:

| Threat | Question | Mitigation |
|--------|----------|------------|
| Spoofing | Can someone pretend to be another user? | MFA, certificate auth |
| Tampering | Can data be modified in transit? | TLS 1.3, HMAC, signatures |
| Repudiation | Can a user deny their actions? | Audit logs, signed transactions |
| Info Disclosure | Can secrets leak? | Encryption, access control, DLP |
| Denial of Service | Can the system be overwhelmed? | Rate limiting, CDN, auto-scaling |
| Elevation of Privilege | Can a user gain admin? | RBAC, ABAC, least privilege |

Action: Run STRIDE on every API endpoint, data store, and user flow.

---

## 3. Authentication and Authorization

### Authentication
- OAuth 2.0 + OpenID Connect (never roll your own).
- MFA: TOTP or WebAuthn/FIDO2 hardware keys.
- Passwords: min 12 chars, check HaveIBeenPwned, hash with Argon2id.
- Sessions: 256-bit random tokens, HttpOnly + Secure + SameSite cookies.
- Lockout after 5 failed attempts with exponential backoff.

### Authorization
- RBAC for simple systems. ABAC for complex.
- Validate on EVERY request server-side. Never trust the client.
- Short-lived JWTs (15 min) + rotated refresh tokens (7 days, single-use).
- Resource-level permissions, not just route-level.

---

## 4. Encryption

### In Transit
- TLS 1.3 minimum. Disable 1.0 and 1.1.
- HSTS: max-age=63072000; includeSubDomains; preload
- Certificate pinning for mobile apps.

### At Rest
- AES-256-GCM for symmetric encryption.
- Encrypt databases (TDE), disks (LUKS, BitLocker), backups.
- App-level encryption for sensitive fields.

### Quantum-Resistant (Post-Quantum)

NIST finalized these in 2024. Start migrating NOW:

| Algorithm | Use Case | Replaces |
|-----------|----------|----------|
| CRYSTALS-Kyber (ML-KEM) | Key exchange | RSA, ECDH |
| CRYSTALS-Dilithium (ML-DSA) | Signatures | RSA sig, ECDSA |
| SPHINCS+ (SLH-DSA) | Hash-based signatures | Backup scheme |

### Rules
- NEVER hardcode keys. Use KMS (Vault, AWS KMS, GCP KMS).
- Rotate keys every 90 days. Separate keys per environment.
- Key versioning for decryption during rotation.

---

## 5. Secrets Management

1. NO secrets in source code. EVER.
2. NO secrets in env vars on shared systems.
3. Use HashiCorp Vault, AWS Secrets Manager, Azure Key Vault.
4. CI/CD: OIDC federation, not long-lived tokens.
5. Scan commits with gitleaks or trufflehog (pre-commit hooks).
6. If committed, it is COMPROMISED. Rotate immediately.

### .gitignore must include:
    .env
    *.pem
    *.key
    *.p12
    *.pfx
    secrets/
    credentials/

---

## 6. OWASP Top 10

| # | Risk | Key Defense |
|---|------|-------------|
| A01 | Broken Access Control | Server-side enforcement, deny by default |
| A02 | Crypto Failures | TLS 1.3, AES-256, no custom crypto |
| A03 | Injection | Parameterized queries, ORM, validation |
| A04 | Insecure Design | Threat modeling, secure patterns |
| A05 | Misconfiguration | Hardened defaults, disable unused |
| A06 | Vulnerable Components | Dependabot, Snyk, Trivy |
| A07 | Auth Failures | MFA, Argon2id, session management |
| A08 | Data Integrity | Signed updates, SRI for CDN |
| A09 | Logging Failures | Centralized logs, no PII in logs |
| A10 | SSRF | Allowlist URLs, block internal IPs |

---

## 7. Supply Chain Security

- Lock dependencies (package-lock.json, go.sum, Cargo.lock).
- Dependabot / Renovate for auto-updates.
- Trivy / Grype in CI for container scanning.
- Verify package signatures (npm audit signatures, pip --require-hashes).
- SLSA framework for build provenance.
- Pin base images by digest, not tag.

---

## 8. Infrastructure Hardening

### Server
- Disable root SSH. Key-based auth only.
- Firewall: allow only required ports.
- Auto security updates (unattended-upgrades).
- Non-root service users. SELinux or AppArmor.

### Containers
- Non-root user. Distroless/alpine images. Read-only FS.
- Drop all capabilities, add only needed. No privileged.
- Scan in CI (Trivy).

### Kubernetes
- Network policies: deny all, allow specific.
- Pod Security Standards: restricted.
- RBAC least privilege. External secrets operator.
- Audit logging enabled.

---

## 9. Incident Response

### Before
1. Document IRP. Define roles.
2. Centralized logging (ELK, Loki, CloudWatch).
3. Anomaly alerts. Quarterly tabletop exercises.

### During
1. DETECT: Identify scope.
2. CONTAIN: Isolate affected systems.
3. ERADICATE: Remove access, patch vulnerability.
4. RECOVER: Restore from clean backups, rotate ALL credentials.
5. LEARN: Post-mortem within 48 hours.

---

## 10. Security Checklist

- [ ] All secrets in secrets manager, not in code
- [ ] TLS 1.3 enforced everywhere
- [ ] MFA for authentication
- [ ] Server-side authorization on every endpoint
- [ ] Input validation on all user data
- [ ] Parameterized queries (no SQL concatenation)
- [ ] Dependencies scanned and updated
- [ ] Container images scanned
- [ ] Rate limiting on public endpoints
- [ ] Security headers (CSP, HSTS, X-Frame-Options)
- [ ] Logging captures security events (no PII)
- [ ] Backups encrypted and tested
- [ ] Incident response plan documented
- [ ] gitleaks in pre-commit hooks
- [ ] CORS: specific origins (not wildcard in prod)

---

> Security is not a feature you add at the end.
> It is a constraint you design with from the first line of code.
