# Ansible Automation — Programmatic Mac Setup

Ansible lets you define your entire Mac configuration as code and replay it on any machine.
Instead of following a checklist manually, you run one command and Ansible does everything.

---

## Why bother?

- New Mac setup takes 20 minutes instead of a day
- Every machine is configured identically
- Changes are tracked in git
- Shareable — others can provision their Mac the same way

---

## How it works

Ansible is agentless — no server needed. You run it locally and it configures the local machine.

```bash
# Run the playbook on your own machine
ansible-playbook site.yml --ask-become-pass
```

---

## Basic structure

```
mac-setup/
├── site.yml                    # Main playbook — what roles to run
├── roles/
│   ├── homebrew/               # Install brew packages
│   │   ├── tasks/main.yml
│   │   └── defaults/main.yml   # List of packages
│   ├── shell/                  # Configure zsh, oh-my-zsh
│   │   ├── tasks/main.yml
│   │   └── templates/          # .zshrc, .zshenv templates
│   └── languages/              # Install Node, Ruby, Python
│       └── tasks/main.yml
```

---

## Minimal starter playbook

`site.yml`:
```yaml
- name: Provision macOS development environment
  hosts: localhost
  connection: local

  roles:
    - homebrew
    - shell
    - languages
```

`roles/homebrew/defaults/main.yml`:
```yaml
homebrew_formulae:
  - git
  - jq
  - gh
  - tree
  - ripgrep

homebrew_casks:
  - iterm2
  - visual-studio-code
```

`roles/homebrew/tasks/main.yml`:
```yaml
- name: Install Homebrew formulae
  community.general.homebrew:
    name: "{{ item }}"
    state: present
  loop: "{{ homebrew_formulae }}"

- name: Install Homebrew casks
  community.general.homebrew_cask:
    name: "{{ item }}"
    state: present
  loop: "{{ homebrew_casks }}"
```

---

## Install Ansible

```bash
brew install ansible

# Install community collection (includes homebrew module)
ansible-galaxy collection install community.general
```

---

## Running the playbook

```bash
# Dry run — see what would change, don't apply
ansible-playbook site.yml --check

# Apply
ansible-playbook site.yml --ask-become-pass
```

---

## Reference implementations

The [appydave-labs/appydave-brain](https://github.com/appydave-labs) ecosystem uses Ansible
to provision a 3-Mac setup. See the `agent-os` project for a real-world example of:

- Role-based structure (homebrew, shell, languages, applications, repos)
- Machine-group variables (workstation vs headless vs creator)
- Idempotent provisioning (safe to run multiple times)

---

## When Ansible makes sense

| Situation | Use Ansible? |
|-----------|-------------|
| Setting up one personal Mac | Maybe — the overhead may not be worth it |
| Setting up 2+ Macs to match | Yes |
| Onboarding new team members | Yes |
| Reproducing a setup after a wipe | Yes |
| Quick one-time installs | No — just use brew |
