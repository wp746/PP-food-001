---
name: PP-Food-Runtime-001
description: Use when a host agent must reproduce the PP Food A/B production workflow across different runtimes with minimal prompt drift, strict current-job isolation, fixed model roles, and deterministic Stage A/Stage B routing.
version: 1.0.0
---

# PP-Food-Runtime-001

This is the production control skill. It is intentionally smaller and stricter than the two research skills.

## Entry

Read in this order only:

```text
VERSION
RUNTIME_CORE.md
SETUP_GATE.md
STARTUP_PROTOCOL.md
PROMPT_COMPILER.md
QC_GATE.md
CURRENT_JOB_ISOLATION.md
executors/A_EXECUTOR.md
executors/B_EXECUTOR.md
```

Then load only the current category profile when B requires it.

Do not load `tests/*` during normal production.
Do not load all category profiles.
Do not dump this repository into IMAGE_MODEL.

## User Commands

```text
执行A / A → Stage A only
执行B / B → current Stage A → PASS → Stage B
启动 → enter PRODUCTION after setup passes
```

## Runtime Principle

> Host agent interprets user intent; Runtime Pack controls execution; IMAGE_MODEL receives only a compact current-job payload.
