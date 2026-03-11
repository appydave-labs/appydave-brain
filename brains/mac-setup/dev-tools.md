# Dev Tools

Installing and managing Node, Ruby, Python, and the editors/utilities that support daily development.

---

## Node via nvm

nvm (Node Version Manager) lets you switch Node versions per project.

```bash
# Install nvm (via Homebrew)
brew install nvm

# Add to ~/.zshrc (brew will tell you this — don't skip it)
export NVM_DIR="$HOME/.nvm"
[ -s "/opt/homebrew/opt/nvm/nvm.sh" ] && \. "/opt/homebrew/opt/nvm/nvm.sh"

# Reload shell
source ~/.zshrc

# Install Node LTS
nvm install --lts
nvm use --lts
nvm alias default node   # make LTS the default

# Verify
node --version
npm --version
```

**Per-project version:** Create a `.nvmrc` file in the project root:
```
20.11.0
```
Then `nvm use` picks it up automatically.

---

## Ruby via rbenv

```bash
# Install rbenv
brew install rbenv ruby-build

# Add to ~/.zshrc
eval "$(rbenv init - zsh)"

# Install Ruby
rbenv install 3.3.0
rbenv global 3.3.0

# Verify
ruby --version
```

---

## Python via pyenv

```bash
# Install pyenv
brew install pyenv

# Add to ~/.zshrc
export PYENV_ROOT="$HOME/.pyenv"
export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"

# Install Python
pyenv install 3.12.0
pyenv global 3.12.0

# Verify
python3 --version
pip3 --version
```

---

## VS Code — command line integration

```bash
# Install (if not already via brew cask)
brew install --cask visual-studio-code

# Enable 'code' command in terminal
# Open VS Code → Cmd+Shift+P → "Shell Command: Install 'code' command"

# Open current folder
code .

# Open a specific file
code ~/dev/myproject/src/app.ts
```

**Useful extensions for developers:**
- GitLens — enhanced git history and blame
- GitHub Copilot — AI code completion
- Prettier — code formatter
- ESLint — JavaScript linting
- Even Better TOML / YAML / etc — syntax support

---

## iTerm2 — terminal setup

```bash
brew install --cask iterm2
```

**Key settings to configure:**
- Preferences → Profiles → Keys → Natural Text Editing (option+arrow, cmd+delete work as expected)
- Preferences → General → Closing → "Quit when all windows are closed"

**Split panes:**
- `Cmd+D` — split vertically
- `Cmd+Shift+D` — split horizontally
- `Cmd+[` / `Cmd+]` — move between panes

---

## GitHub CLI (gh)

```bash
brew install gh

# Authenticate
gh auth login
# Choose: GitHub.com → HTTPS or SSH → Login with browser

# Verify
gh auth status
```

After auth, `gh repo clone`, `gh pr create`, `gh pr view --web` all work without tokens.

---

## Useful utilities

```bash
brew install \
  bat \       # cat with syntax highlighting (alias: bat file.js)
  eza \       # modern ls replacement (alias: ls="eza --icons")
  delta \     # better git diff output
  tldr        # practical man pages (tldr git push)
```

Add to `~/.zshrc` or `~/.oh-my-zsh/custom/aliases.zsh`:
```bash
alias cat="bat"
alias ls="eza --icons"
```
