---
description: Run a QAEverest security scan against a URL
argument-hint: [https://target.example.com]
---

Run a security scan against: **$ARGUMENTS**

1. If `$ARGUMENTS` is not a URL, ask for one.
2. Confirm the user is authorized to scan that host before calling anything. If it isn't obviously their own staging or production environment, ask. Scanning someone else's host is the mistake this step exists to prevent.
3. Call `qae_security_scan` with the URL. Use `scan_type: "full"` unless the user asked for just headers, SSL, or vulnerabilities.
4. Present the findings grouped by risk, highest first. For each one, say what it means in practice — a missing `Strict-Transport-Security` header is a downgrade risk, not just a missing string.

Consumes credits.
