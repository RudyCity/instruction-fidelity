# Instruction Fidelity

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![AI Agent Skill](https://img.shields.io/badge/Skill-Autonomous%20AI%20Agent-orange.svg)](SKILL.md)
[![Compatibility](https://img.shields.io/badge/Environment-Antigravity%20%7C%20Codex%20%7C%20Claude%20Code%20%7C%20Cursor-green.svg)](SKILL.md)

> **Universal execution discipline and fidelity framework for autonomous AI coding agents.**

Instruction Fidelity guarantees that user directives and negative constraints are executed accurately from prompt to verified completion—eliminating scope drift, premature claims of success, silent omissions, and workspace collisions.

---

## The Problem: Why Coding Agents Drift

Autonomous coding agents often suffer from predictable operational failure modes:
- **Premature Victory**: Declaring a task done immediately after editing code, without running live tests or checking exit codes.
- **Drive-by Refactoring**: Inadvertently reformatting untouched lines, reordering imports, or adding unnecessary dependencies that pollute `git diff`.
- **Silent Omission**: Skipping tricky edge cases, negative constraints, or secondary requirements requested by the user.
- **Concurrent Collisions**: Overwriting uncommitted modifications or files produced by concurrent agents or users in the same workspace.

Instruction Fidelity solves these issues by establishing a non-negotiable operational contract for every tool call and file edit.

---

## The Six Core Laws

1. **Mandatory Interactive Approval Gate (Model 1)**: For every new user prompt, never immediately execute tools or modify files. State the understood intent, scope, and concrete action plan, then stop and wait for user confirmation ("Lanjut" / approval) before executing.
2. **Zero Unrequested Scope Creep**: Modify strictly what is required to satisfy the user request. Never perform unsolicited reformatting, package upgrades, or drive-by refactoring.
3. **Zero Silent Omissions**: Every requirement, edge case, and deliverable must be tracked and addressed. Placeholder comments (`// TODO`, `...`, stubs) are strictly disallowed.
4. **Negative Constraints Are Absolute**: Explicit prohibitions ("do not touch X", "do not add dependencies", "maintain existing signatures") override convenience. Violating a negative constraint is an immediate failure.
5. **Evidence-Gated Completion**: Code explanations are never proof of functionality. Every deliverable must be verified with terminal evidence (compiler output, test suite results, exit code 0) before declaring completion.
6. **Lossless Delegation Cascade**: When delegating work to subagents, swarms, or background processes, preserve all constraints and inspect raw execution diffs before accepting results.

---

## The 5-Phase Execution Cycle

```
[Phase 1: Ingest & Confirm] --> Articulate intent & plan; STOP and wait for user approval ("Lanjut").
       │
[Phase 2: Preflight]        --> Run git status to detect concurrent agents; inspect existing code patterns.
       │
[Phase 3: Execute]          --> Make minimal, atomic code changes tailored strictly to the assigned scope.
       │
[Phase 4: Verify]           --> Run build, unit tests, and live runtime commands; inspect git diff.
       │
[Phase 5: Report]           --> Present terminal evidence, file links, and 3-tier next steps (Must/Good/Nice).
```

### Mandatory 3-Tier Next-Step Recommendations (Phase 5)
Every task summary must conclude with structured, actionable next steps:
1. 🔴 **Must-Have (Prioritas Kritis)**: Critical bug fixes, security gates, or urgent operational dependencies.
2. 🟡 **Good-to-Have (Sangat Dianjurkan)**: Quality improvements, regression test coverage, or workflow automation.
3. 🟢 **Nice-to-Have (Penyempurnaan Lanjutan)**: Optional polish, extended documentation, or future enhancements.

---

## Concurrent Agent Protection

In modern multi-agent or collaborative developer environments, multiple agents or CLI sessions may operate in the same repository simultaneously.

To prevent collisions:
- **Preflight `git status` Check**: Always inspect repository state before modifying files.
- **Detection**: If uncommitted changes or untracked files are detected that were not created by the current task, assume another agent or developer is active.
- **Non-Interference**: Never execute destructive commands like `git checkout .`, `git clean -fd`, or `git restore`.
- **Targeted Staging**: Avoid blanket commands like `git add .` or `git add -A`. Only stage explicitly modified task files.
- **Worktree Isolation**: For complex or conflicting changes, use an isolated `git worktree`.

---

## Reference Guides

This repository includes four deep-dive reference manuals located in [`references/`](references/):

| Guide | Description |
| :--- | :--- |
| [**Constraint Taxonomy & Parsing**](references/constraint-taxonomy-and-parsing.md) | Six-dimensional constraint classification ($C^+$, $C^-$, $C^{env}$, $C^{arch}$, $C^{imp}$, $C^{sec}$) and intent deconstruction. |
| [**Delegation & Multi-Agent Contracts**](references/delegation-and-multi-agent-contracts.md) | Brief schema, non-interference directives, and 3-step parent receipt audits for subagent delegation. |
| [**Rationalization Defense & Failure Modes**](references/rationalization-defense-and-failure-modes.md) | Detailed analysis of the 11 common AI rationalization traps and operational tripwires. |
| [**Verification Protocols & Evidence Ledger**](references/verification-protocols-and-evidence-ledger.md) | The 4-tier verification pipeline (Static, Unit/Regression, E2E/Live, Diff Audit) and tabular evidence tracking. |

---

## Installation & Integration

### Option 1: Google Antigravity & Gemini CLI

Clone or copy this folder directly into your skills directory:

```powershell
# Windows
git clone https://github.com/RudyCity/instruction-fidelity.git "$HOME\.gemini\config\skills\instruction-fidelity"
```

```bash
# macOS / Linux
git clone https://github.com/RudyCity/instruction-fidelity.git ~/.gemini/config/skills/instruction-fidelity
```

### Option 2: Project Workspace Rule (`AGENTS.md`)

Add the following rule block to your project's `AGENTS.md` or `GEMINI.md`:

```markdown
## Execution Discipline
Every task must adhere to Instruction Fidelity:
1. Always run `git status` before touching files to protect concurrent work.
2. Respect all negative constraints and forbidden boundaries.
3. Verify every modification with live terminal commands (exit code 0).
4. Stage only explicitly modified files; avoid blanket `git add .` commands.
```

### Option 3: Claude Code, Cursor & Codex

Reference `SKILL.md` directly in your workspace instructions (`.cursorrules`, `CLAUDE.md`, or system prompt files) to enforce fidelity rules across all interactions.

---

## Example Verification Ledger

Every task tracks progress and evidence using a structured execution ledger:

| ID | Requirement / Constraint | Category | Status | Verification Command | Observable Terminal Evidence |
| :--- | :--- | :---: | :---: | :--- | :--- |
| **R1** | Core logic implementation | $C^+$ | `PASS` | `bun test tests/feature.test.ts` | 6/6 tests passed (24ms) |
| **R2** | Preserve backward compatibility | $C^-$ | `PASS` | `bun test tests/regression.test.ts` | 18/18 tests passed (42ms) |
| **R3** | Clean diff without formatting noise | $C^{imp}$ | `PASS` | `git diff --stat` | 1 file changed, +14, -2 |

---

## Contributing

Contributions, improvements to failure mode catalogs, and platform adapters are welcome. Please open an issue or pull request.

## License

[MIT](LICENSE)
