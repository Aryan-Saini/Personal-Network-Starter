---
name: network
description: Read the owner's personal machine-network documentation to answer questions about their computers, tailnet, remote access, T3 Code, Syncthing, and services. Use whenever the owner asks about their network, machines, server, tailnet, remote coding, or what runs where.
---

# Personal network

The network source of truth is this repository. During installation, record its absolute path in the
agent's global instructions; examples below assume `~/Personal-Network`.

## Required workflow

1. Read `~/Personal-Network/computers.md` first.
2. Read the relevant machine README under `macbook/` or `arch-server/`.
3. Answer from observed documentation. Clearly label missing or stale values; do not guess.
4. Before operating a machine, resolve the exact hostname/user from the docs and run read-only status
   checks first.
5. Ask before access-interrupting or destructive changes, including reboot, suspend, SSH/firewall
   policy replacement, deleting data, stopping unrelated services, or changing a public stream.
6. After a verified topology/service change, update the relevant docs and commit only this repo.

## Security

Never add passwords, tokens, cookies, private SSH keys, agent sessions, T3 credentials, cloud
credentials, or stream keys to the repo. The installer owns all accounts. Other people receive explicit,
narrow access rather than shared passwords or copied credentials.
