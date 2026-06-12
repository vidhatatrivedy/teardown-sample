# Audit Dimension 06 — Security

**Severity:** High  
**Examined:** Input handling, secrets, dependencies, data exposure, OWASP basics

## Findings

### F6.1 — DEBUG exception handler leaks internals (High)

**Evidence:** `backend/app/main.py` global handler returns `str(exc)` and exception type when `DEBUG=true`.

**Risk:** Stack traces and internal paths exposed to clients. Common misconfiguration in staging.

**Direction:** Never return exception details to clients; log server-side only. Use separate `LOG_LEVEL=debug`.

---

### F6.2 — Secrets in environment files (Medium — standard pattern)

**Evidence:** `backend/.env` holds `JWT_SECRET`, `OPENAI_API_KEY`, OAuth client secrets, SMTP credentials.

**Risk:** `.env` committed to repo would be catastrophic. Verify `.gitignore` coverage.

**Direction:** Use secret manager in production; rotate JWT secret requires session invalidation plan.

---

### F6.3 — OAuth tokens stored in MongoDB (Medium)

**Evidence:** `EmailIntegration` model stores refresh/access tokens for Gmail/Outlook.

**Risk:** DB breach exposes email access for all integrated restaurants. Tokens should be encrypted at rest.

**Direction:** Encrypt token fields; restrict DB network access; audit token refresh flow.

---

### F6.4 — Admin panel separate auth (Medium)

**Evidence:** `backend/app/routers/admin.py` uses credentials from `admin_credentials.json` file.

**Risk:** File-based admin creds without MFA. Separate from restaurant user JWT.

**Direction:** Move admin to env-based creds or SSO; enforce strong password policy; add audit log.

---

### F6.5 — CORS allowlist (Positive with caveat)

**Evidence:** `ALLOWED_ORIGINS` in config includes localhost ports and production domains.

**Risk:** Wildcard or overly broad origins in misconfigured env would enable CSRF-like attacks from malicious sites (mitigated by JWT in header, not cookies).

**Direction:** Keep explicit allowlist; review on each new frontend deploy target.

---

### F6.6 — Password hashing (Positive)

**Evidence:** bcrypt via auth utilities for signup/login/password reset.

**Risk:** Low for password-based auth.

**Direction:** Maintain; ensure Google OAuth users can't set weak passwords on merge flows.

---

### F6.7 — Dependency audit gap (Medium)

**Evidence:** `requirements.txt` without pinned hashes or automated Dependabot alerts visible in repo.

**Risk:** Known CVEs in transitive dependencies may go unnoticed.

**Direction:** Enable Dependabot; pin versions in production lockfile.

## OWASP quick check

| Category | Status |
|----------|--------|
| A01 Broken access control | See Audit 07 — partial gaps |
| A02 Cryptographic failures | bcrypt OK; tokens at rest unencrypted |
| A03 Injection | Pydantic + Beanie parameterization — low risk |
| A05 Security misconfiguration | DEBUG handler — fix |
| A07 Auth failures | JWT refresh flow present |
| A09 Logging failures | AI/email logging exists; no centralized security audit log |

**Business risk:** Investor technical diligence will ask about tenant isolation and secret handling. DEBUG leak and unencrypted OAuth tokens are fixable before diligence.
