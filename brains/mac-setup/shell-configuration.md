# Shell Configuration

Setting up zsh, oh-my-zsh, aliases, and dotfiles on macOS.

---

## oh-my-zsh — install and configure

oh-my-zsh is a zsh framework that adds themes, plugins, and a structured place for customisation.

```bash
# Install
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

After install, your config lives at `~/.zshrc` and custom aliases go in `~/.oh-my-zsh/custom/`.

---

## Key zsh files

| File | Purpose |
|------|---------|
| `~/.zshrc` | Main config — plugins, theme, PATH, shell options |
| `~/.zshenv` | Environment variables (loaded for all shells, including non-interactive) |
| `~/.oh-my-zsh/custom/` | Custom aliases and plugins — any `.zsh` file here is auto-sourced |

---

## Adding aliases

**Option A — oh-my-zsh custom folder (recommended)**

Create a file in `~/.oh-my-zsh/custom/`:
```bash
# ~/.oh-my-zsh/custom/aliases.zsh
alias ll="ls -la"
alias gs="git status"
alias gd="git diff"
alias gc="git commit"
alias gp="git push"
alias gl="git log --oneline -10"
```

Files in `custom/` are auto-loaded — no need to source them manually.

**Option B — append to ~/.zshrc**
```bash
echo 'alias ll="ls -la"' >> ~/.zshrc
source ~/.zshrc
```

---

## Useful zsh options

Add to `~/.zshrc`:
```bash
# History
HISTSIZE=10000
SAVEHIST=10000
setopt HIST_IGNORE_DUPS      # don't store duplicate commands
setopt SHARE_HISTORY          # share history between terminal sessions

# Navigation
setopt AUTO_CD               # type folder name to cd into it
setopt CDPATH=$HOME:$HOME/dev  # search these paths when using AUTO_CD
```

---

## Dotfiles — back up and share your config

Dotfiles are the config files that define your environment (`.zshrc`, `.gitconfig`, etc). Back them up so a new machine setup takes minutes.

```bash
# Create a dotfiles repo
mkdir ~/.dotfiles && cd ~/.dotfiles && git init

# Symlink config files into place
ln -sf ~/.dotfiles/.zshrc ~/.zshrc
ln -sf ~/.dotfiles/.gitconfig ~/.gitconfig
```

**What to put in dotfiles:**
- `.zshrc`
- `.zshenv`
- `.gitconfig`
- `Brewfile`
- Custom aliases (`aliases.zsh`)
- SSH config (`~/.ssh/config`)

Commit to a private GitHub repo. On a new machine: clone, run `brew bundle install`, symlink files.

---

## Checking that changes took effect

```bash
# Reload current shell
source ~/.zshrc

# Verify an alias is active
type ll

# See all active aliases
alias | grep "^ll"
```

---

## Common issues

**Alias not found after adding it**
The file wasn't sourced. Either open a new terminal or: `source ~/.zshrc`

**oh-my-zsh custom folder not working**
Files must end in `.zsh` to be auto-sourced. Check: `ls ~/.oh-my-zsh/custom/*.zsh`

**PATH changes not persisting**
Export PATH in `~/.zshenv` (loaded for all shell types), not just `~/.zshrc`.
