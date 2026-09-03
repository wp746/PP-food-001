# B Executor

Trigger: `B` / `执行B`.

## Input
- current user image;
- current user business/copy information;
- active runtime configuration.

## Mandatory Chain

```text
CURRENT USER IMAGE
→ A_EXECUTOR
→ Stage A QC PASS
→ CURRENT_JOB_STAGE_A_PASS_IMAGE
→ B COPY GATE
→ CURRENT CATEGORY ROUTE
→ COMPACT B CONTRACT
→ STAGE B IMAGE_MODEL
→ B QC
→ TARGETED RETRY
```

## Procedure

1. Create/reset current-job state if this is a new image.
2. Execute the full current A path. Do not reuse an old A result.
3. Confirm `CURRENT_JOB_STAGE_A_PASS_IMAGE` exists and passed QC.
4. Build current copy state.
5. Unless `DEFAULT_COPY_AUTHORIZED = TRUE`, require:
```text
HEADLINE
SUBTITLE
AUXILIARY_INFORMATION_COUNT >=1
```
Ask only for the minimum missing field(s). Stop before Stage B until the gate passes.
6. Create `COPY_ALLOWLIST` and `COPY_BLOCKLIST`.
7. Re-route the current product into exactly one primary category profile and optional one weak auxiliary profile.
8. Build compact B contract.
9. Compile the six B prompt blocks from `PROMPT_COMPILER.md`.
10. IMAGE_MODEL receives current Stage A PASS image as the actual reference.
11. VISION_MODEL reads Stage B output and applies `QC_GATE.md`.
12. If fail, run one targeted retry mapped to the failure.
13. Deliver only after B QC passes.

## Copy Authorization
Generated soft copy is allowed only after explicit authorization such as `按默认文案来`.
Hard facts are never invented.

## Product Hero
```text
PRODUCT = visual priority 1
HEADLINE = visual priority 2
```
Typography may be spatial and high-impact, but cannot demote or conceal the product.

## Forbidden
- Stage B directly from raw snapshot;
- previous-job A/B image;
- missing-copy auto-fill without authorization;
- all 12 category profiles active at once;
- previous-job typography/background skin;
- product/packaging/vessel/plating redesign;
- random full-image retries.
