# PP-Food-Runtime-001 V1.0.0

A compact production controller for reproducing the PP Food `执行A / 执行B` workflow across different host agents with less prompt drift.

## Production Goal

The runtime deliberately reduces host-agent freedom.

It fixes:
- A/B routing;
- Stage A → Stage B handoff;
- current-job isolation;
- model roles;
- B copy gate;
- category selection;
- prompt compiler shape;
- QC;
- targeted retry.

## Normal User Flow

```text
install runtime
→ configure VISION_MODEL + IMAGE_MODEL + connection
→ READY
→ user says 启动
→ upload current image
→ 执行A or 执行B
```

## A
```text
current image
→ visual analysis
→ compact A contract
→ fixed A prompt
→ reference-image generation
→ visual QC
→ targeted retry
```

## B
```text
current image
→ full current A
→ Stage A PASS
→ copy gate
→ current category profile
→ compact B contract
→ fixed B prompt
→ Stage B reference-image generation
→ visual QC
→ targeted retry
```

## Anti-Drift Rules

1. Never dump the whole repository into the image model.
2. Never load tests in normal production.
3. Never activate all category profiles at once.
4. Never reuse previous-job entities or visual skin by default.
5. Never let B skip current Stage A.
6. Never let headline outrank product.
7. Never invent business hard facts.
8. Never random-regenerate after a local failure.

## Production Files

```text
SKILL.md
VERSION
RUNTIME_CORE.md
SETUP_GATE.md
STARTUP_PROTOCOL.md
HANDOFF.md
MODEL_CONFIG.md
REQUIRED_READ_SET.md
EXECUTION_MODES.md
CURRENT_JOB_ISOLATION.md
PROMPT_COMPILER.md
QC_GATE.md
RETRY_POLICY.md
FAIL_CLOSED_RULES.md
CATEGORY_PROFILES.yaml
executors/A_EXECUTOR.md
executors/B_EXECUTOR.md
executors/A_CONTRACT_TEMPLATE.md
executors/B_CONTRACT_TEMPLATE.md
```

Development-only:
```text
tests/runtime-contract-tests.md
RELEASE_GATE.md
```

## Source Skills

`PP-food-001` and `PP-food-KV-001` remain research/methodology sources. This Runtime Pack is the production authority for portable deployment.
