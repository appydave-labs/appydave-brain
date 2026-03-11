# Homebrew Essentials

Mac's package manager. Install it first — almost everything else depends on it.

---

## Install Homebrew

```bash
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

After installing on Apple Silicon, add to your shell:
```bash
echo 'eval "$(/opt/homebrew/bin/brew shellenv)"' >> ~/.zshrc
source ~/.zshrc
```

Verify:
```bash
brew --version
brew doctor   # diagnose any issues
```

---

## Core CLI tools (install these first)

```bash
brew install \
  git \
  jq \
  gh \
  curl \
  wget \
  tree \
  ripgrep \
  fzf
```

| Tool | What it does |
|------|-------------|
| `git` | Version control (system git is outdated) |
| `jq` | JSON processing in the terminal |
| `gh` | GitHub CLI — PRs, repos, issues from terminal |
| `curl` | HTTP requests |
| `wget` | File downloads |
| `tree` | Directory tree visualisation |
| `ripgrep` (rg) | Fast text search across files |
| `fzf` | Fuzzy finder — powers interactive history search |

---

## Developer tools

```bash
brew install \
  nvm \
  rbenv \
  pyenv \
  postgresql@16
```

Note: `nvm` via brew requires extra setup — see `dev-tools.md` for nvm configuration.

---

## GUI applications (casks)

```bash
brew install --cask \
  iterm2 \
  visual-studio-code \
  github \
  rectangle
```

| App | What it does |
|-----|-------------|
| iTerm2 | Terminal replacement (split panes, profiles) |
| Visual Studio Code | Code editor |
| GitHub Desktop | Visual git client |
| Rectangle | Window management keyboard shortcuts |

---

## Brewfile — save and restore your setup

A `Brewfile` captures everything installed so you can recreate it on a new machine.

```bash
# Save current state
brew bundle dump --file=~/.dotfiles/Brewfile

# Restore on a new machine
brew bundle install --file=~/.dotfiles/Brewfile
```

Starter Brewfile:
```ruby
# Brewfile
brew "git"
brew "jq"
brew "gh"
brew "tree"
brew "ripgrep"
brew "fzf"
brew "nvm"
brew "rbenv"

cask "iterm2"
cask "visual-studio-code"
cask "rectangle"
```

Commit your Brewfile to a dotfiles repo — it's your Mac setup manifest.

---

## Useful brew commands

```bash
brew update           # update brew's package index
brew upgrade          # upgrade all outdated packages
brew outdated         # see what's out of date
brew cleanup          # remove old versions
brew list             # all installed packages
brew info <package>   # details about a package
brew search <term>    # find packages by name
```
