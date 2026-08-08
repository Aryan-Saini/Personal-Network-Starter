# Security and ownership

Keep an instantiated repository private unless the owner deliberately removes all personal topology
details. The unfilled template itself is safe to share.

## Never commit

- passwords, recovery codes, cookies, tokens, API keys, OAuth files, or agent sessions;
- SSH private keys (`id_ed25519`); only public keys ending in `.pub` may be tracked;
- T3 Connect credentials, Codex/Claude auth state, cloud credentials, or stream keys;
- `.env` files, credential JSON, certificates, or databases.

The `.gitignore` blocks common secret formats, but it is only a backstop. Inspect every staged diff.

## Account model

The installer owns the Tailscale tailnet, GitHub repo access, T3 Connect account, and agent
subscriptions. Anyone else's access should be granted explicitly as a collaborator or through a
narrow Tailscale node share/ACL. Do not share account passwords.

## SSH

Prefer Tailscale SSH for remote access. If conventional SSH keys are also used, generate a unique key
on each client and install only its public key on the server. Disable password SSH only after a second
verified session succeeds, so setup cannot lock out the owner.
