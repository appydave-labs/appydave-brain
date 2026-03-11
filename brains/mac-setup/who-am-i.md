# Who Am I — Discovering Your Mac Setup

Run these commands to understand what's already installed and configured on this machine.
Share the output with your AI to get personalised setup recommendations.

---

## Quick discovery (run this first)

```bash
echo "=== SYSTEM ===" && sw_vers && echo "" \
  && echo "=== SHELL ===" && echo $SHELL && $SHELL --version 2>&1 | head -1 && echo "" \
  && echo "=== HOMEBREW ===" && (command -v brew &>/dev/null && brew --version | head -1 || echo "Not installed") && echo "" \
  && echo "=== GIT ===" && (command -v git &>/dev/null && git --version || echo "Not installed") && echo "" \
  && echo "=== NODE ===" && (command -v node &>/dev/null && node --version || echo "Not installed") && echo "" \
  && echo "=== RUBY ===" && (command -v ruby &>/dev/null && ruby --version || echo "Not installed") && echo "" \
  && echo "=== PYTHON ===" && (command -v python3 &>/dev/null && python3 --version || echo "Not installed") && echo "" \
  && echo "=== JQ ===" && (command -v jq &>/dev/null && jq --version || echo "Not installed") && echo "" \
  && echo "=== OH-MY-ZSH ===" && ([ -d ~/.oh-my-zsh ] && echo "Installed" || echo "Not installed") && echo "" \
  && echo "=== ITERM2 ===" && ([ -d "/Applications/iTerm.app" ] && echo "Installed" || echo "Not installed") && echo "" \
  && echo "=== VS CODE ===" && (command -v code &>/dev/null && code --version | head -1 || echo "Not installed")
```

Paste the output to your AI with: *"Here's my Mac setup — what do I need to install?"*

---

## Detailed sections

### Operating system

```bash
sw_vers
# ProductName: macOS
# ProductVersion: 15.x.x
# BuildVersion: ...

uname -m
# arm64 = Apple Silicon (M1/M2/M3/M4)
# x86_64 = Intel
```

**Why it matters:** Apple Silicon (arm64) uses Homebrew at `/opt/homebrew/`. Intel uses `/usr/local/`. Some tools have different install paths.

---

### Shell configuration

```bash
echo $SHELL               # current shell (/bin/zsh on modern Macs)
cat ~/.zshrc | head -40   # first 40 lines of your zsh config
ls ~/.oh-my-zsh/custom/   # custom aliases and plugins (if oh-my-zsh installed)
```

---

### Homebrew — what's installed

```bash
# All installed packages
brew list --formula       # CLI tools
brew list --cask          # GUI applications

# Is a specific tool installed?
brew list | grep jq
```

---

### Development tools

```bash
# Node version manager
command -v nvm &>/dev/null && nvm list || echo "nvm not installed"
command -v fnm &>/dev/null && fnm list || echo "fnm not installed"

# Ruby version manager
command -v rbenv &>/dev/null && rbenv versions || echo "rbenv not installed"

# Python version manager
command -v pyenv &>/dev/null && pyenv versions || echo "pyenv not installed"
```

---

### SSH keys

```bash
ls -la ~/.ssh/
# Check for id_ed25519 (modern) or id_rsa (older)
# If empty or missing — you'll need to generate a key for GitHub SSH access
```

Generate a new key:
```bash
ssh-keygen -t ed25519 -C "your@email.com"
# Then add to GitHub: cat ~/.ssh/id_ed25519.pub | pbcopy
```

---

### Git configuration

```bash
git config --list --global
# Should show: user.name, user.email at minimum
```

Set if missing:
```bash
git config --global user.name "Your Name"
git config --global user.email "your@email.com"
```

---

## Interpreting results — what to do next

| Finding | Next step |
|---------|-----------|
| Homebrew not installed | See homebrew-essentials.md |
| oh-my-zsh not installed | See shell-configuration.md |
| No SSH key | Generate one (above) and add to GitHub |
| Node/Ruby/Python missing | See dev-tools.md |
| Want automated setup | See ansible-automation.md |
| git user not configured | Run the config commands above |
