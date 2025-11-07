## Contributing

🔗 https://gitlab.com/rgdacosta/classroom_env/-/wikis/home

✉️ If you have ideas or requests - mail me at rdacosta@redhat.com

If you fancy contributing:

Create a branch -> Create a merge request -> Assign me as a reviewer.

# 🛠️ Productivity Enhancements for the Red Hat Training environment

- ✅ General Linux Productivity
- ☸️  OpenShift Courses
- 🤖 Ansible Ansible Courses 

# 🚀 Getting startd
Requires Ansible to be installed. 

```
git clone https://gitlab.com/rgdacosta/classroom_env.git

cd classroom_env

ansible-playbook playbook.yml
```

---

## ✅ General Environment

These settings benefit all users, regardless of technology focus.

### ⚙️ Bash Aliases

| Alias         | Description                                    |
|---------------|------------------------------------------------|
| `..`, `...`   | Navigate up 1 or 2 directories                 |
| `please`      | Run last command with `sudo`                   |
| `decomment`   | Strip comments from files                      |
| `avc`         | Show AVC denials using `ausearch` + `aureport` |
| `mnt`         | List mounted device filesystems                |
| `pwgen`       | Generate a random secure password              |

---

### 🧠 General Bash Functions

| Function            | Description                                                 |
|---------------------|-------------------------------------------------------------|
| `mcd <dir>`         | Make and cd into a directory                                |
| `pastebin <file>`   | Upload file as GitLab public snippet (requires your API key |
| `gnb <branch>`      | Create and push new git branch                              |

---

### 💬 Enhanced Prompt

Shows the current OpenShift project when logged in:
```bash
[user@host folder (my-namespace)] $
```
---

### 🧩 Vim Plugins (General)

| Plugin             | Description                        |
|--------------------|------------------------------------|
| `vim-airline`      | Enhanced status/tabline            |
| `indentLine`       | Vertical indent guides             |
| `vim-commentary`   | Easy commenting/uncommenting       |
| `ale`              | Background linting                 |
| `vim-yaml-folds`   | Smart YAML folding                 |

---

### ☸️ OpenShift Aliases

| Alias               | Description                                                                                                                    |
|---------------------|--------------------------------------------------------------------------------------------------------------------------------|
| `al`                | Admin Login i.e. `oc login -u admin -p redhatocp https://api.ocp4.example.com:6443`                                            |
| `dl`                | Developer Login i.e. `oc login -u developer -p developer https://api.ocp4.example.com:6443`                                    |
| `ccl`               | Central Cluster Login (ACS courses) i.e. `oc login -u admin -p redhatocp https://api.ocp4.example.com:6443`                    |
| `lcl`               | Local Cluster Login (ACM courses) i.e. `oc login -u admin -p redhatocp https://api.ocp4.example.com:6443`                      |
| `mcl`               | Managed Cluster Login (ACM courses) i.e. `oc login -u admin -p redhatocp https://api.ocp4-mng.example.com:6443`                |
| `vl`                | Virtual Admin Login (OpenShift Virt courses) i.e. `oc login -u vt-admin -p vt-redhatocp https://api.ocp4.example.com:6443`     |
| `clustercheck`      | Checks if OpenShift is ready to be used                                                                                        |
| `events`            | Check the project events in chronological order. Usage `events ${project_name}`                                                |
| `podsw`             | Same as `oc get pods -o wide -n ${project_name}`                                                                               |
| `ocd`               | `oc describe`                                                                                                                  |
| `ocp`               | `oc project`                                                                                                                   |
| `ocg`               | `oc get`                                                                                                                       |
| `ocl`               | `oc logs`                                                                                                                      |
| `showtaints`        | Show node taints                                                                                                               |
| `showpods`          | Show all pods and where they are running                                                                                       |
| `showcapacity`      | Show cluster compute capacity                                                                                                  |
| `showallocatable`   | Show allocatable compute capacity                                                                                              |

---

### ☸️ OpenShift Functions

| Function            | Description                                 |
|---------------------|---------------------------------------------|
| `whohas <role>`     | List all users/groups bound to a role       |
| `whomembers <group>`| List members of an OpenShift group          |
| `plogs <pod>`       | Follow logs in current namespace            |

---

### 🔐 OpenShift SSH Virtualization Configuration

Auto-generated in `~/.ssh/config`:

```ssh
Host vm/*
    ProxyCommand virtctl port-forward --stdio=true %h %p
    IdentityFile ~/.ssh/lab_rsa
    User cloud-user

Host vmi/*
    ProxyCommand virtctl port-forward --stdio=true %h %p
    IdentityFile ~/.ssh/lab_rsa
    User cloud-user
```
This allows you to ssh into a VM using `ssh vm/${VM_NAME}` or `ssh vmi/${VM_NAME}`
---

### 🤖 Ansible Aliases

| Alias     | Description                                |
|-----------|--------------------------------------------|
| `ap`      | Run Ansible playbook                       |
| `apsc`    | Check playbook syntax                      |
| `av`      | Show Ansible version                       |
| `acd`     | Show Ansible config                        |
| `aig`     | Graph inventory tree                       |
| `anr`     | Navigator: run with stdout mode            |
| `ansc`    | Navigator: syntax check                    |
| `anch`    | Navigator: check mode                      |
| `anv`     | Navigator: version                         |
| `anig`    | Navigator: inventory graph                 |

---
## 🧪 Ansible Navigator Config

```yaml
ansible-navigator:
  execution-environment:
    image: utility.lab.example.com/ee-supported-rhel8:latest
    pull:
      policy: missing
```

---

### 📘 Vim Plugin Cheat Sheet 

#### ### 1. `indentLine` — Visual Indentation Guides

- Displays vertical lines at each indent level
- Helps navigate YAML and Python visually

```vim
:IndentLinesToggle
```

Recommended setting:

```vim
set expandtab shiftwidth=2 tabstop=2
```

---

#### ### 2. `vim-yaml-folds` — Smart Folding for YAML

```vim
zM     " Close all folds
zR     " Open all folds
zc     " Close current fold
zo     " Open current fold
za     " Toggle current fold
```

Suggested `.vimrc`:

```vim
set foldmethod=expr
set foldexpr=yaml#foldexpr()
set foldlevel=99
```

---

#### ### 3. `ALE` — Asynchronous Linting Engine

- Background linting for YAML, Ansible, Shell, etc.
- Works well with `yamllint`, `ansible-lint`, and `shellcheck`

```vim
]e          " Next error
[e          " Previous error
:ALEFix     " Auto-fix errors
:ALEInfo    " Show ALE debug info
:ALELint    " Force a manual recheck
```

Optional `.vimrc` config:

```vim
let g:ale_linters = {
\ 'yaml': ['yamllint'],
\ 'ansible': ['ansible_lint'],
\}
let g:ale_fixers = {
\ 'yaml': ['prettier', 'yamlfmt'],
\}
```

---

#### ### 4. `vim-commentary` — Quick Comment Toggling

```vim
gcc         " Toggle comment on current line
gc2j        " Comment next 2 lines
gc          " Comment in visual mode
```

---

#### ### 5. `vim-airline` — Modern Statusline

Features:
- Git branch
- Current file
- Errors/warnings (from ALE)

Recommended config:

```vim
let g:airline_theme='dark'
let g:airline_powerline_fonts = 1
```

Navigation:

```vim
:bn      " Next buffer
:bp      " Previous buffer
:b#      " Last buffer
```

---

#### ### 6. `ansible-vim` — YAML + Jinja Syntax

- Smart syntax highlighting and indent rules for Ansible playbooks

Suggested `.vimrc`:

```vim
syntax enable
filetype plugin indent on
set tabstop=2 shiftwidth=2 expandtab
```

Example:

```yaml
- name: Ensure package is installed
  ansible.builtin.dnf:
    name: vim
    state: present
```

---

### 🔄 Recommended Vim Workflow for Ansible/OpenShift

```bash
vim site.yml      # Open file
zM                # Collapse everything
zo                # Open a section
gcc               # Comment out a line
:ALEFix           # Auto-fix errors
```

---

## 🗂️ Dotfiles Deployed

| File                                                  | Purpose                                 |
|--------------------------------------------------------|-----------------------------------------|
| `~/.vimrc`                                             | Core Vim settings                       |
| `~/.nanorc`                                            | Syntax highlighting for Nano            |
| `~/.tmux.conf`                                         | Tmux configuration                      |
| `~/.ansible-navigator.yml`                             | Execution environment config            |
| `~/.config/monitors.xml`                               | Monitor resolution                      |
| `~/.local/share/applications/org.gnome.Terminal.desktop` | GNOME Terminal shortcut              |

---

