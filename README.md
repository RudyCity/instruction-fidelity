# Instruction Fidelity

Universal execution discipline and fidelity framework for AI coding agents.

## Overview

Instruction Fidelity ensures that AI agents faithfully follow user requirements and negative constraints without scope creep, unverified claims, or silent omissions.

### Core Disciplines
- **Zero Unrequested Scope Creep**: Only modify files explicitly needed for the task.
- **Negative Constraints**: Strictly respect negative constraints and boundaries.
- **Evidence-Gated Completion**: Verify all changes with terminal execution and test evidence before declaring completion.
- **Concurrent Agent Protection**: Always check `git status` before editing files to detect concurrent agents.

## Structure
- `SKILL.md`: Main execution engine and 5-phase execution loop.
- `references/`: Detailed reference documentation and protocols.

## License
MIT
