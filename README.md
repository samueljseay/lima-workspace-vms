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

# Run a command in a sandbox
sandbox run claude ~/Code/myproject
sandbox run "npm test" ~/Code/myproject

# Custom sandbox name
sandbox ~/Code/myproject --name foo
sandbox run claude ~/Code/myproject --name foo

# Management
sandbox list              # List all sandboxes
sandbox stop myproject    # Stop (preserves state)
sandbox rm myproject      # Delete
```

## What's Included

Each sandbox VM comes with:

- Ubuntu 24.04
- Claude Code (native installer)
- Node.js (via nvm)
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
- Your IDE on the host can edit files directly (they're the same files)

## Customization

Edit `lima-template.yaml` to adjust:

- CPU/memory allocation
- Pre-installed packages
- Default shell configuration
