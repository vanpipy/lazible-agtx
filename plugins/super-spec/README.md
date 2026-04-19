# super-spec

A high-integrity `agtx` plugin that enforces a **Specification-First** workflow using a gated internal loop.

## How the Gate Works

`super-spec` prevents the common "AI drift" where code doesn't match the plan. It introduces a **Gatekeeper Flag** (`.agtx/audit_passed.md`).

1. **The Plan**: The agent generates a plan and tasks.
2. **The Audit**: The `super-analyze` skill forces the agent to review its own work against the spec.
3. **The Lock**: `agtx` will stay in the Planning phase indefinitely until the audit passes.
4. **The Unlock**: Only when the agent (or you) creates `.agtx/audit_passed.md` will the `Running` phase begin.

## User Guide

### 1. Prerequisites
Ensure `speckit` and `superpowers` tools are available in your agent environment (e.g., `oh-my-openagent`).

### 2. The Internal Loop
If the agent is "stuck" in the Planning phase:
- Check `.agtx/review.md` to see why the audit failed.
- The agent will automatically attempt to fix the plan and re-run the audit.
- You can manually intervene by editing the `plan.md` or `tasks.md` yourself.

### 3. Manual Override
If the AI is struggling to satisfy the auditor but you are happy with the plan, you can manually unlock the next phase by running:
`touch .agtx/audit_passed.md` in the project worktree.

## File Map
- `specs/*/spec.md`: The Source of Truth.
- `.agtx/audit_passed.md`: The Phase Unlock Signal (The "Key").
- `.agtx/review.md`: The Auditor's Feedback Log.
