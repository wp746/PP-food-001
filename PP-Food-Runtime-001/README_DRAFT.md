# PP-Food-Runtime-001 V1.0.0

Production runtime pack for stable cross-agent reproduction of the PP Food A/B workflow.

## Goal

The runtime is designed to reduce cross-agent drift by minimizing host discretion.

It is not a broad methodology library. It is a production controller.

## User Experience

After setup:

```text
启动
```

Then use:

```text
执行A
执行B
```

A performs only high-fidelity commercial re-photography.
B always performs the current A first, then builds the category-native KV from the current Stage A PASS image.

## Runtime Architecture

```text
User
→ Host Agent
→ Runtime Core
→ A/B Executor
→ Compact Contract
→ Fixed Prompt Compiler
→ IMAGE_MODEL
→ VISION_MODEL QC
→ targeted retry
```

## Anti-Drift Design

- one P0 Runtime Core;
- one current-job state;
- one current reference chain;
- fixed A/B executors;
- fixed six-block prompt compilers;
- one current category profile (+ optional weak auxiliary);
- no full repository prompt dump;
- no tests in production context;
- no previous-job skin/entity import;
- targeted retry only.

## Files

```text
SKILL.md
RUNTIME_CORE.md
SETUP_GATE.md
STARTUP_PROTOCOL.md
HANDOFF.md
REQUIRED_READ_SET.md
CURRENT_JOB_ISOLATION.md
PROMPT_COMPILER.md
QC_GATE.md
CATEGORY_PROFILES.yaml
executors/A_EXECUTOR.md
executors/B_EXECUTOR.md
executors/A_CONTRACT_TEMPLATE.md
executors/B_CONTRACT_TEMPLATE.md
tests/runtime-contract-tests.md
```

## Runtime Dependencies

The host must provide:
- a visual model that can read user and generated images;
- a reference-image capable image model;
- valid API/connection credentials;
- Stage A output → Stage B input pass-through.

## Security

Do not commit real API keys, private base URLs, private credentials or provider-specific secrets.

## Release Rule

Normal production does not load `tests/*`. Tests are used only for development, audit and release regression.
