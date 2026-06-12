# Security Model

## Threat surface

```mermaid
flowchart TB
    subgraph external [External threats]
        XSS[Cross-site scripting]
        StolenJWT[Stolen JWT]
        BruteForce[Auth brute force]
        LLM abuse[AI endpoint abuse]
    end
    subgraph internal [Internal threats]
        TenantLeak[Cross-tenant access]
        SecretLeak[Secret exposure]
        TokenLeak[OAuth token theft from DB]
    end
    subgraph assets [Assets to protect]
        PII[Customer PII in enquiries]
        EmailAccess[Connected email accounts]
        BusinessData[Bookings and pricing]
    end
    XSS --> StolenJWT
    StolenJWT --> TenantLeak
    BruteForce --> StolenJWT
    SecretLeak --> EmailAccess
    TokenLeak --> EmailAccess
    TenantLeak --> BusinessData
    TenantLeak --> PII
```

## Security controls

| Control | Implementation | Status |
|---------|----------------|--------|
| Password hashing | bcrypt | Implemented |
| JWT signing | HS256 with `JWT_SECRET` | Implemented |
| HTTPS | Nginx + Let's Encrypt in deploy.sh | Production |
| CORS allowlist | `ALLOWED_ORIGINS` | Implemented |
| Input validation | Pydantic models | Implemented |
| RBAC | permissions.py | Implemented — gaps on standalone routes |
| Subscription gate | Frontend AuthWrapper | Partial — backend enforcement needed |
| Rate limiting | — | **Not implemented** |
| Token encryption at rest | — | **Not implemented** |
| Security headers | — | Verify Nginx config |

## Secrets handling

| Secret | Storage | Rule |
|--------|---------|------|
| JWT_SECRET | backend `.env` | Rotate with forced re-login |
| OPENAI_API_KEY | backend `.env` | Never in frontend |
| OAuth client secrets | backend `.env` | Never commit |
| Admin password | admin_credentials.json | Move to env; use strong password |
| User passwords | MongoDB hashed | Never log |

**Agent rule:** Never commit or print `.env` values. Use `[REDACTED]` in docs.

## Authentication flows

### JWT lifecycle
- Access token: short-lived (configurable)
- Refresh token: longer-lived, rotation on refresh
- Stored in browser localStorage — **XSS is the primary token theft vector**

**Mitigations:**
- Sanitize user-generated HTML in email views
- CSP headers on frontend deploy
- Avoid `dangerouslySetInnerHTML` without DOMPurify

### Google OAuth
- Used for user login and Gmail email integration (separate scopes)
- Callback URLs must match Google Cloud Console exactly

## Data classification

| Class | Examples | Handling |
|-------|----------|----------|
| Public | Marketing copy, taxonomy lists | Cacheable |
| Internal | Restaurant settings | Tenant-scoped API |
| Confidential | Client pricing, bank details | RBAC + audit log (future) |
| Restricted | OAuth tokens, passwords | Encrypt/hash; minimal access |

## AI data handling

- Enquiry text sent to OpenAI/DeepSeek contains customer PII
- Privacy policy must disclose AI processing ([`/privacy`](/privacy) page)
- Log retention: avoid logging full email bodies in production

## Incident response (minimal)

1. Rotate JWT_SECRET → all users re-login
2. Revoke compromised OAuth integration via admin UI
3. Disable affected restaurant subscription pending review

## Pre-diligence checklist

- [ ] DEBUG=false in all production envs
- [ ] Global exception handler never returns stack traces
- [ ] Cross-tenant integration tests pass
- [ ] Dependabot enabled on GitHub repo
- [ ] OAuth tokens encrypted at rest

See [rbac_access_control.md](rbac_access_control.md) for authorization detail.
