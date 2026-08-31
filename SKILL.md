---
name: universal-food-commercial-photography
description: Use when a user provides a real food, beverage, bakery, or packaged-product photo and wants a premium commercial photograph while the exact product identity, geometry, vessel or package, arrangement, surface state, and physical relationships must remain highly faithful.
version: 6.4.0
---

# PP-food-001 V6.4.0

## Entry

Start with `BOOTSTRAP.md`.

Normal production uses the **Runtime Minimal Core** only. Do not load `tests/*` or all `references/*` into production context.

Authority:

```text
P0 invariants        → RUNTIME_MANIFEST.md
A operator SOP       → SOP-A.md
runtime capability   → HANDOFF.md
per-job reads        → REQUIRED_READ_SET.md
production gate      → PRE_FLIGHT_CHECKLIST.md
current-job contract → EXECUTION_CONTRACT_TEMPLATE.md
```

## Role

```text
CURRENT USER IMAGE
→ VISION_MODEL
→ CURRENT_JOB_FACTS
→ compact A Execution Contract
→ IMAGE_MODEL reference edit
→ QC
→ targeted retry
→ Stage A PASS
```

## Non-Negotiables

```text
SOURCE_TRUTH = CURRENT_USER_IMAGE
OUTPUT = EXACT 9:16
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container >=98
Plating / Arrangement >=95
Physical Relationship >=95
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
BACKGROUND_ARCHITECTURE > PROP_STYLING
RETRY = TARGETED_NOT_RANDOM
```

Food/Product DNA is conservative. Background architecture, lighting, depth and commercial photography can be aggressive only when they do not alter the product.

## A / B

- `A / 执行A` → Stage A only, follow `SOP-A.md`.
- `B / 执行B` → still complete current Stage A first; only Stage A PASS may enter Stage B.
- No A/B + no clear KV business info → A.
- No A/B + clear KV business info → B, but Stage A still first.

## Anti-Drift Runtime Rule

Every new image creates a new `CURRENT_JOB_FACTS`.

Do not inherit previous-job product facts, brand facts, copy, food entity, category skin, background skin or examples unless the user explicitly asks to continue them.

Do not send the repository to IMAGE_MODEL. Send only:

```text
current reference image
+ compact current-job contract
+ compact current-job prompt
```

## Packaging

For packaged products, package shape, lid/seal, label structure, logo/brand text, visible hard information and relative layout belong to Product DNA. Photography may change; packaging identity may not.

## Fail Closed

If VISION_MODEL cannot read the current image, IMAGE_MODEL cannot perform reference editing, credentials/pass-through are unavailable, the current contract is contaminated/incomplete, or a P0 conflict is unresolved:

```text
PRODUCTION_GATE = BLOCKED
```

## Security

Never store real API keys, private provider configuration, private base URLs, or user credentials in the repository.
