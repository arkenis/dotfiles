# My dotfiles

![Terminal](images/terminal.png)

Personal dotfiles with modern shell tooling, optimized for Laravel/PHP development. Features fast startup times, smart directory navigation, and modern CLI tools.

## Contents

**Getting started**

- [Key Features](#key-features)
- [Quick Start](#quick-start) - clone and run `bin/install`
- [What's Included](#whats-included) - [Shell & Prompt](#shell--prompt) · [Modern CLI Tools](#modern-cli-tools) · [Development Tools](#development-tools) · [QuickLook Plugins](#quicklook-plugins)

**Reference**

- [How It Works](#how-it-works) - [Symlinked Files](#symlinked-files) · [Sourced Files](#sourced-files) · [Custom Agnoster Theme](#custom-agnoster-theme)
- [Daily Usage](#daily-usage) - [Smart Navigation](#smart-navigation) · [Laravel/PHP Shortcuts](#laravelphp-shortcuts) · [Data Processing](#data-processing) · [Maintenance Commands](#maintenance-commands)
- [Version Management](#version-management) - [Node.js via fnm](#nodejs-via-fnm) · [PHP & Composer via Homebrew](#php--composer-via-homebrew)
- [Package Management](#package-management) - the Brewfile and global npm and Composer packages

**AI setup**

- [AI Development Setup](#ai-development-setup) - the Claude Code config, version-controlled
  - [Quick Install (Standalone)](#quick-install-standalone) - the AI setup without the rest of the dotfiles
  - [Skills](#skills) - the local skills, grouped by purpose
  - [Plugins](#plugins) - marketplace plugins, preferred over vendored skills
  - [Code Intelligence](#code-intelligence) - Laravel LSP, Intelephense, TypeScript
  - [Agents](#agents) - custom subagents
  - [The Review Workflow](#the-review-workflow) - the six lanes behind `review-code` and `review-pr`
  - [Settings Worth Knowing](#settings-worth-knowing)
  - [Adding New Skills](#adding-new-skills) - and the two rules that decide whether a skill gets used

**Everything else**

- [Customization](#customization) - [Personal Aliases & Functions](#personal-aliases--functions) · [Project-Specific Variables](#project-specific-variables)
- [Post-Installation](#post-installation) · [Tool Comparisons](#tool-comparisons) · [Utilities](#utilities) · [Credits](#credits)

---

## Key Features

- **Custom Agnoster Theme** - Clean powerline prompt with no branch symbols, `•` for changes
- **Version-Controlled AI Setup** - Skills, agents, settings, and instructions for Claude Code, from one source
- **Framework-Aware Code Intelligence** - Laravel LSP, Intelephense, and TypeScript language servers wired into the agent
- **Fast Tools** - fnm, zoxide, ripgrep, bat, eza (all Rust-based for speed)
- **One Command Install** - `bin/install` sets up everything including Claude Code

---

## Quick Start

```bash
git clone git@github.com:arkenis/dotfiles.git ~/.dotfiles
cd ~/.dotfiles
bin/install
```

---

## What's Included

### Shell & Prompt

- **Oh My Zsh** - Framework for managing Zsh configuration (with agnoster theme by default)
- **zoxide** - Smart directory jumping based on frecency
- **fzf** - Fuzzy finder for files and history
- **direnv** - Automatic environment variables per directory

### Modern CLI Tools

- **fnm** - Fast Node.js version manager
- **bat** - Cat with syntax highlighting
- **eza** - Modern ls replacement with icons
- **ripgrep** - Fast grep alternative
- **fd** - Fast find alternative
- **git-delta** - Better git diffs
- **jq** - JSON processor and formatter
- **yq** - YAML processor and formatter
- **bottom** - Modern system monitor

### Development Tools

- **PHP** - Latest version via Homebrew
- **Composer** - Dependency manager via Homebrew
- **Node.js** - LTS version managed via fnm
- **Laravel Valet** - Local development server
- **MySQL** - Database with auto-start

### QuickLook Plugins

Instant file previews in Finder: code files, markdown, JSON, CSV, patches, and archives.

---

## How It Works

### Symlinked Files

The installation creates symlinks from your home directory to the dotfiles repository. This allows you to version control your configuration while keeping files in their expected locations.

| Symlink Location | Points To | Purpose |
|-----------------|-----------|---------|
| `~/.zshrc` | `~/.dotfiles/home/.zshrc` | Main Zsh configuration (Oh My Zsh with custom agnoster theme) |
| `~/.gitconfig` | `~/.dotfiles/home/.gitconfig` | Git configuration with delta diff viewer |
| `~/.global-gitignore` | `~/.dotfiles/home/.global-gitignore` | Global Git ignore patterns |
| `~/.vimrc` | `~/.dotfiles/home/.vimrc` | Vim configuration |
| `~/.vim/` | `~/.dotfiles/home/.vim/` | Vim runtime files |
| `~/.mackup.cfg` | `~/.dotfiles/macos/.mackup.cfg` | Mackup backup configuration |
| `~/.claude/skills` | `~/.dotfiles/config/claude/skills/` | All Claude Code skills (version-controlled) |
| `~/.claude/agents` | `~/.dotfiles/config/claude/agents/` | All Claude Code agents (version-controlled) |
| `~/.claude/CLAUDE.md` | `~/.dotfiles/config/claude/AGENTS.md` | Agent instructions (Claude reads `CLAUDE.md`, not `AGENTS.md`) |
| `~/.claude/settings.json` | `~/.dotfiles/config/claude/settings.json` | Claude Code settings |
| `~/.config/zed/settings.json` | `~/.dotfiles/config/zed/settings.json` | Zed editor settings |
| `~/.config/zed/keymap.json` | `~/.dotfiles/config/zed/keymap.json` | Zed custom keybindings |
| `~/.config/ghostty/config` | `~/.dotfiles/config/ghostty/config` | Ghostty terminal settings |

To manually symlink the Zed configuration (if not using `bin/install`):

```bash
mkdir -p ~/.config/zed
ln -sf ~/.dotfiles/config/zed/settings.json ~/.config/zed/settings.json
ln -sf ~/.dotfiles/config/zed/keymap.json ~/.config/zed/keymap.json
```

### Sourced Files

These files are loaded by `.zshrc` but remain in the dotfiles directory:

- `home/.aliases` - Shell command aliases
- `home/.functions` - Custom shell functions
- `home/.exports` - Environment variables

### Custom Agnoster Theme

The default configuration uses a customized agnoster theme stored in `oh-my-zsh-custom/themes/agnoster.zsh-theme`:

**Customizations:**
- No git branch symbol (cleaner look)
- Uses `•` for unstaged changes instead of `±`
- Powerline arrows for segment separators
- Requires a font with powerline glyphs

**Git Status Symbols:**
- `✚` - Staged changes (files added with `git add`)
- `•` - Unstaged changes (modified files not yet staged)
- Yellow background - Uncommitted changes
- Green background - Clean working directory

---

## Daily Usage

### Smart Navigation

```bash
z dotfiles          # Jump to frequently used directories
zi                  # Interactive directory picker
Ctrl+R              # Fuzzy search command history
Ctrl+T              # Fuzzy find files
Alt+C               # Fuzzy change directory
```

### Laravel/PHP Shortcuts

```bash
a                   # php artisan
p                   # Run Pest/PHPUnit tests
c                   # claude
mfs                 # php artisan migrate:fresh --seed
nah                 # git reset --hard; git clean -df
```

### Data Processing

```bash
# JSON processing with jq
curl api.github.com/users/arkenis | jq
cat composer.json | jq '.require'
php artisan tinker --execute="echo json_encode(User::first());" | jq

# YAML processing with yq
yq '.jobs' .github/workflows/ci.yml
yq -o json docker-compose.yml

# System monitoring
btm                 # Modern system monitor (aliased from top/htop)
```

### Maintenance Commands

```bash
bin/update          # Update all packages and tools
```

---

## Version Management

### Node.js (via fnm)

```bash
fnm install --lts     # Install latest LTS
fnm use lts-latest    # Use latest LTS
fnm install 20        # Install specific version
fnm use 20            # Switch to specific version
fnm list              # Show installed versions
```

### PHP & Composer (via Homebrew)

```bash
brew upgrade php      # Update PHP to latest
brew upgrade composer # Update Composer
```

---

## Package Management

All Homebrew packages are declared in `config/Brewfile`. To add a new tool:

```bash
echo 'brew "neovim"' >> ~/.dotfiles/config/Brewfile
brew bundle --file=~/.dotfiles/config/Brewfile
```

**Complete package list:**

- **Core**: node, php, composer, pkg-config, wget, httpie, ncdu, hub, ack, doctl, 1password-cli, git-secret, imagemagick, mysql, yarn, ghostscript, mackup
- **Modern CLI**: zoxide, bat, eza, ripgrep, fd, git-delta, fnm, fzf, direnv, jq, yq, bottom, zsh-autosuggestions
- **QuickLook**: qlcolorcode, qlstephen, qlmarkdown, quicklook-json, qlprettypatch, quicklook-csv, betterzip, suspicious-package
- **PHP Extensions**: imagick, memcached, xdebug, redis
- **Global npm**: agent-browser, intelephense, typescript-language-server, typescript
- **Global Composer**: laravel/envoy, spatie/phpunit-watcher, laravel/valet, laravel/lsp

---

## AI Development Setup

Everything Claude Code needs lives in `config/claude/`. Conventions come from marketplace plugins rather than vendored copies, so the local skills stay few.

```
config/claude/
├── AGENTS.md          the instructions, symlinked as ~/.claude/CLAUDE.md
├── settings.json      Claude Code settings, permissions, plugins
├── agents/            custom subagents
└── skills/            local skills, plus the laravel-lsp plugin
```

`AGENTS.md` keeps the cross-tool name so upstream changes merge cleanly, and so another harness (Codex, Zed) can read it as is.

### Quick Install (Standalone)

Install just the AI setup without the full dotfiles:

```bash
curl -fsSL https://raw.githubusercontent.com/arkenis/dotfiles/main/bin/install-claude-code | bash
```

That installs the Claude Code CLI and symlinks the config, skills, and agents.

### Skills

All skills live in `config/claude/skills/` and are version-controlled. On a new Mac they are available immediately after the installer runs.

**Review and audit**

| Skill | What it does |
|-------|--------------|
| `review-code` | Runs 6 review lanes in parallel over the working tree, then applies the fixes |
| `review-pr` | Reviews a GitHub PR with the same lanes, gates on CI, merges, thanks the author. Releases only when asked |
| `audit-architecture` | Whole-codebase audit of how state and data are modelled. Read-only, ranked P0 to P3 |
| `explain-changes` | Explains the code on the current branch as an HTML page opened in the browser, written for a reviewer |

**Tooling**

| Skill | What it does |
|-------|--------------|
| `conductor` | Conductor workspaces and sessions, the CLI, the API, deep links, settings, writing briefs |

### Plugins

Coding conventions and most delegation come from plugins enabled in `settings.json`, not from vendored skills. A vendored copy drifts from its source and shadows the plugin version.

| Plugin | Provides |
|--------|----------|
| `euranka-guidelines@euranka` | euranka PHP, Laravel, JavaScript, security, and version-control conventions |
| `bright-guidelines@bright` | The Bright equivalents |
| `laravel@laravel` | Taylor's marketplace, notably the `laravel-simplifier` agent used by the review workflow |
| `superpowers@claude-plugins-official` | Brainstorming, planning, TDD, and debugging workflows |
| `frontend-design@claude-plugins-official` | Frontend design guidance |
| `agent-browser@agent-browser` | Browser automation |
| `marketing-skills@marketingskills` | Marketing, CRO, and SEO skills |
| `cloudflare@cloudflare` | Cloudflare tooling |
| `php-lsp`, `typescript-lsp` | Language servers, see below |

`laravel-lsp` is the one plugin that lives in this repo, under `skills/laravel-lsp/`, because no official plugin exists for it. Any directory under `skills/` with a `.claude-plugin/plugin.json` loads as a plugin named `<name>@skills-dir`.

### Code Intelligence

Three language servers give the agent diagnostics after every edit and real symbol navigation instead of grep.

| Server | Provides | Install |
|--------|----------|---------|
| `laravel-lsp@skills-dir` | Config keys, route names, view paths, translation strings, middleware aliases, and container bindings, in `.blade.php` | `composer global require laravel/lsp` |
| `php-lsp` | PHP types, symbols, references, signatures | `npm i -g intelephense` |
| `typescript-lsp` | TypeScript and TSX intelligence | `npm i -g typescript-language-server typescript` |

Laravel LSP is first-party (announced at Laracon US 2026) and has no official Claude plugin, so `skills/laravel-lsp/` wraps it in a small `.lsp.json`. Its `phpEnvironment` defaults to `auto`, which finds Herd and Valet without configuration.

Claude Code registers **one server per file extension**, so the two PHP servers split the work: Intelephense takes `.php` for types, undefined methods, and references, and Laravel LSP takes `.blade.php` for route names, view paths, and translation strings. To flip that priority, disable `php-lsp` and add `".php"` back to `skills/laravel-lsp/.lsp.json`.

### Agents

Custom subagents live in `config/claude/agents/`.

- `laravel-feature-builder` - Implements new features across models, controllers, migrations, and views

Most delegation now happens through plugins instead, notably the `laravel-simplifier:laravel-simplifier` agent from Taylor's `laravel` marketplace, which is lane 2 of the review workflow.

### The Review Workflow

`review-code` and `review-pr` share one definition of what a review is, in `skills/review-code/references/lanes.md`. Six lanes run in parallel:

1. **Correctness** - bugs, via `/code-review`
2. **PHP simplification** - via the `laravel-simplifier` agent
3. **euranka PHP conventions** - via `euranka-laravel-php`
4. **Laravel practices** - via Laravel Boost's per-repo `laravel-best-practices`
5. **JavaScript** - via `euranka-javascript`, only when JS or TS changed
6. **Security** - authorization, mass assignment, injection, XSS, secrets, SSRF, PII in logs, with `euranka-security` as the org baseline

Findings are deduplicated, and security outranks correctness, which outranks conventions. Both defect lanes require a concrete failure scenario, so "consider adding a null check" does not count as a finding.

The lanes file has a per-harness table, so the same review can run under another harness with its own tools and available subagents.

### Settings Worth Knowing

| Setting | Why |
|---------|-----|
| `permissions.ask` | Always confirms before reading `~/.ssh`, `~/.aws`, Claude credentials, and `.env` files, in every mode |
| `skillOverrides` | Hides 8 bundled skills from the model while keeping them typeable, saving context |
| `cleanupPeriodDays` | Transcript retention, set to a year |
| `defaultMode: auto` | A classifier handles approvals instead of prompting on every step |

### Adding New Skills

Before vendoring a skill, check whether a marketplace plugin provides it. Prefer the plugin.

```bash
# Install a skill (adds directly to your dotfiles)
npx skills add <owner/repo>

cd ~/.dotfiles
git add config/claude/skills/
git commit -m "Add new skill"
```

Two rules that decide whether a skill ever gets used:

1. **The name and description determine everything.** A skill named after a person, or after a quarter of what it does, will not be found. Write the description around the phrases you would actually type.
2. **Keep the body short and push detail into `references/`.** A skill body stays in context for the rest of the session once loaded, while reference files load only when needed.

Browse more skills at [skills.sh](https://skills.sh)

---

## Customization

### Personal Aliases & Functions

Create custom configurations that won't be committed:

```bash
mkdir -p ~/.dotfiles-custom/shell
vim ~/.dotfiles-custom/shell/.aliases
```

These files are automatically loaded by `.zshrc` if they exist.

### Project-Specific Variables

Use `direnv` for automatic environment loading:

```bash
cd my-project
echo 'export DEBUG=true' > .envrc
direnv allow
```

Variables load when you enter the directory and unload when you leave.

---

## Post-Installation

1. **Restore settings** (optional): Run `mackup restore` if you have backups

2. **Migrate history** (upgrading only): Run `migration/migrate-z-to-zoxide.sh` if you have `~/.z`

---

## Tool Comparisons

| Old Tool | New Tool | Why Better |
|----------|----------|------------|
| z.sh / autojump | zoxide | Smarter frecency algorithm, Rust speed |
| nvm | fnm | 40x faster, simpler, Rust-based |
| cat | bat | Syntax highlighting, git integration |
| ls | eza | Icons, tree view, git status |
| grep | ripgrep | 5-10x faster, respects .gitignore |
| find | fd | Simpler syntax, 10x faster |
| diff | delta | Side-by-side diffs, syntax highlighting |
| htop | bottom | Better UI, graphs, Rust-based |

---

## Utilities

The `bin/` directory contains helper scripts:

- **install** - Main installation script (idempotent, safe to re-run)
- **install-claude-code** - Standalone installer for the AI setup: the CLI and the symlinks
- **update** - Update dotfiles, Homebrew, npm, and Composer packages
- **doctor** - Health check and diagnostic tool

---

## TODO

- [ ] Review agents: consider removing `laravel-feature-builder` (partial overlap with the superpowers workflow).
- [ ] Review `config/Brewfile`: candidates for removal are `hub` (deprecated, replaced by `gh`), `ack` (replaced by `ripgrep`), `starship` (using agnoster), `doctl`, `git-secret`, `mackup`.
- [ ] Review `home/.aliases` and `home/.functions`: identify Freek-specific shortcuts to override in `~/.dotfiles-custom/shell/`.

---

## Credits

Forked from [Freek Van der Herten's dotfiles](https://github.com/freekmurze/dotfiles). Maintained by [Jonathan Flammier](https://github.com/arkenis).

See `config/Brewfile` for complete package list.
