# Lab Notes — moodle-cli

Running log of agent-session setup and activity for this repo, on the
`agent` branch, per the `start-agent` skill.

## 2026-10-01

- `harmeling/moodle-cli` is a **fork** of `bunizao/moodle-cli` (the clone
  registered an `upstream` remote pointing there, with tag history through
  v0.9.6) — not an original harmeling project like the other repos in this
  workflow. All agent work here happens on harmeling's own fork; nothing
  pushes to `upstream`.
- No `agent` branch existed (locally or on `origin`) — created it from
  `main`.
- `CLAUDE.md` already present at repo root (from upstream) — skipped
  `/init`.

## 2026-10-01 10:32 — moodle-cli-1 launch (idle, Remote Control), tmux-on-ls8-slurm scheme

- Launched idle — no task given, standing by for Remote Control.
- Session name: `moodle-cli-1`
- Claude Code session ID (transcript UUID, for `--resume`):
  `635f96c9-2890-45bb-85af-6709768930c7`
- Hit the first-run "trust this folder" prompt (new clone location on this
  host); confirmed with explicit user permission.
- Launch command used (run locally, already on `ls8-slurm`):
  `tmux new-session -d -s moodle-cli-1 -c ~/git/moodle-cli 'claude --remote-control moodle-cli-1'`
- Monitor: `tmux capture-pane -t moodle-cli-1 -p | tail -n 50`
- Attach: `tmux attach -t moodle-cli-1`
- Resume (after a kill or restart): use the `resume-agent` skill.
- Cancel: `tmux kill-session -t moodle-cli-1`

## 2026-10-01 — Node setup

- Installed nvm v0.40.3 (~/.nvm) and Node 22.23.3 on the login node (light, no SLURM).
- SLURM job 113971: `srun -p interactive -c 1 --mem=2G -t 10 npm ci --omit=dev --ignore-scripts` — install runtime deps only. Completed, 0 vulnerabilities.
- Running `src/cli.ts` directly fails: ERR_MODULE_NOT_FOUND for `./intent-contract.js` (imports use `.js` for `.ts` files); needs a build (`tsup`, dev dep).
