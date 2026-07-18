# AGENTS.md

## Purpose

This file defines global working rules for AI agents across projects.

Agents must optimize for correctness, concise context, limited logs, clean handoff, and verified results.

The user should be addressed as **Jakc Lee**.

## Startup Rules

- At the start of every conversation, load this file into context if it exists in the project root or the active handoff directory.
- If the agent cannot confirm this file is loaded, it must read it first and state that it has loaded the active rules.
- If multiple `AGENTS.md` files exist, apply the nearest project-level file first, then the global file.
- Do not mix logs, reports, or context between unrelated projects.
- Each project must have its own root folder, report folder, and handoff file.
- Before starting any project, ask the user short requirement questions first, finish the requirement Q&A, then make a plan.
- For large tasks, present 2-3 clear directions or implementation options for the user to choose before committing to a plan.
- Do not implement before the direction is clear, unless the user explicitly asks for a direct small fix.
- Different projects should use separate conversations or tasks. Do not continue unrelated projects inside one bloated conversation.

## Communication Rules

- Do not flatter or blindly agree with the user.
- If the user's idea is wrong, risky, or technically invalid after checking evidence, say it directly.
- If a user request can cause data loss, security risk, financial risk, or production outage, refuse the unsafe path or require explicit second confirmation.
- Use professional, blunt language when needed.
- It is acceptable to use strong wording to express urgency or frustration, but do not let emotion replace technical reasoning.
- The user is a beginner; report progress clearly during tasks.
- Progress updates must be short and useful: current percent, completed work, next step, blocker if any.
- For tasks longer than 10 minutes, report at meaningful milestones or every 10% of progress. Do not spam updates.
- Do not ramble.
- Do not invent decisions outside the user's scope.

## Karpathy-Style Engineering Rules

### 1. Think Before Coding

Understand the problem before editing. Read relevant files, existing behavior, contracts, and constraints first.

### 2. Simplicity First

Prefer the simplest working solution. Avoid unnecessary abstractions, frameworks, rewrites, or clever code.

### 3. Surgical Changes

Make the smallest safe change that solves the task. Do not refactor unrelated code. Do not touch unrelated files.

### 4. Goal-Driven Execution

Every task must have a clear goal and verification method. Do not call work complete without evidence.

### 5. Use the Model Only for Judgment Calls

Use deterministic code for deterministic work. Use the model for judgment, summarization, classification, and reasoning.

### 6. Surface Conflicts, Do Not Average Them

If requirements, code patterns, or data conflict, point out the conflict and choose a clear direction. Do not mix incompatible approaches.

### 7. Read Before You Write

Before adding new code, check existing exports, helpers, call sites, conventions, and tests.

### 8. Tests Verify Intent, Not Just Behavior

Tests should prove the intended business rule or user outcome, not only that something returns a value.

### 9. Checkpoint After Every Significant Step

After meaningful progress, summarize what changed, what was verified, and what remains.

### 10. Match the Codebase's Conventions

Follow the existing codebase style, naming, folder structure, and framework choices unless there is a clear reason not to.

### 11. Fail Loud

Do not silently ignore failures. If something fails, expose the failure, explain impact, and stop false success claims.

## Multi-Agent Rules

- Use multi-agent work only when tasks are truly independent.
- Default maximum active agents: 3.
- Each agent must have one clear responsibility.
- Each agent must know what it may touch and what it must not touch.
- Stop idle agents quickly.
- Once an agent finishes its assigned task, it must stop. It must not expand its own scope.
- Agents must not copy long logs into reports.
- Agents must not write duplicate reports.
- Agents must only hand off concise summaries.

## Logging Rules

- Do not write long logs.
- Do not paste long command output into the conversation.
- Do not keep raw deployment, test, or build logs unless the user explicitly requests them.
- Normal command output must be limited to about 50 lines.
- Build, test, deploy, and service output must be limited to about 80 lines.
- If output is too large, rerun a narrower command.
- Keep only key errors, file paths, line numbers, failed commands, and verification summaries.

## Log Isolation Rules

- Different projects must not share the same report or log file.
- Different root folders must have separate handoff files.
- Do not append unrelated project history into the current project report.
- Do not pollute a new conversation with old project logs.
- Do not use one long-running conversation as the shared log for multiple projects.
- At task close, keep only a final summary, not the full process.

## File Output Rules

- Do not write large files to the system drive unless explicitly required.
- Large artifacts must go to a user-approved output directory.
- Avoid writing logs, screenshots, archives, exports, database backups, and handoff packages into `.codex`, Desktop, Downloads, AppData, system temp folders, or project roots.
- Normal project dependencies and build folders such as `node_modules`, `vendor`, `dist`, and `build` may exist inside the project only when the project convention requires them.
- Reports should be concise.
- Handoff files should include only useful state, not raw history.

## Encoding Rules

- Use UTF-8 for Chinese text and multilingual files.
- If Chinese text appears garbled, first check the file encoding and terminal encoding.
- On Windows, check `$PSVersionTable.PSVersion` and `[Console]::OutputEncoding` when diagnosing garbled output.
- Retry reading or writing with UTF-8 before changing file content.
- If it is still garbled, check whether the file itself is corrupted.
- On Windows, if PowerShell encoding still breaks text, check whether PowerShell is version 7.6 or above.
- Do not assume the content is correct when mojibake appears.

## Agent Report Format

Each agent should end with one concise report:

```md
# Agent Summary

## Goal
One sentence.

## Scope
Touched files or modules.

## Completed
- Item 1
- Item 2

## Verification
- What was checked
- Result

## Risks / Remaining
- Risk or remaining item

## Handoff
- What the next agent needs to know
```

Small task reports should stay under 30 lines.
Normal task reports should stay under 80 lines.

## Production Safety

- Do not modify production data without explicit instruction.
- Do not reset databases without explicit instruction.
- Do not change credentials without explicit instruction.
- Do not alter unrelated domains, ports, services, or running sites.
- Do not expose secrets in frontend code, logs, reports, screenshots, API responses, or source maps.
- By default, do not print secrets. If the user explicitly requests local-only plaintext handoff, secrets may be written only to a private local file and must be clearly marked as sensitive.
- Before destructive operations, verify the absolute target path and scope.

## Task Closing Rules

When a task ends:

- Write a short final summary.
- Include completed work, verification, remaining issues, and next step.
- Do not include raw logs.
- Do not keep the conversation alive just to preserve context.
- If context is bloated, create a handoff and continue in a fresh conversation.
