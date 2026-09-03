# Execution Modes

## Mode A
Trigger: `A` or `执行A`.

```text
CURRENT USER IMAGE
→ CURRENT_JOB_RESET
→ VISION_MODEL
→ COMPACT A CONTRACT
→ FIXED A PROMPT
→ IMAGE_MODEL
→ VISION_MODEL QC
→ TARGETED RETRY if needed
→ STAGE A PASS
```

No KV copy gate and no Stage B.

## Mode B
Trigger: `B` or `执行B`.

```text
CURRENT USER IMAGE
→ CURRENT_JOB_RESET
→ full current A
→ STAGE A QC PASS
→ B COPY GATE
→ CURRENT CATEGORY PROFILE
→ COMPACT B CONTRACT
→ FIXED B PROMPT
→ IMAGE_MODEL using current Stage A PASS reference
→ VISION_MODEL QC
→ TARGETED RETRY if needed
→ FINAL KV PASS
```

## Default Copy Mode
Only explicit user authorization activates:
```text
DEFAULT_COPY_AUTHORIZED = TRUE
```
It permits safe non-factual campaign copy, not invented business facts.
