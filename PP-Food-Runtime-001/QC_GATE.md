# QC Gate

VISION_MODEL must inspect generated results. Self-declared IMAGE_MODEL success is not QC.

## Stage A Gate

Required:
```text
ASPECT = exact 9:16 by default
FOOD_OR_PRODUCT_IDENTITY >=95
KEY_GEOMETRY >=95
VESSEL_OR_PACKAGING >=98
ARRANGEMENT_OR_PLATING >=95
PHYSICAL_RELATIONSHIPS >=95
SURFACE_OR_MATERIAL_STATE = PASS
HERO_READABILITY >=85
PHOTOGRAPHY_QUALITY >=85
CATEGORY_RELEVANCE >=85
NO_PREVIOUS_JOB_CONTAMINATION
NO_CRITICAL_FAILURE
```

Critical failure examples:
- product becomes a different but similar item;
- vessel/package/label structure drifts materially;
- surface state looks re-cooked or materially changed;
- major ingredient/product count changes;
- previous-job style/entity appears;
- final ratio is wrong;
- background is generic and category-agnostic when a specific route was available.

## Stage B Gate

Required:
```text
CURRENT_STAGE_A_REFERENCE_CONFIRMED = TRUE
FOOD_OR_PRODUCT_FIDELITY >=95
VESSEL_OR_PACKAGING >=98
PRODUCT_DOMINANCE = PASS
HEADLINE_PRIORITY = 2
TYPOGRAPHY_ACCURACY = 100%
COPY_ALLOWLIST_ONLY = PASS
CATEGORY_PROFILE_MATCH >=90
SPATIAL_TEXT_SYSTEM = PASS
ONE_BIG_IDEA = PASS
PREVIOUS_SKIN_CONTAMINATION = FALSE
UPPER_BOUND_READINESS >=90 when upper-bound mode is active
```

## Retry Mapping

```text
Product drift            → PRODUCT_LOCK_RETRY
Surface-state drift      → SURFACE_STATE_RETRY
Vessel/package drift     → VESSEL_PACKAGE_RETRY
Wrong ratio              → ASPECT_CORRECTION_RETRY
Weak A background        → BACKGROUND_ARCHITECTURE_RETRY
Wrong B category skin    → CATEGORY_ROUTE_RETRY
Product demotion         → PRODUCT_HERO_RETRY
Flat/weak text system    → SPATIAL_TYPOGRAPHY_RETRY
Typography/copy error    → COPY_ACCURACY_RETRY
Previous-job contamination → CURRENT_JOB_RESET_RETRY
Weak Big Idea            → CREATIVE_CONCEPT_RETRY
```

## Retry Limit
Maximum 3 targeted attempts per stage. Preserve dimensions that already passed. If a hard gate remains unreliable, do not pretend PASS.
