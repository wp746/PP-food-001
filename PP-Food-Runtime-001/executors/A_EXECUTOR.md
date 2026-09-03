# A Executor

Trigger: `A` / `执行A`.

## Input
- current user image;
- optional current product/category/brand notes;
- active runtime configuration.

## Procedure

1. Create new `CURRENT_JOB_ID` and apply `CURRENT_JOB_ISOLATION.md`.
2. VISION_MODEL reads the current image. Never infer unseen content from filename or previous jobs.
3. Build compact A contract:
```text
PRODUCT_LOCK
SURFACE_STATE_LOCK
DIRECT_SUPPORT_LOCK
CURRENT_CATEGORY_ROUTE
BACKGROUND_BIG_IDEA
HERO_PLAN
HARD_NEGATIVES
```
4. Select only current A-relevant category guidance. Do not load all category profiles.
5. Compile the six A prompt blocks from `PROMPT_COMPILER.md`.
6. IMAGE_MODEL performs reference-image generation/editing using the actual current image.
7. VISION_MODEL reads the generated output.
8. Apply `QC_GATE.md` Stage A gate.
9. If fail, map to one targeted retry. Preserve successful dimensions.
10. When PASS, save `CURRENT_JOB_STAGE_A_PASS_IMAGE`.
11. Deliver Stage A only. Do not enter KV automatically after explicit A.

## Core Lock Targets

```text
Food/Product Identity >=95
Key Geometry >=95
Vessel/Packaging >=98
Arrangement/Plating >=95
Physical Relationships >=95
Surface/Material State = PASS
Output = exact 9:16 by default
```

## Creative Freedom
High freedom is allowed only in lighting, environment, depth, camera refinement, background architecture and commercial finish.

## Forbidden
- change product count or identity;
- replace/add/remove major ingredients or package elements;
- re-cook/re-brown/re-glaze product beyond source state;
- replace vessel/package/direct support;
- import previous-job style;
- generate KV typography in A;
- random full regeneration after a local failure.
