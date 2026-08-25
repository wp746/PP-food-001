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

Examples: noodles, fish slices, burger patty, main meat, cake body, sushi fish, pizza's dominant toppings.

### Level B — Structural secondary ingredients

Visible supporting ingredients that materially affect the source layout.

Examples: greens, pickles, cheese, sauce, cream, peppers, bean sprouts.

Preserve when visibly identifiable. Do not add or remove them for aesthetics.

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

Example:

```text
fish slices:
- thin slices
- approximately five dominant visible pieces
- overlapping fan-like distribution
- green peppers concentrated near top/center
```

Do not convert this topology into thicker pieces, more pieces, chunks or a new arrangement.

## 4. Vessel / package manifest

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

## 5. Plating topology

Record:

- dominant center ingredient(s)
- top/bottom relationships
- peripheral ingredients
- sauce/broth coverage
- topping clusters
- pile direction
- layer order

## 6. Physical relationship manifest

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
- shelf/display relationship
- key neighboring context

If package:

- open/closed state
- food-package relationship
- package orientation

If tabletop/counter:

- contact plane
- vessel orientation
- contact shadow expectations

## 7. Visible vs hidden content

Explicitly distinguish:

- visible and locked information;
- partially occluded information;
- unknown information.

Rule:

> Unknown ≠ permission to invent.

When unseen regions need extension, infer only the minimum plausible continuation supported by visible evidence.

## 8. Region edit budget

Classify:

### Region A — Subject Core
Food + major ingredients + vessel/package + contact areas.

Edit freedom: very low.

### Region B — Subject Support
Hands, utensils, tray, immediate support plane, direct shelf zone.

Edit freedom: low to moderate.

### Region C — Environment
Background, distant surface, wall, unrelated clutter, secondary props, distant people/lights.

Edit freedom: high.

## 9. Original scene and photography defects

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
