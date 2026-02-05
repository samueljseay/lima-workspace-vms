# Claude Sandbox

Isolated Lima VMs for running Claude Code safely in YOLO mode.

## Installation

```bash
# Clone the repo
git clone git@github.com:samueljseay/lima-workspace-vms.git
cd lima-workspace-vms

# Add to your PATH (add to ~/.zshrc or ~/.bashrc)
export PATH="$PWD:$PATH"

# Or create a symlink
ln -s "$PWD/sandbox" /usr/local/bin/sandbox
```

## Usage

```bash
# Enter a sandbox (creates on first run)
sandbox ~/Code/myproject

# Attach to existing sandbox by name
sandbox myproject

# Run a command in an existing sandbox
sandbox myproject run claude
sandbox myproject run "npm test"

# Run a command (creates sandbox if needed)
sandbox run claude ~/Code/myproject
sandbox run "npm test" ~/Code/myproject

# Custom sandbox name
sandbox ~/Code/myproject --name foo
sandbox run claude ~/Code/myproject --name foo

# Specify Claude model (default: opus)
sandbox ~/Code/myproject --model sonnet
sandbox run claude ~/Code/myproject --model haiku

# Management
sandbox list              # List all sandboxes
sandbox stop myproject    # Stop (preserves state)
sandbox rm myproject      # Delete
```

## What's Included

Each sandbox VM comes with:

- Ubuntu 24.04
- Claude Code (native installer, YOLO mode by default)
- Docker + Docker Compose (for wp-env, etc.)
- Node.js (via nvm)
- PHP + Composer
- Git, ripgrep, fd, tmux, vim
- Your codebase mounted at `/workspace`
- 100GB disk (50GB with `--no-docker`)

## Authentication & Settings

Claude authentication is automatically synced from your macOS Keychain. If you're logged into Claude Code on your host machine, the sandbox will use the same credentials.

The model preference (default: `opus`) is set in `~/.claude/settings.json` on your host and shared with the VM via mount. Use `--model` to override.

## Requirements

- Lima (`brew install lima`)
- jq (`brew install jq`)

## Tips

- Use `tmux` inside the sandbox for persistent sessions
- The `claude` alias automatically enables YOLO mode (`--dangerously-skip-permissions`)
- Sandboxes persist across restarts - use `sandbox stop` to free resources
- Multiple sandboxes can run simultaneously
- Your IDE on the host can edit files directly (they're the same files via mount)
- Docker containers (e.g., wp-env) run inside the VM for full isolation
- Lima auto-forwards ports, so `localhost:8888` in the VM is accessible on your Mac

## Customization

Edit `lima-template.yaml` to adjust:

- CPU/memory allocation (default: 4 CPUs, 8GB RAM, 50GB disk)
- Pre-installed packages
- Default shell configuration
