# Security policy

## Reporting a vulnerability

Don't open a public issue. Use [GitHub's private vulnerability
reporting](https://github.com/tsvrc/vpm/security/advisories/new) for this repository
instead, so the report isn't visible before a fix is available.

If that's not accessible to you for some reason, contact
[@ToniSeas](https://github.com/ToniSeas) directly.

## Scope

This covers vulnerabilities in this repo's own build tooling: `source.json`,
`Website/`, and the GitHub Actions workflows here. A vulnerability in a package
*listed* here (for example, `tsvrc-core`) belongs to that package's own repo instead,
see its `SECURITY.md`.

## Supported versions

Only the latest state of `main` is supported, there's no versioning for this repo
itself.

## Response

This project is maintained by one person in their spare time. There's no guaranteed
response time or SLA, but security reports get priority over other issues.
