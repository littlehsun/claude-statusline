# Claude Code Enhanced Statusline ⚡

A statusline for **Claude Code** that displays model, folder, git status, context usage, and rate limits for Pro / Max tiers.

For the Ubuntu / GNOME top-bar indicator, use the unified **[rate-limit-indicator](https://github.com/littlehsun/rate-limit-indicator)** project for Codex, Claude, Grok, and Gemini.

## ✨ Features

* **🌈 Two-line visual statusline** — line 1 shows model, git branch & status, context usage; line 2 shows 5h / 7d rate limit progress bars with reset times
* **🌿 Git status at a glance** — staged (`+`), modified (`!`), untracked (`?`), ahead (`↑`), behind (`↓`)
* **⏱ Countdown + absolute time** — 5H reset shows both countdown (e.g. `2h15m`) and absolute time (e.g. `19:00`)
* **⑂ Worktree support** — automatically shows worktree name when active
* **🎨 RGB truecolor** — dynamic color coding based on usage: green → orange → yellow → red
* **🐧 Cross-platform** — compatible with macOS and Ubuntu/Linux

## 🖼️ Preview

Claude Code statusline:

```
Sonnet │ my-project  main !1 ↑2 │ ✍ 45%
5H ●●●●○○○○○○ 38% ↻ 2h15m (19:00)    7D ●●●●●●●○○○ 72% ↻ 03/30 08:00
```

Ubuntu GNOME top bar (optional):

```
Claude logo  8%|1% ⟳2h30m
```

## 🚀 Quick Start

**Requirement:** `jq` (auto-installed by the setup script)

```bash
chmod +x setup.sh
./setup.sh
```

During setup, you'll be asked:

1. **Progress bar style**

| Option | Style | Preview |
|--------|-------|---------|
| 1 (default) | Square | `▰▰▰▱▱▱▱▱▱▱` |
| 2 | Circle | `●●●○○○○○○○` |
| 3 | Half-block | `███▌░░░░░░` |

Then inside Claude Code, run:

```bash
/statusline ~/.claude/statusline-command.sh
```

Send any message and the statusline will appear.

> If you use a custom `CLAUDE_CONFIG_DIR`, replace the path with the `statusline-command.sh` in that directory.

## 🖥️ Ubuntu GNOME Rate Limit Indicator

Displays live usage in the GNOME system tray — visible even when Claude Code is closed.

Install the Claude provider from `rate-limit-indicator`:

```bash
git clone https://github.com/littlehsun/rate-limit-indicator.git
cd rate-limit-indicator
./install.sh claude
```

**Data flow:**

```
Claude Code statusline → ~/.claude/rate_limits_live.json → GNOME indicator (refreshes every 60s)
```

## 📁 Files

| File | Description |
|------|-------------|
| `statusline-command.sh` | Main script — displays model, git status, context, rate limits; also writes `rate_limits_live.json` |
| `setup.sh` | Setup script — checks for `jq` and copies the script to the Claude config directory |

## 🙏 Credits

Visual design inspired by [kamranahmedse/claude-statusline](https://github.com/kamranahmedse/claude-statusline), including the RGB color palette, `●○` progress bar style, and two-line layout concept.
