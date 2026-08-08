# Setup runbook

This is written for an agent operating interactively with the owner. Complete phases in order. At
each `HUMAN` marker, pause for the owner to finish authentication or approve a sensitive choice.

## Phase 0 — inventory and safety

- [ ] On each computer, record `hostname`, username, OS/version, disk availability, and current
      Tailscale status in `computers.md`.
- [ ] Confirm the owner's GitHub username and T3 Connect email.
- [ ] Confirm the Mac and Arch box are backed up sufficiently for package/config changes.
- [ ] Inspect existing SSH, Tailscale, Syncthing, T3, Codex, and Claude installs before changing them.
- [ ] Inventory existing workloads and do not modify unrelated services as part of this setup.

Suggested read-only commands:

```bash
hostname
whoami
uname -a
tailscale status
```

## Phase 1 — repository ownership

- [ ] Create a private repo from this template and clone it into `~/Personal-Network` on the MacBook.
- [ ] Ensure the owner controls the GitHub repository.
- [ ] Configure the owner's own Git name/email on both machines.
- [ ] Clone the repo on Arch only after SSH/network access is verified.
- [ ] Verify the owner can pull and push a harmless documentation commit.

`HUMAN`: The owner authenticates GitHub CLI or SSH and accepts any collaborator/transfer invitation.

## Phase 2 — Tailscale foundation

Arch Linux:

```bash
sudo pacman -S tailscale
sudo systemctl enable --now tailscaled
sudo tailscale up --ssh
tailscale status
```

MacBook:

```bash
brew install --cask tailscale
open -a Tailscale
```

- [ ] Sign both computers into the owner's tailnet.
- [ ] Install Tailscale on both phones if device-to-device access is desired.
- [ ] Record names and IPs in `computers.md`.
- [ ] From the Mac, run `tailscale ping <arch-name>`.
- [ ] Add this Mac SSH alias using observed values:

```sshconfig
Host arch-server
    HostName <arch-tailscale-name>
    User <arch-user>
```

- [ ] Verify `ssh arch-server` in a fresh terminal.
- [ ] Reboot Arch once and verify Tailscale and SSH return automatically.

`HUMAN`: The owner completes Tailscale web login and reviews the tailnet device list. If another
person needs access, use a deliberate node share and narrowly scoped ACL; do not share an account.

## Phase 3 — Arch server baseline

Install only after checking what is already present:

```bash
sudo pacman -S --needed git base-devel openssh tmux syncthing
sudo systemctl enable --now sshd
systemctl --user enable --now syncthing
mkdir -p ~/drop
```

- [ ] Keep the GUI unless the owner explicitly wants a headless default.
- [ ] Decide with the owner whether this server should sleep. Phones cannot wake a sleeping server over
      the T3 relay; an always-available server needs suspend disabled and sensible power recovery.
- [ ] Enable BIOS “restore on AC power loss” if available.
- [ ] Verify a fresh SSH session before tightening any SSH settings.
- [ ] Record decisions in `arch-server/README.md`.

## Phase 4 — Syncthing drop folder

MacBook:

```bash
brew install syncthing
brew services start syncthing
mkdir -p ~/Desktop/screenshots
```

Arch is already started in Phase 3. Use each local Syncthing UI at `http://127.0.0.1:8384`.

- [ ] Exchange device IDs and record them in `computers.md`.
- [ ] Share Mac `~/Desktop/screenshots` with Arch `~/drop`.
- [ ] Test Mac → Arch with a harmless file.
- [ ] Test Arch → Mac with a different harmless file.
- [ ] Configure the Mac screenshot tool to save into the shared folder if desired.

## Phase 5 — package/runtime baseline

On both computers, inspect first, then install current supported Node.js and pnpm. On Arch, prefer an
explicit user-level pnpm home for global CLIs. Do not use npm, yarn, or bun for global setup.

