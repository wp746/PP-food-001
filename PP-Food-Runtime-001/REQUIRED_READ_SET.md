# Runtime Read Set

The purpose of this file is to prevent both under-reading and over-reading.

## Cold Start Minimal Core

Read exactly:
```text
VERSION
RUNTIME_CORE.md
SKILL.md
SETUP_GATE.md
STARTUP_PROTOCOL.md
HANDOFF.md
PROMPT_COMPILER.md
QC_GATE.md
CURRENT_JOB_ISOLATION.md
```

Do not read `tests/*` during normal production.
Do not preload `CATEGORY_PROFILES.yaml` into IMAGE_MODEL.

## A Job
Read/use:
```text
executors/A_EXECUTOR.md
executors/A_CONTRACT_TEMPLATE.md
```
VISION_MODEL may inspect only the current category-relevant profile information when needed for background semantics.

## B Job
Read/use:
```text
executors/B_EXECUTOR.md
executors/B_CONTRACT_TEMPLATE.md
```
Then select exactly one primary profile and optional one weak auxiliary profile from `CATEGORY_PROFILES.yaml`.

## Context Budget Rule

```text
FULL_REPO_LOAD = FORBIDDEN
ALL_CATEGORY_LOAD = FORBIDDEN
PREVIOUS_JOB_EXAMPLES = FORBIDDEN
TESTS_IN_RUNTIME_CONTEXT = FORBIDDEN
```

The host must compile a current-job contract before calling IMAGE_MODEL.
