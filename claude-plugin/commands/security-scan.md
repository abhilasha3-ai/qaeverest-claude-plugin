---
description: Run a QAEverest security scan against a URL (headers, SSL/TLS, common vulnerabilities)
argument-hint: [full URL to scan, e.g. https://staging.example.com]
---

Run a QAEverest security scan for: **$ARGUMENTS**

Steps:
1. Treat `$ARGUMENTS` as the target URL. If it has no scheme, ask the user to confirm the full URL (including `https://`). If empty, ask what to scan.
2. Call the `security_scan` tool with `scanType: "full"` unless the user asked for only `headers`, `ssl`, or `vulnerability`.
3. Summarize findings grouped by risk (critical → info) and call out the single most important issue to fix first.

This scans an external, user-supplied target and consumes QAEverest credits. Only scan hosts the user is authorized to test.
