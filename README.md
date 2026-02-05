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
# Create a new sandbox with your codebase
sandbox new myproject ~/Code/myproject

# Attach to it (starts if stopped)
sandbox attach myproject

# Inside the sandbox, run Claude in YOLO mode
claude  # aliased to --dangerously-skip-permissions

# List all sandboxes
sandbox list

# Stop a sandbox (preserves state)
sandbox stop myproject

# Delete a sandbox
sandbox delete myproject
```

## What's Included

Each sandbox VM comes with:

- Ubuntu 24.04
- Node.js (via nvm)
- Claude Code (pre-installed)
- Claude Code Safety Net (pre-installed)
- PHP + Composer
- Git, ripgrep, fd, tmux, vim
- Your codebase mounted at `/workspace`

## Requirements

- Lima (`brew install lima`)
- jq (`brew install jq`)

## Tips

- Use `tmux` inside the sandbox for persistent sessions
- The `claude` alias automatically enables YOLO mode
- Sandboxes persist across restarts - use `sandbox stop` to free resources
- Multiple sandboxes can run simultaneously

## Customization

Edit `lima-template.yaml` to adjust:

- CPU/memory allocation
- Pre-installed packages
- Default shell configuration
