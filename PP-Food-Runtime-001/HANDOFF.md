# PP-Food-Runtime-001 Handoff

This file defines the minimum runtime wiring for a new host agent.

## Required Capabilities

```text
VISION_MODEL
IMAGE_MODEL
REFERENCE_IMAGE_EDIT = TRUE
VISION_CAN_READ_USER_IMAGE = TRUE
VISION_CAN_READ_GENERATED_OUTPUT = TRUE
STAGE_A_OUTPUT_CAN_FEED_STAGE_B = TRUE
CREDENTIAL_PRESENT = TRUE
```

## Recommended Runtime Variables

```text
PP_FOOD_VISION_MODEL
PP_FOOD_IMAGE_MODEL
PP_FOOD_API_BASE_URL
PP_FOOD_API_KEY
```

The exact variable names may differ by host. Never store actual secrets in the Skill repository.

## Startup

1. Load the Runtime Minimal Core.
2. Resolve only missing runtime capabilities.
3. When declared capabilities pass, enter `READY_WAITING_FOR_START`.
4. User says `启动`.
5. Enter `PRODUCTION`.

## Production UX

User only needs to:
- upload current image;
- say `执行A` or `执行B`;
- provide current product/copy information in natural language.

Do not ask the user to understand contracts, category IDs, prompt blocks or internal JSON.

## Failure Recovery

If image reading, reference edit, credential, output readback or A→B pass-through fails:
```text
RUNTIME_STATE = SETUP_GATE
PRODUCTION_GATE = BLOCKED
```
Ask only for the specific missing capability.
