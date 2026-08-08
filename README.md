# Personal Network Starter

An agent-maintained template for a personal device network: a MacBook is the controller, an Arch
Linux machine is the always-available worker/server, and phones can reach both through T3 Connect.

This repository is documentation and configuration source-of-truth. It intentionally contains no
passwords, API keys, agent sessions, stream keys, or private credentials.

## Target result

- The owner uses their own Tailscale tailnet and GitHub repository.
- The Arch box is reachable by Tailscale SSH and can run long agent jobs in `tmux`.
- The lab MacBook controls the Arch box and is itself available remotely when desired.
- A Syncthing drop folder moves screenshots and generated files between Mac and Arch.
- T3 Code Nightly runs on both computers; T3 Connect exposes them to the owner's phones.
- Codex and Claude are installed and authenticated separately on each computer.
- This repo records every hostname, service, access path, and recovery procedure.
- Agent instruction/config repos can be added after the basic network passes verification.

## Start here

Give an agent the following instruction:

> Read `AGENTS.md` completely, then execute `SETUP.md` in order. Work on one phase at a time,
> record discovered values in `computers.md`, run every verification check, and stop only at the
> explicitly marked human-login steps. Never copy another person's credentials, tailnet, T3
> account, SSH private keys, or agent sessions. Use accounts owned by the person setting this up.

The agent should begin on the MacBook. Keep the Arch box powered on and accessible locally during
initial setup.

## Files

- `SETUP.md` — end-to-end, agent-executable installation and verification runbook.
- `computers.md` — fill-in network map and operational record.
- `macbook/README.md` and `arch-server/README.md` — per-machine notes.
- `skills/network/SKILL.md` — reusable personal network skill template.
- `SECURITY.md` — credentials, sharing, and repository rules.

## Design boundary

This is an original, fill-in-the-blank architecture—not a copy of anyone's private repository or
identity. Every installer uses their own Tailscale, GitHub, T3 Connect, Codex, Claude, Apple/Google,
and cloud accounts. Cross-tailnet access is optional and must be granted explicitly.