```bash
corepack enable
corepack prepare pnpm@latest --activate
pnpm --version
node --version
```

- [ ] Record installed versions in each machine README.
- [ ] Ensure the pnpm global binary directory is on `PATH` in the user's shell.

## Phase 6 — T3 Code Nightly and T3 Connect

Use the current official T3 Code installation instructions because release commands can change.
Use this target architecture, but verify current official commands instead of copying stale versions:

- MacBook: T3 Code Nightly desktop app, backend on port 3773, app-managed T3 Connect relay.
- Arch: Nightly T3 CLI/backend as a systemd user service on port 3773, service-managed relay.
- Both: publish to the owner's T3 Connect account and give projects friendly names.
- Optional: configure Tailscale Serve HTTPS as a second path.

- [ ] Install T3 Code Nightly on Mac and open it.
- [ ] Install the exact current Nightly CLI version on Arch with pnpm.
- [ ] Install/update the Arch user service using the T3 CLI's current service command.
- [ ] Sign both into the owner's T3 Connect account and publish both environments.
- [ ] Rename home projects to `<Owner>'s MacBook` and `<Owner>'s Arch Server`.
- [ ] Verify both show **Available / Relay online** in T3 Connections.
- [ ] On each work phone, sign into T3 Code and open a harmless session on each machine.
- [ ] Reboot Arch and verify the backend and relay recover.

`HUMAN`: The owner performs the T3 Connect login and phone sign-in. Never copy another person's
Connect credential. If the account has a device limit, review it before adding both computers.

## Phase 7 — Codex and Claude

Install the current official CLIs through their documented method. Authenticate on each machine as
the owner. Authentication state is local and must never enter this repo.

- [ ] Install and authenticate Codex on Mac.
- [ ] Install and authenticate Codex on Arch.
- [ ] Install and authenticate Claude on Mac.
- [ ] Install and authenticate Claude on Arch.
- [ ] From T3 mobile, start one harmless agent session on each computer.
- [ ] Confirm agents can read `~/Personal-Network/computers.md`.

`HUMAN`: The owner completes provider logins and chooses subscriptions/accounts.

## Phase 8 — install the personal network skill

Install `skills/network/` into each agent's personal skill directory using that tool's current skill
installation convention. If both Claude and Codex share skills through a tracked config repo, use a
single documented source of truth and symlink/copy only as supported.

- [ ] Test: ask, “What machines are in my network and how do I reach the Arch server?”
- [ ] Confirm the answer comes from this repo and identifies unknown fields instead of guessing.
- [ ] Confirm an agent updates docs after a real topology change.

## Phase 9 — optional config synchronization

Do this only after the basic network works. Recommended mature design: separate private allowlisted
repos checked out directly over each live config directory (`~/.codex`, `~/.claude`, and optionally
`~/.agents`/`~/.cursor`). Explicitly exclude tokens, keys, `.env`, databases, caches, and sessions.

- [ ] Decide which instructions/skills the owner actually wants shared.
- [ ] Create owner-controlled private config repos; do not copy another person's private config.
- [ ] Add allowlist `.gitignore` files before the first commit.
- [ ] Add a pull timer on Arch only after manual pull/push and divergence behavior are tested.
- [ ] Prefer `git pull --ff-only`; alert on divergence instead of auto-merging agent instructions.

## Final acceptance test

- [ ] Mac reaches Arch by Tailscale name and SSH after an Arch reboot.
- [ ] A screenshot syncs Mac → Arch and a generated file syncs Arch → Mac.
- [ ] Both machines appear in T3 Connect from both phones.
- [ ] A Codex or Claude session runs remotely on Arch through a phone.
- [ ] The network skill answers accurately from this repository.
- [ ] `git grep` and staged diff inspection find no credentials.
- [ ] All placeholders in `computers.md` are filled or explicitly marked “not configured.”
- [ ] The owner can recover each service using the per-machine README without outside help.
