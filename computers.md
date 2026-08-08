# My computers

Fill this file with observed values during setup. Do not paste credentials.

## Accounts

| service | owner-controlled account | verified |
|---|---|---|
| GitHub | `<username>` | no |
| Tailscale | `<email>` | no |
| T3 Connect | `<email>` | no |
| Codex/OpenAI | `<email>` | no |
| Claude | `<email>` | no |

## Machines

| role | friendly name | hostname | OS | Tailscale name/IP | local user | notes |
|---|---|---|---|---|---|---|
| controller | Lab MacBook | `<fill>` | macOS `<fill>` | `<fill>` | `<fill>` | source of truth |
| server | Arch server | `<fill>` | Arch Linux | `<fill>` | `<fill>` | worker/server |
| mobile | Work phone 1 | `<n/a>` | `<fill>` | `<fill>` | `<n/a>` | T3 mobile client |
| mobile | Work phone 2 | `<n/a>` | `<fill>` | `<fill>` | `<n/a>` | T3 mobile client |

## Access paths

- Mac → Arch over Tailscale SSH: `ssh arch-server` after configuring the alias.
- Phones → Mac/Arch: T3 Code mobile/web through T3 Connect relay.
- Mac ↔ Arch files: Syncthing, `~/Desktop/screenshots` ↔ `~/drop`.
- Optional fallback: Tailscale Serve HTTPS for T3 Code when the client is on the tailnet.

## Service inventory

| machine | service | launch mechanism | port | verification | status |
|---|---|---|---|---|---|
| MacBook | Tailscale | macOS app | — | `tailscale status` | pending |
| MacBook | Syncthing | Homebrew service | 8384 local UI | `brew services list` | pending |
| MacBook | T3 Code Nightly | desktop app | 3773 | Connections UI | pending |
| Arch | tailscaled | system unit | — | `systemctl is-active tailscaled` | pending |
| Arch | sshd/Tailscale SSH | system unit | 22/overlay | new SSH session | pending |
| Arch | Syncthing | user unit | 8384 local UI | `systemctl --user is-active syncthing` | pending |
| Arch | T3 Code Nightly | user unit | 3773 | `t3 status` / Connections UI | pending |

## Syncthing device IDs

- MacBook: `<fill>`
- Arch server: `<fill>`

## Recovery notes

- If Tailscale is connected but SSH times out, verify the route and that SSH is enabled on the Arch
  device. Keep local access available until remote access has been tested after a reboot.
- If T3 is unavailable, test the backend locally first, then the T3 Connect relay, then Tailscale
  Serve. These are independent paths.
- If a machine identity changes after reinstall, update this document rather than preserving stale
  host keys or IP assumptions.
