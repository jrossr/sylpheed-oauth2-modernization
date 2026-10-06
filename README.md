# Sylpheed OAuth2 Modernization

Experimental modernization of Sylpheed OAuth2/XOAUTH2 support, developed and successfully built on AlmaLinux 9.8.

The work adds PKCE/public-client support, secure OAuth state generation, refresh-token handling and rotation, IMAP/POP3/SMTP integration, safer authentication logging, and improved OAuth helper failure handling.

## Project Status

**Experimental — builds successfully — Microsoft end-to-end OAuth not yet validated.**

Microsoft IMAP/TLS connectivity worked and advertised `AUTH=XOAUTH2 LOGINDISABLED`. The modified Sylpheed source built successfully, but final testing required a Microsoft application registration/client ID. That registration could not be completed through the available Entra/Azure enrollment path, so the live OAuth authorization exchange was never reached.

> This is not a claim of a completed Microsoft OAuth implementation. It is a documented, compilable development checkpoint intended for further testing and continuation.

## What the Patch Adds

- PKCE (`S256`) support for desktop/public OAuth clients
- Optional `client_secret` handling
- Cryptographically secure PKCE verifier and OAuth state generation on Linux
- Refresh-token caching, refresh grants, and token rotation
- `invalid_grant` recovery behavior
- Preservation of cached credentials during transient failures
- IMAP, POP3, and SMTP OAuth2 integration
- Removal/redaction of secret-bearing OAuth debug output
- Correct OAuth helper-process exit-status handling
- Cleanup of a helper stdout allocation leak

## Patch

The source changes are provided in `sylpheed-oauth2-modernization.patch`.

The patch contains only the six tracked source files changed during development: 422 insertions and 46 deletions. Build products, generated Autotools files, backups, and development checkpoints are excluded.

## Continue the Work

A developer with access to a suitable Microsoft application registration/client ID can use this checkpoint to continue end-to-end Microsoft OAuth testing.

Remaining work includes live Microsoft validation, portable secure randomness for non-Linux platforms, additional token-parser hardening, and upstream-quality review/cleanup.

## Full Engineering Write-Up

The complete investigation, implementation details, build results, security work, and explanation of what stopped final testing:

https://jrossr.tech/sheets/sylpheed-oauth2-modernization.html

## Security

No passwords, OAuth tokens, authorization codes, client secrets, private email addresses, usernames, hostnames, or machine-specific home paths are intentionally included in this repository.

---

Published so the work can be continued rather than rediscovered from scratch.
