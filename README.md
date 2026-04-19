# 💤 Lazible Agents-Tmux-X

A tmux-based agent execution and worktree management system with a curated plugin setup.

## Overview

`agtx` (Agents-Tmux-X) provides a configuration framework for running AI agents in isolated tmux sessions with worktree support, theme customization, and plugin extensibility. This repository contains the Lazible configuration with curated plugins and theme settings.

## Prerequisites

- **tmux** — agent sessions run in a dedicated tmux server
- **gh** (optional) — GitHub CLI for PR operations

## Quick Start

### 1. Install agtx

```bash
curl -fsSL https://raw.githubusercontent.com/fynnfluegge/agtx/main/install.sh | bash
```

### 2. Clone this config repository

```bash
git clone https://github.com/vanpipy/lazible-agtx.git ~/.config/agtx
```

### 3. Run agtx

```bash
cd your-project && agtx
```

### 4. Dashboard mode (manage all projects)

```bash
agtx -g
```

## Configuration

Edit `~/.config/agtx/config.toml` to customize:

### General Settings

| Key | Default | Description |
|-----|---------|-------------|
| `default_agent` | `"opencode"` | The default agent to use |
| `fullscreen_on_enter` | `false` | Whether to enter fullscreen when attaching |

### Worktree Settings

| Key | Default | Description |
|-----|---------|-------------|
| `worktree.enabled` | `true` | Enable/disable worktree creation |
| `worktree.auto_cleanup` | `true` | Auto-cleanup completed worktrees |
| `worktree.base_branch` | `""` | Base branch for worktrees (auto-detected if empty) |
| `worktree.worktree_dir` | `".agtx/worktrees"` | Directory for worktree storage |

### Theme Colors

| Key | Default | Description |
|-----|---------|-------------|
| `color_selected` | `#ead49a` | Selected item highlight |
| `color_normal` | `#5cfff7` | Normal text |
| `color_dimmed` | `#9C9991` | Dimmed/secondary text |
| `color_text` | `#f2ece6` | Main text color |
| `color_accent` | `#5cfff7` | Accent/highlight color |
| `color_description` | `#C4B0AC` | Description text |
| `color_column_header` | `#a0d2fa` | Column headers |
| `color_popup_border` | `#9ffcf8` | Popup borders |
| `color_popup_header` | `#69fae7` | Popup headers |

## Plugins

Place plugins in the `plugins/` directory.

### Included Plugins

#### super-spec

A spec-driven workflow plugin that enforces a **Specification-First** workflow using a gated internal loop.

**How the Gate Works:**

1. **The Plan**: The agent generates a plan and tasks
2. **The Audit**: The `super-analyze` skill forces the agent to review its own work against the spec
3. **The Lock**: `agtx` will stay in the Planning phase indefinitely until the audit passes
4. **The Unlock**: Only when the agent creates `.agtx/audit_passed.md` will the Running phase begin

**User Guide:**

- Check `.agtx/review.md` to see why the audit failed
- The agent will automatically attempt to fix the plan and re-run the audit
- Manually intervene by editing the `plan.md` or `tasks.md` yourself
- Manual override: `touch .agtx/audit_passed.md` in the project worktree

**File Map:**
- `specs/*/spec.md`: The Source of Truth
- `.agtx/audit_passed.md`: The Phase Unlock Signal
- `.agtx/review.md`: The Auditor's Feedback Log

## Projects

The `projects/` directory stores project state databases. Each project gets its own `.db` file for tracking state across sessions.

## Keyboard Shortcuts

| Key | Action |
|-----|--------|
| `h/l` or `←/→` | Move between columns |
| `j/k` or `↑/↓` | Move between tasks |
| `o` | Create new task |
| `R` | Enter research mode |
| `↩` | Open task (view agent session) |
| `Ctrl+f` | Fullscreen attach to task's tmux session |
| `m` | Move task forward in workflow |
| `r` | Resume task / Move back |
| `d` | Show git diff |
| `x` | Delete task |
| `/` | Search tasks |
| `P` | Select spec-driven workflow plugin |
| `q` | Quit |

## See Also

- [agtx documentation](https://github.com/fynnfluegge/agtx#readme) - Full documentation
