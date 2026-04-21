---
name: security-audit
category: security
description: >
  Audit code for security vulnerabilities. Use when the user says "security-audit",
  "security check", "is this secure", "audit for vulnerabilities", or before any
  public deployment. Covers OWASP Top 10 and common API/backend attack surfaces.
---

# Security Audit

You are doing a security audit. Find real vulnerabilities — not theoretical risks, not style issues.

---

## Scope

If the user specifies a file or feature, audit only that. Otherwise audit files changed since the last commit:

```
git diff HEAD --name-only
```

Read only files in scope. Do not speculatively read the whole repo.

---

## Checklist (run in this order)

### 1. Injection
- SQL: any string-concatenated queries? Must use parameterized queries or ORM.
- Command injection: any `exec`, `spawn`, `eval` with user input?
- Path traversal: any file reads/writes using user-supplied paths without sanitization?

### 2. Authentication & Authorization
- Any endpoint reachable without authentication?
- Any ownership check missing (user A can access user B's data)?
- Any token or session stored insecurely (localStorage for sensitive tokens, logged to console)?

### 3. Secrets & Credentials
- Any API keys, passwords, or tokens hardcoded in source?
- Any `.env` values accidentally logged or returned in API responses?
- Any secrets in error messages sent to the client?

### 4. Input Validation
- Any user input used without validation at system boundaries (API routes, DB writes, file ops)?
- Any missing length/type/format checks that could cause unexpected behaviour?

### 5. Error Handling & Information Leakage
- Any stack traces, DB schema details, or internal paths reaching the client?
- Any catch blocks that swallow errors silently without logging server-side?

### 6. Transport & CORS
- Any `http://` calls to external services in production code?
- Any `Access-Control-Allow-Origin: *` on non-public endpoints?

### 7. Rate Limiting
- Any public-facing endpoints (authenticated or not) without rate limiting?

---

## Output format

For each finding:

```
[SEVERITY] file:line — one-line description
ATTACK: how an attacker exploits this
FIX: exact change needed
```

Severity levels: `CRITICAL` | `HIGH` | `MEDIUM`

Stop at 7 findings. If there are more, note "further issues likely — address these first."

If nothing is found: "No security vulnerabilities found in scope."

---

## What NOT to do

- Do not flag issues that only appear in test/dev environments
- Do not suggest performance improvements or refactors
- Do not quote large code blocks — use file:line references
- Do not add "looks secure overall" filler
