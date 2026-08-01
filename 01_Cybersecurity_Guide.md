# 01 - Cybersecurity Guide

## The Definitive Security Hardening Reference

> "Security is not a feature. It is a foundation."

---

## Table of Contents

1. [Threat Modeling](#1-threat-modeling)
2. [Zero-Trust Architecture](#2-zero-trust-architecture)
3. [Encryption Standards](#3-encryption-standards)
4. [Input Validation and Sanitization](#4-input-validation-and-sanitization)
5. [Authentication and Authorization](#5-authentication-and-authorization)
6. [API Security](#6-api-security)
7. [Dependency Security](#7-dependency-security)
8. [Infrastructure Security](#8-infrastructure-security)
9. [Incident Response](#9-incident-response)
10. [Legal Compliance](#10-legal-compliance)
11. [Security Checklist](#11-security-checklist)

---

## 1. Threat Modeling

### 1.1 STRIDE Analysis

Every project MUST undergo STRIDE threat modeling before development begins:

| Threat | Category | Mitigation |
|--------|----------|------------|
| Spoofing | Identity | Multi-factor authentication, certificate pinning |
| Tampering | Integrity | Digital signatures, HMAC, checksums |
| Repudiation | Non-repudiation | Audit logs, blockchain anchoring |
| Information Disclosure | Confidentiality | Encryption at rest and in transit |
| Denial of Service | Availability | Rate limiting, CDN, auto-scaling |
| Elevation of Privilege | Authorization | Least privilege, RBAC, ABAC |

### 1.2 Attack Surface Mapping

Before writing any code, map every entry point:

- Network endpoints (APIs, webhooks, sockets)
- User inputs (forms, file uploads, URL parameters)
- Third-party integrations (OAuth providers, payment gateways)
- Internal services (message queues, microservice calls)
- Build pipeline (CI/CD secrets, artifact registries)

### 1.3 Threat Intelligence Integration

Stay current with the latest threats:

- Subscribe to CISA KEV (Known Exploited Vulnerabilities) catalog
- Monitor OWASP Top 10 updates (latest: 2025 revision)
- Track CVE databases (NVD, MITRE)
- Follow security advisories for all dependencies
- Participate in bug bounty programs for awareness

---

## 2. Zero-Trust Architecture

### 2.1 Core Principles

Zero Trust means: Never trust, always verify.

1. Verify Explicitly - Authenticate and authorize based on all available data points
2. Use Least Privilege Access - Limit user access with Just-In-Time and Just-Enough-Access
3. Assume Breach - Minimize blast radius, segment access, encrypt all data

### 2.2 Implementation Pattern

Every request must pass through:

1. Identity verification (Who are you?)
2. Device compliance (Is your device trusted?)
3. Context evaluation (Where, when, how?)
4. Risk assessment (Is this behavior normal?)
5. Policy enforcement (Are you allowed?)
6. Continuous monitoring (Are you still allowed?)

### 2.3 Network Segmentation

- Use micro-segmentation for all services
- Implement service mesh (Istio, Linkerd) for east-west traffic
- Deploy Web Application Firewall (WAF) for north-south traffic
- Use mutual TLS (mTLS) between all internal services
- Implement network policies (Kubernetes NetworkPolicy, security groups)

### 2.4 Developer Access Control

Even developers must not have unrestricted access:

- Use short-lived credentials (max 1 hour)
- Implement Privileged Access Management (PAM)
- All production access requires approval workflow
- Session recording for all privileged operations
- Break-glass procedures with automatic revocation

---

## 3. Encryption Standards

### 3.1 Data in Transit

| Protocol | Version | Configuration |
|----------|---------|---------------|
| TLS | 1.3 minimum | Disable TLS 1.0, 1.1, 1.2 fallback |
| Cipher Suites | AEAD only | TLS_AES_256_GCM_SHA384, TLS_CHACHA20_POLY1305_SHA256 |
| Certificate | ECDSA P-384 or Ed25519 | Auto-renewal via ACME/Let us Encrypt |
| HSTS | Enabled | max-age=63072000; includeSubDomains; preload |
| Certificate Pinning | Mobile apps | Pin intermediate + root CA |

### 3.2 Data at Rest

| Data Type | Algorithm | Key Management |
|-----------|-----------|----------------|
| Database | AES-256-GCM | KMS-managed keys, auto-rotation |
| Files/Objects | AES-256-CTR + HMAC | Envelope encryption pattern |
| Backups | AES-256-GCM | Separate key from primary |
| Secrets | AES-256-GCM | HSM-backed, never in code |
| Passwords | Argon2id | m=65536, t=3, p=4 |

### 3.3 Post-Quantum Cryptography

Prepare for the quantum computing era NOW:

- Key Encapsulation: CRYSTALS-Kyber (ML-KEM) - NIST standardized 2024
- Digital Signatures: CRYSTALS-Dilithium (ML-DSA) - NIST standardized 2024
- Hybrid Mode: Use classical + PQC algorithms together during transition
- Hash Functions: SHA-3 / BLAKE3 (quantum-resistant by design)
- Key Sizes: Double current key sizes as interim measure

### 3.4 Key Management

- NEVER hardcode keys in source code
- Use environment variables or secret managers (HashiCorp Vault, AWS KMS)
- Implement key rotation (automatic, every 90 days maximum)
- Use envelope encryption for large datasets
- Maintain key hierarchy: Master Key then Data Encryption Keys then Session Keys
- Implement key escrow for disaster recovery
- Destroy keys securely (crypto-shredding)

### 3.5 Even If the Server Is Hacked

Design so that a server compromise yields nothing useful:

1. Encrypt data with client-side keys before sending to server
2. Use end-to-end encryption for all sensitive communications
3. Store only encrypted blobs on the server
4. Keep decryption keys on client devices or in HSMs
5. Implement perfect forward secrecy (PFS) for all sessions
6. Use homomorphic encryption where computation on encrypted data is needed
7. Zero-knowledge architecture: server proves knowledge without revealing data

---

## 4. Input Validation and Sanitization

### 4.1 The Golden Rules

1. Reject, do not sanitize - If input does not match expected format, reject it
2. Validate on the server - Client-side validation is UX only, never security
3. Allowlist, do not blocklist - Define what IS allowed, not what is not
4. Validate at every boundary - API gateway, service, database layer
5. Fail closed - On validation error, deny access, do not fall through

### 4.2 Common Attack Vectors and Defenses

| Attack | Defense |
|--------|---------|
| SQL Injection | Parameterized queries, ORM, prepared statements |
| XSS (Cross-Site Scripting) | Content Security Policy, output encoding, DOMPurify |
| CSRF | SameSite cookies, CSRF tokens, Origin header validation |
| SSRF | URL allowlisting, disable redirects, network segmentation |
| Command Injection | Avoid shell execution, use safe APIs, strict input validation |
| Path Traversal | Canonicalize paths, reject dot-dot, use chroot/jail |
| XML External Entity (XXE) | Disable DTD processing, use JSON instead |
| Deserialization | Avoid native deserialization, use safe formats (JSON) |
| File Upload | Validate MIME type, scan for malware, rename files, limit size |
| LDAP Injection | Use parameterized LDAP queries, escape special characters |

### 4.3 Content Security Policy (CSP)

Implement strict CSP headers with default-src none, script-src self with nonce, style-src self, img-src self data https, font-src self, connect-src self and your API domain, frame-ancestors none, base-uri self, form-action self, and upgrade-insecure-requests.

---

## 5. Authentication and Authorization

### 5.1 Authentication Best Practices

- Implement Multi-Factor Authentication (MFA) - TOTP + WebAuthn/FIDO2
- Use Argon2id for password hashing (NEVER MD5, SHA-1, or weak bcrypt)
- Implement account lockout after 5 failed attempts (with exponential backoff)
- Support passkeys (WebAuthn) for passwordless authentication
- Use short-lived access tokens (15 min) with refresh token rotation
- Implement device fingerprinting for anomaly detection
- Send security notifications for new device/location logins

### 5.2 Authorization Models

| Model | Use Case |
|-------|----------|
| RBAC (Role-Based) | Simple hierarchical permissions |
| ABAC (Attribute-Based) | Complex, context-aware permissions |
| ReBAC (Relationship-Based) | Social/collaborative features |
| PBAC (Policy-Based) | Enterprise, compliance-heavy systems |

### 5.3 Session Management

- Use secure, HttpOnly, SameSite=Strict cookies
- Implement session timeout (30 min idle, 8 hr absolute)
- Support concurrent session management (view/revoke active sessions)
- Regenerate session ID after privilege changes
- Implement CSRF protection on all state-changing operations

---

## 6. API Security

### 6.1 OWASP API Security Top 10 (2023)

1. Broken Object Level Authorization (BOLA)
2. Broken Authentication
3. Broken Object Property Level Authorization
4. Unrestricted Resource Consumption
5. Broken Function Level Authorization
6. Unrestricted Access to Sensitive Business Flows
7. Server-Side Request Forgery (SSRF)
8. Security Misconfiguration
9. Improper Inventory Management
10. Unsafe Consumption of APIs

### 6.2 API Hardening Checklist

- Rate limiting per user, per IP, per endpoint
- Request size limits (body, headers, query params)
- Response filtering (never return more data than needed)
- API versioning with deprecation policy
- Request signing for server-to-server communication
- Correlation IDs for distributed tracing
- Circuit breakers for downstream service failures
- Idempotency keys for mutation operations

### 6.3 GraphQL Security (if applicable)

- Disable introspection in production
- Implement query depth limiting (max depth: 10)
- Implement query complexity analysis
- Use persisted queries (disable arbitrary query strings)
- Apply authorization at the resolver level
- Implement alias limiting to prevent batching attacks

---

## 7. Dependency Security

### 7.1 Supply Chain Security

- Use lock files (package-lock.json, poetry.lock, Cargo.lock)
- Enable Dependabot / Renovate for automated updates
- Run npm audit / pip audit / cargo audit in CI
- Verify package integrity (checksums, signatures)
- Use SCA tools (Snyk, Trivy, Grype) in pipeline
- Pin dependency versions in production
- Review new dependencies before adding

### 7.2 Software Bill of Materials (SBOM)

Generate and maintain SBOM for every release:

- Use SPDX or CycloneDX format
- Include all direct and transitive dependencies
- Update with every release
- Store in artifact registry alongside binaries
- Use for rapid vulnerability response

### 7.3 Build Pipeline Security

- Sign all commits (GPG/SSH)
- Use reproducible builds
- Scan container images (Trivy, Grype)
- Implement SLSA framework for supply chain integrity
- Use ephemeral build environments
- Never store secrets in build scripts
- Implement artifact signing and verification

---

## 8. Infrastructure Security

### 8.1 Server Hardening

- Disable root SSH login, use key-based auth only
- Configure firewall (ufw, iptables, nftables) - default deny
- Enable automatic security updates
- Remove unnecessary packages and services
- Configure fail2ban for brute-force protection
- Use SELinux / AppArmor for mandatory access control
- Implement file integrity monitoring (AIDE, Tripwire)
- Regular vulnerability scanning (OpenVAS, Nessus)

### 8.2 Container Security

- Use minimal base images (distroless, alpine)
- Run as non-root user
- Scan images in CI/CD pipeline
- Use read-only filesystems where possible
- Limit capabilities (drop ALL, add only needed)
- Implement resource limits (CPU, memory)
- Use network policies for pod-to-pod communication
- Sign and verify container images (cosign, Notary)

### 8.3 Cloud Security

- Enable MFA on ALL cloud accounts
- Use IAM roles instead of access keys
- Enable CloudTrail / audit logging
- Encrypt all storage (S3, EBS, RDS)
- Use VPC with private subnets for databases
- Implement security groups with least privilege
- Regular access review (remove unused permissions)
- Enable GuardDuty / Security Hub for threat detection

### 8.4 DNS Security

- Enable DNSSEC for all domains
- Use DNS-over-HTTPS (DoH) or DNS-over-TLS (DoT)
- Implement CAA records to restrict certificate issuance
- Monitor for DNS hijacking
- Use short TTLs for critical records

---

## 9. Incident Response

### 9.1 Incident Response Plan

Every project must have a documented IR plan:

1. Preparation - Tools, contacts, runbooks ready
2. Identification - Detect and classify the incident
3. Containment - Isolate affected systems
4. Eradication - Remove threat, patch vulnerability
5. Recovery - Restore from clean backups
6. Lessons Learned - Post-mortem, update defenses

### 9.2 Logging and Monitoring

- Centralized logging (ELK Stack, Grafana Loki)
- Security Information and Event Management (SIEM)
- Real-time alerting for anomalies
- Log retention: minimum 1 year (compliance dependent)
- NEVER log sensitive data (passwords, tokens, PII)
- Implement structured logging with correlation IDs
- Monitor for: failed auth, privilege escalation, data exfiltration patterns

### 9.3 Backup and Disaster Recovery

- 3-2-1 backup rule: 3 copies, 2 media types, 1 offsite
- Test restores quarterly
- Encrypt all backups
- Define RTO (Recovery Time Objective) and RPO (Recovery Point Objective)
- Document recovery procedures
- Automate backup verification

---

## 10. Legal Compliance

### 10.1 Regulatory Framework

| Regulation | Region | Key Requirements |
|-----------|--------|-----------------|
| GDPR | EU/EEA | Consent, right to erasure, DPO, 72hr breach notification |
| CCPA/CPRA | California | Opt-out, data disclosure, no discrimination |
| HIPAA | US (Health) | PHI protection, audit trails, BAAs |
| PCI DSS | Global (Payments) | Cardholder data protection, quarterly scans |
| SOC 2 | Global (SaaS) | Security, availability, confidentiality |
| LGPD | Brazil | Similar to GDPR |
| PDPA | Singapore/Thailand | Consent, purpose limitation |
| DPDP Act | India | Data fiduciary obligations, consent |

### 10.2 Compliance by Design

- Privacy Impact Assessment (PIA) before collecting any personal data
- Data minimization: collect only what is strictly necessary
- Purpose limitation: use data only for stated purpose
- Storage limitation: define and enforce retention periods
- Implement user data export and deletion
- Maintain Records of Processing Activities (ROPA)
- Appoint Data Protection Officer if required
- Include privacy policy, terms of service, cookie policy

### 10.3 Open Source Legal Safety

- Use permissive licenses (MIT, Apache 2.0) for maximum compatibility
- Maintain NOTICE file with all attribution requirements
- Run license scanning (FOSSA, Snyk License Compliance)
- Avoid GPL dependencies in proprietary code
- Document all third-party components in SBOM
- Include proper copyright headers in all source files

---

## 11. Security Checklist

### Before Any Code Is Written
- STRIDE threat model completed
- Attack surface mapped
- Security requirements documented
- Compliance requirements identified
- Encryption strategy defined
- Authentication/authorization model chosen

### During Development
- Input validation on ALL entry points
- Parameterized queries everywhere
- CSP headers configured
- Secure cookie flags set
- Rate limiting implemented
- Error messages sanitized (no stack traces in production)
- Secrets managed via vault/KMS
- Dependencies pinned and audited
- Logging implemented (no sensitive data)
- Unit tests for security-critical paths

### Before Deployment
- SAST scan passed (Semgrep, CodeQL, SonarQube)
- DAST scan passed (OWASP ZAP, Burp Suite)
- Dependency scan passed (Snyk, Trivy)
- Container image scanned
- Penetration test completed
- SSL/TLS configuration verified (testssl.sh)
- Security headers verified (securityheaders.com)
- Backup and recovery tested
- Incident response plan documented
- Legal review completed

### Ongoing
- Automated security scanning in CI/CD
- Monthly dependency updates
- Quarterly access reviews
- Annual penetration testing
- Continuous threat intelligence monitoring
- Regular security training for team

---

## References

- OWASP Top 10 (2025): https://owasp.org/www-project-top-ten/
- NIST Cybersecurity Framework 2.0: https://www.nist.gov/cyberframework
- NIST Post-Quantum Cryptography: https://csrc.nist.gov/projects/post-quantum-cryptography
- CIS Benchmarks: https://www.cisecurity.org/cis-benchmarks
- MITRE ATT and CK: https://attack.mitre.org/
- CISA KEV Catalog: https://www.cisa.gov/known-exploited-vulnerabilities-catalog

---

*Last Updated: August 2026*
*Version: 2.0.0*
*Author: Shoumik Bala Somu*
