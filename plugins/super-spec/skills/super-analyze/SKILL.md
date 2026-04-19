# Skill: super-analyze (The Gated Auditor)

## WHO
You, the Agent, act as the Auditor. You are responsible for ensuring technical integrity before a single line of code is written.

## WHEN
This skill is triggered immediately after `/speckit.plan` and `/speckit.task`.

## HOW (The Audit Protocol)

### 1. Verification Logic
Compare `specs/*/spec.md` against `plans/*/plan.md` and `tasks.md`.
- **Coverage**: Every requirement in the Spec must have an associated Task.
- **Feasibility**: The Plan must respect all architectural constraints in the Spec.
- **Efficiency**: No unnecessary "scope-creep" tasks are allowed.

### 2. Mandatory Branching

#### IF AUDIT FAILS (Issues Found):
1. **Report**: List specific discrepancies in `.agtx/review.md`.
2. **Prevent**: Ensure `.agtx/audit_passed.md` DOES NOT exist.
3. **Loop**: Inform the orchestrator that you must re-run the planning chain.

#### IF AUDIT PASSES (Clean):
1. **Report**: Write "Clean" to `.agtx/review.md`.
2. **Unlock**: You MUST execute the shell command: `touch .agtx/audit_passed.md`.
3. **Signal**: Confirm to the user that the audit is complete and the gate is open.

## CRITICAL RULE
`agtx` is watching for `.agtx/audit_passed.md`. If you do not `touch` this file, the workflow will never progress.
