# Arch server

Always-available worker for remote agents and long jobs.

## Fill during setup

- Hostname: `<fill>`
- Arch/kernel version: `<fill>`
- Local user: `<fill>`
- Tailscale name/IP: `<fill>`
- T3 Code Nightly version: `<fill>`
- Node/pnpm versions: `<fill>`
- Syncthing device ID: `<fill>`
- Sleep policy: `<fill>`
- Power-loss recovery: `<fill>`

## Expected services

- `tailscaled.service`
- `sshd.service` and/or Tailscale SSH
- `syncthing.service` as a user unit, sharing `~/drop`
- T3 Code as a user service with T3 Connect relay

## Existing workload boundary

Network onboarding must not alter pre-existing workloads, ports, repositories, credentials, or boot
behavior without a separate explicit request.

## Recovery

After setup, record exact commands for checking/restarting each expected service and the results of a
reboot acceptance test.
