# Personal Network Agent Instructions

This repository becomes the source of truth for its owner's computers and how they connect.

## Operating rules

1. Ask the owner's preferred name once and record it in `computers.md`.
2. Before answering questions about the owner's network, read `computers.md` and the relevant machine
   README. Do not guess values that can be checked.
3. During initial setup, follow `SETUP.md` sequentially and update checkboxes only after verification.
4. Use owner-controlled accounts and credentials. Never copy another person's tokens, SSH private keys,
   Tailscale identity, T3 credential, Codex/Claude session, or stream key.
5. Never commit secrets. Read `SECURITY.md` before adding configuration files.
6. Ask before actions that can interrupt access or work: reboot, suspend, firewall changes,
   replacing SSH policy, deleting data, stopping services not created by this repo, or changing a
   public stream.
7. Prefer Tailscale names over fixed `100.x` addresses in commands. Record both for diagnosis.
8. Use `pnpm`, not npm/yarn/bun, for JavaScript package installation.
9. Do not run application dev servers or builds unless the task requires them.
10. After a confirmed network change, update the relevant documentation and commit it. Do not
    auto-commit unrelated repositories.

## Definition of done

A setup phase is complete only when its verification commands succeed and its discovered values are
written to `computers.md`. Human login/approval steps must be handed back clearly; never work around
them by borrowing another person's account.
