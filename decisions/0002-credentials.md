# 0002 — Where logins and secrets are kept

**Date:** 2026-11-03
**Decided by:** pending (Krischan)
**Status:** proposed (standing default from the team's template)

## Context

The product will have logins: Cloudflare, a domain registrar, extension stores, a tip platform, maybe Supabase. Plain-text passwords in Git are a risk: they stay in history forever, sit in every clone, and are read by every AI session that opens the repo.

## Options

1. **Shared password manager vault** (for example Bitwarden or 1Password, one vault for this product). The repo records which logins exist and where they're kept. Recommended: simplest, revocable per person, nothing secret in Git.
2. **Encrypted file in the repo** (SOPS with age, or git-crypt).
3. **Plain text in the repo.** Not recommended.

Deploy tokens for the code (Cloudflare API tokens) belong in the code repository's CI secrets, never here.

## Decision

Pending. Until decided, no plain-text secrets in the repo (see [AGENTS.md](../AGENTS.md#credentials)).
