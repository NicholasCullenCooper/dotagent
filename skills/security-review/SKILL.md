---
name: security-review
description: Security-focused code review targeting OWASP top risks. Use when reviewing code that handles user input, authentication, authorization, or external data.
---

# Security Review

## When to use

- Reviewing PRs that touch auth, input handling, or data boundaries
- Auditing a codebase for security posture
- Before shipping code that handles PII or credentials
- After a dependency upgrade that touches security-sensitive paths

## Threat checklist

Work through these categories in order. Stop and report when you find a real issue.

### 1. Injection

- SQL: Are queries parameterized? No string concatenation with user input.
- Command: Is `exec`/`spawn` called with user-controlled strings? Use arrays, not shell strings.
- Template: Is user input rendered without escaping in HTML/email templates?
- Path traversal: Is user input used in file paths without sanitization? Check for `../`.

### 2. Authentication

- Are passwords hashed with bcrypt/scrypt/argon2, not MD5/SHA?
- Are session tokens sufficiently random and rotated on privilege change?
- Is there rate limiting on login endpoints?
- Are failed auth attempts logged (without logging the password)?

### 3. Authorization

- Is there a check on every protected endpoint, not just the frontend route?
- Are object-level permissions checked (IDOR)? Can user A access user B's resource by changing an ID?
- Are admin endpoints behind proper role checks, not just hidden URLs?

### 4. Data exposure

- Are API responses filtered to only include fields the caller should see?
- Are credentials, tokens, or PII logged anywhere?
- Are error messages generic to users but detailed in server logs?
- Is sensitive data encrypted at rest and in transit?

### 5. Dependencies

- Are there known CVEs in current dependencies? Check `npm audit` / `go vuln` / `pip audit`.
- Are dependency versions pinned? (lockfiles committed)
- Are dependencies from trusted sources?

## Output format

- Severity: critical / high / medium / low
- Location: file and line
- Issue: what's wrong
- Impact: what an attacker could do
- Fix: specific remediation
