# Dotfiles

## Quick Start

Prerequisite: `curl`.

```bash
cd ~
git clone https://github.com/nicopujia/dotfiles.git .dotfiles
cd .dotfiles
./install.sh
```

The installer bootstraps Homebrew if it is missing, which then installs GNU Stow, Bun, uv, formulae, and casks.

## Secrets

Create `~/.env` for private values (not tracked):

```bash
export API_KEY="your-key-here"
export WHATEVER_SECRET_YOU_HAVE="goes-here"
```

The shell config automatically sources `~/.env` if it exists.

## Syncthing

Used for two-way file sync between machines (e.g. VPS ↔ laptop) without a cloud
intermediary. Installed via the Brewfile.

Each machine generates its own device ID on first run — this is stateful,
per-machine data, so it's intentionally **not** tracked in this repo (unlike
the rest of the symlinked config). Set it up per machine instead:

```bash
brew services start syncthing
# Open http://127.0.0.1:8384, grab this machine's device ID from
# Actions -> Show ID, then add each other machine as a remote device
# and share a folder between them.
```

## Workflow

**Files are symlinked**, so you edit in the repo, and changes apply immediately.

**Sync to another machine:**

```bash
cd ~/.dotfiles && git pull && ./install
```

**If you edited the live file directly** (e.g., `~/.zshrc`), copy changes back:

```bash
cp ~/.zshrc ~/.dotfiles/misc/shell-config.sh
cd ~/.dotfiles && git commit -am "Update shell config"
```
