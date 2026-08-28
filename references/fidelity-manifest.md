# Fidelity Manifest

Build this manifest internally before editing. Do not expose lengthy internal analysis unless the user asks.

The manifest converts the vague target “>=95% fidelity” into explicit source invariants.

## 1. Subject identity

Record:
- `primary_food_subject`
- `food_category`
- `food_subtype`
- `temperature_state`: hot | warm | room_temperature | cold | frozen | unknown
- `cooking_state`

## 2. Ingredient map

Classify visible ingredients.

### Level A — Critical ingredients
Identity-defining components. Any addition, removal, substitution or major shape change is a Critical Failure.

### Level B — Structural secondary ingredients
Visible supporting ingredients that materially affect the source layout. Preserve when visibly identifiable. Do not add or remove them for aesthetics.

### Level C — Micro details
Small fragments such as sesame seeds, chili seeds, crumbs or micro oil droplets. Minor pixel-level variation is acceptable, but absence must not become abundance.

Suggested internal structure:

```text
critical_ingredients:
- identity
- shape/cut
- approximate count relationship
- location

secondary_ingredients:
- identity
- location
- structural role

micro_details:
- identity
- presence level
```

## 3. Geometry manifest

For identity-defining components record:
- shape
- cut
- thickness
- width
- length relationship
- orientation
- curl
- stacking
- layering
- distribution
- relative scale
- approximate visible count relationship

Do not convert this topology into thicker pieces, more pieces, chunks or a new arrangement.

## 4. Surface / material state manifest

Record source-supported surface state separately from geometry. This is a hard lock, not an appetite suggestion.

Use only relevant fields:

```text
base_color_and_gradient
browning_level
char_level
cooking_doneness
surface_gloss_level
surface_matte_level
moisture_level
sauce_oil_coverage
crust_skin_state
crack_scoring_state
cream_frosting_state
sugar_powder_state
condensation_frost_state
translucency
freshness_cues
```

Rule:

> Improve how clearly the source state is photographed; do not increase the state itself.

Examples of identity drift:
- light browning becoming dark char;
- mild gloss becoming lacquered/mirror-like;
- natural cracks becoming exaggerated burst-open scoring;
- original doneness changing;
- sauce/oil coverage becoming thicker or more abundant;
- natural moisture becoming artificial heavy wetness.

## 5. Vessel / package manifest

Record:
- `container_type`
- `material`
- `color`
- `shape`
- `depth`
- `rim_characteristics`
- `pattern_or_marks`
- `relative_scale`
- `visible_damage_or_use_marks` if identity-relevant

Lighting/reflection may change. Identity may not.

## 6. Plating / arrangement topology

Record:
- dominant center ingredient(s)
- top/bottom relationships
- peripheral ingredients
- sauce/broth coverage
- topping clusters
- pile direction
- layer order
- repeated-unit arrangement
- overlap order
- density pattern

## 7. Physical relationship manifest

If handheld:
- hand side
- grip type
- visible contact points
- food orientation
- hand/product scale

If utensil-held:
- utensil type
- contact location
- lifted food identity
- direction

If shelf/display:
- product position
- direct tray/board/liner relationship
- identity-critical display context, if any

If package:
- open/closed state
- food-package relationship
- package orientation

If tabletop/counter:
- contact plane
- vessel orientation
- contact shadow expectations

## 8. Visible / occluded / unknown / completion confidence

Explicitly distinguish:
- visible and locked information;
- partially occluded information;
- cropped-but-continuable information;
- unknown information.

For any source edge that may require outpainting/completion, assign:

```text
completion_confidence = HIGH | MEDIUM | LOW
```

### HIGH
Visible evidence strongly defines the same serving/product continuation.

### MEDIUM
Some continuation is supported, but only minimal conservative completion is allowed.

### LOW
Do not invent product content. Prefer environment extension, crop adjustment, or natural occlusion.

Rule:

> Unknown ≠ permission to invent.

## 9. Topology-Preserving Completion manifest

When product/plating is cropped or not fully photographed, record what may safely continue:

```text
completion_target:
known_identity_to_continue:
known_geometry_to_continue:
known_orientation_to_continue:
known_layer_overlap_to_continue:
known_density_to_continue:
known_surface_state_to_continue:
known_container_support_to_continue:
forbidden_new_content:
```

Core command:

> Complete the same serving; do not design a better serving.

The completion may extend the same food/plating topology, but cannot re-plate, standardize, beautify or introduce unsupported ingredients.

## 10. Region edit budget

### Region A — Subject Core
Food + major ingredients + vessel/package + surface/material state + contact areas.

Edit freedom: **very low**.

### Region B — Subject Support
Hands, utensils, tray, immediate support plane, direct shelf zone.

Edit freedom: low to moderate.

### Region C — Environment
Background, distant surface, wall, unrelated clutter, secondary props, distant people/lights.

Edit freedom: high.

## 11. Original scene and photography defects

Record one primary scene:
- TABLETOP
- HANDHELD
- RETAIL_SHELF
- DISPLAY_CASE
- RESTAURANT
- STREET_FOOD
- CAFE
- CLEAN_COMMERCIAL_STUDIO
- OTHER

Record actual photographic defects, e.g.:
- flat lighting
- cluttered background
- poor crop
- white-balance error
- weak separation
- harsh highlights
- muddy shadows
- weak material readability
- distracting surface
- poor perspective

This list determines what may be changed. Do not change the product just because the photo is poor.