# Project Agent Guidelines

Baseline: `SATSET-AGENTS v1`
Repository: `Satsetx4/model-cek`
Default branch: `main`

This file defines the default engineering behavior for agents working in this repository. Project-specific instructions in more narrowly scoped `AGENTS.md` files or explicit repository contracts may add stricter rules. More restrictive security and permission rules always win.

## Source of truth
- In ChatGPT mode chat, GitHub is the source of truth for this project.
- Do not assume a local workspace is current unless the user explicitly switches to local/Work execution and selects that workspace.
- Inspect relevant repository files, issues, branches, PRs, tests, and documentation before making project-specific claims or changes.
- Never silently expand permissions or execution scope.

## Core engineering behavior
### 1. Think before coding
- Inspect before modifying.
- State material assumptions when they affect correctness or scope.
- Surface meaningful ambiguity instead of choosing a risky interpretation silently.
- Define observable acceptance criteria before non-trivial implementation.
- For multi-step work, use a short plan with a verification check for each step.

### 2. Simplicity first
- Implement only what is required by the task and acceptance criteria.
- Do not add speculative features, abstractions, configuration, or frameworks.
- Prefer existing repository patterns over new mechanisms.
- Choose the smallest implementation that provides the required behavior and safety.

### 3. Surgical changes
- Touch only files and lines required by the task.
- Do not refactor, reformat, or clean up unrelated code.
- Match existing style and naming conventions.
- Remove only dead code or imports made obsolete by your own change.
- Report unrelated defects separately.
- Every changed file must trace directly to the task or its verification.

### 4. Goal-driven execution
- Convert requests into verifiable outcomes.
- For bug fixes, reproduce the defect before fixing when feasible, then prove the reproduction passes.
- For refactors, establish relevant behavior before the change and verify it afterward.
- For workflow or configuration changes, validate syntax and expected behavior where feasible.
- Do not declare completion merely because code was written.

## Standard task loop
```text
request
-> inspect source of truth
-> define acceptance criteria
-> implement the minimum change
-> run focused QA
-> inspect final diff/result
-> report evidence
```

## Testing and QA
- Follow existing repository test/build/lint instructions; do not invent commands when authoritative instructions exist.
- Run the smallest sufficient checks first, then broader validation when risk warrants it.
- Record the exact checks performed and their outcome.
- Never report an unexecuted test as passing.
- If QA cannot run, state the blocker and use the strongest available static or structural verification instead.

## Git and GitHub discipline
- Do not push implementation work directly to the default branch when a reviewable branch/PR path is available or required.
- Keep branches and commits scoped to one task.
- Do not mix unrelated cleanup into a task commit.
- Inspect the changed-file list and final diff before publishing.
- Preserve unrelated existing work.
- Include QA evidence in PRs or completion reports when applicable.

## Delegation and agent handoff
When work is delegated to Antigravity, Work/Codex, or another coding agent, provide:
1. the exact task;
2. observable acceptance criteria;
3. the authoritative repository/ref;
4. explicit constraints and forbidden actions;
5. the evidence that must be reported back.

Delegation is not completion. The delegating agent must verify the returned state and evidence before reporting success to the user. GitHub should contain the durable result for work that must be visible from ChatGPT mode chat.

## Required completion report
```text
STATUS: <completed|partial|failed>
SUMMARY: <what changed and why>
FILES: <changed or inspected paths>
QA: <commands/checks and outcomes>
GIT: <branch/commit/PR when applicable>
LIMITATIONS: <anything not verified>
NEXT: <next action or None>
```

Do not hide failed tests, skipped verification, scope deviations, or unresolved assumptions.

## Completion checklist
- acceptance criteria are satisfied;
- the implementation is no larger than necessary;
- no unrelated refactor or formatting slipped in;
- relevant QA actually ran or its blocker is documented;
- the final diff/result was inspected;
- changed files and QA results are reported;
- GitHub contains the durable result when required.
