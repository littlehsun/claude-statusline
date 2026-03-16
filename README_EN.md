# Claude Code Rate Limit Statusline ⚡

A lightweight, zero-cost, and 100% accurate rate limit statusline for **Claude Code** (Pro / Max tiers).
Accurately displays 5-hour and 7-day quotas for Claude Code Pro / Max plans.

## 💡 Why This Project?

Claude Code's official `/statusline` API does not expose concrete Rate Limit data. Polling the official Usage API frequently via scripts will easily trigger `429 Too Many Requests` blocks.

**The solution:**
By running a minimal local Node.js reverse proxy, we intercept and parse the `anthropic-ratelimit-unified-*` headers returned by the Anthropic API during normal conversations, then convert them into a format that the native Statusline can read.

## ✨ Features

* **🚫 No 429 blocks** — sends zero extra requests; relies entirely on intercepting existing traffic.
* **🎯 100% official data** — reads server-side Unified Rate Limit directly, no local estimation.
* **🌈 Visual statusline** — dynamic color coding shows remaining 5h and 7d quota percentages and reset times (yellow above 50%, red above 80% consumed).
* **👻 Silent background process** — all output redirected to `/dev/null`, no log files on disk.
* **🐧 Dual-platform** — automatically compatible with macOS and Ubuntu/Linux.

## 🚀 Quick Start

Run the following command in your terminal to download and execute the one-click setup script. The script will automatically check for required tools (e.g., `jq`), start the proxy server in the background, and help configure your shell.

```bash
chmod +x setup_claude_status.sh
./setup_claude_status.sh
```

## 🛠️ Usage

After installation, you just need to let Claude Code know to use the local proxy.

### 1. Configure Auto-start

At the end of the installation script, it will detect your shell profile (`~/.zshrc` or `~/.bashrc`) and ask if you want to add the auto-start configuration:

```
💡 Would you like to add the Proxy auto-start to ~/.zshrc? (y/N)
```

- **Select `y`**: Automatically writes to your profile. You'll need to run `source ~/.zshrc` (or restart your terminal) for it to take effect.
- **Select `N` (Default)**: Displays the manual command for you to copy and paste.
- **If shell is not detected**: It will list both zsh and bash versions for manual configuration.

Once configured, every time you open a new terminal, it will automatically ensure the Proxy is running and set `ANTHROPIC_BASE_URL=http://localhost:19999`.

### 2. Launch Claude Code

```bash
claude
```

### 3. Bind the Statusline

Inside the Claude interface, run the following command to bind the generated script:

```bash
/statusline ~/.claude/statusline-command.sh
```

🎉 Send any message to Claude and your statusline will light up immediately!

## 🛑 Stop the Proxy

To temporarily stop the background proxy server:

```bash
kill $(cat /tmp/claude_proxy.pid) && rm -f /tmp/claude_proxy.pid
```

Or search by name:

```bash
pkill -f "node claude-proxy.js"
```

## 📁 File Reference

| File | Description |
|------|-------------|
| `claude-proxy.js` | Node.js reverse proxy — forwards requests to `api.anthropic.com`, captures Rate Limit headers, and writes them to `/tmp/claude_rate_limit.json` |
| `setup_claude_status.sh` | One-click setup script — installs dependencies, starts the proxy, and copies the statusline script |
| `statusline-command.sh` | Statusline script — displays model name, Git branch, context usage, and 5h / 7d Rate Limit |

## ⚙️ Technical Details

* **Proxy Port**: `19999`
* **Data Path**: `/tmp/claude_rate_limit.json`
* **PID Path**: `/tmp/claude_proxy.pid` (used for management)
* **Reset Fields**: `reset_5h` and `reset_7d` are Unix timestamps (not ISO 8601).
* **Display Format**: `5h:<used>%(↺HH:MM) 7d:<used>%(↺MM/DD HH:MM)`
* **Port Conflict**: The setup script automatically detects if port `19999` is already in use and provides the PID and process name for troubleshooting.
