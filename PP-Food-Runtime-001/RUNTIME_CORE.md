# PP-Food-Runtime-001 Runtime Core

This file is the P0 production authority. If any other runtime file conflicts with it, block production until the conflict is resolved.

## P0-01 — User UX
User speaks naturally. Internal JSON/contracts are hidden unless explicitly requested.

## P0-02 — Model Roles
```text
VISION_MODEL = image understanding + current-job facts + routing + QC
IMAGE_MODEL = reference-image generation/editing only
```
A non-visual host must never guess image content.

## P0-03 — Intent Router
```text
Explicit A / 执行A → Stage A only
Explicit B / 执行B → current Stage A → QC PASS → Stage B
No explicit A/B → host may infer only if intent is obvious; otherwise default A
```
Explicit A always overrides automatic B inference.

## P0-04 — Current Job Isolation
Each new user image creates a new `CURRENT_JOB_ID` and invalidates previous-job product facts, copy, category skin, stage images and prompt fragments unless the user explicitly requests continuation.

## P0-05 — Stage B Reference
```text
STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
```
Raw snapshot and previous-job images are forbidden once current Stage A PASS exists.

## P0-06 — Fidelity First
When design ambition conflicts with product truth:
```text
REDUCE_DESIGN_AGGRESSION = TRUE
REDUCE_PRODUCT_FIDELITY = NEVER
```
Food/product identity, key geometry, vessel/packaging, plating/arrangement, physical relationships and visible surface/material state must remain faithful.

## P0-07 — Product Hero
For B:
```text
1 PRODUCT / FOOD HERO
2 HEADLINE
3 SPATIAL CONCEPT
4 SUBTITLE
5 SLOGAN / SELLING POINTS
6 BUSINESS / UTILITY
```
Headline may be strong; product must remain stronger.

## P0-08 — B Copy Gate
Before Stage B, unless `DEFAULT_COPY_AUTHORIZED = TRUE`:
```text
HEADLINE = required
SUBTITLE = required
AUXILIARY_INFORMATION_COUNT >= 1
```
Ask only for the minimum missing copy. Do not silently invent missing fields.

## P0-09 — Default Copy Authorization
Only explicit user authorization such as `按默认文案来 / 文案你来安排` allows generated soft campaign copy.
Never auto-invent hard facts: phone, address, price, opening hours, origin, certification, awards, history, official endorsement, unverified ingredients/flavor/process, health claims.

## P0-10 — Category Isolation
Every B job re-routes category. Activate:
```text
1 primary category profile
+ optional 1 weak auxiliary profile
```
All-category activation and previous-category skin reuse are forbidden.

## P0-11 — Prompt Payload Boundary
IMAGE_MODEL receives only:
```text
CURRENT_REFERENCE_IMAGE
+ CURRENT_COMPACT_CONTRACT
+ CURRENT_COMPACT_PROMPT
```
Never send full repository Markdown, tests, all profiles, old examples or previous-job data.

## P0-12 — Fixed Compilers
A and B prompts must follow `PROMPT_COMPILER.md`. Host agents may fill current-job fields but may not redesign compiler structure.

## P0-13 — Targeted Retry
Diagnose first. Retry only the failed dimension while preserving successful locks. Random full regeneration is forbidden.

## P0-14 — Exact Output
Default final output is strict 9:16 portrait unless user explicitly requests another ratio and the host supports that override.

## P0-15 — Fail Closed
Block production if any required runtime capability, current reference, current Stage A PASS for B, current contract, copy gate, category route, or unresolved P0 conflict is missing.
