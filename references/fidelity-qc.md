# Fidelity Quality Control

Run after image generation/editing. The >=95% target is perceptual and should be judged through explicit invariants, not by pretending to compute exact pixel similarity.

## Critical Failures

Any one of these is an automatic FAIL:

- food category changed;
- major ingredient added, removed or replaced;
- identity-defining ingredient geometry significantly changed;
- serving vessel replaced;
- vessel material changed;
- package redesigned;
- plating significantly rearranged;
- handheld relationship changed;
- shelf/display context incorrectly removed when identity-critical;
- food becomes physically implausible;
- container visibly warped or replaced;
- generated output no longer reads as the same specific serving/product;
- **surface/material state drift**: browning, char, doneness, gloss, moisture, sauce/oil coverage, crust/skin, crack/scoring, cream/frosting, condensation/frost or translucency changed beyond normal photographic rendering;
- **appetite mutation**: a mild source property was made materially stronger only to appear more appetizing/premium;
- **completion invention**: cropped/hidden product areas were filled with unsupported ingredients, different geometry, re-plating, standardized shapes or a different cooking/surface state.

## Fidelity score (100)

Score conservatively:

- Food identity: 20
- Ingredient / product geometry: 18
- Surface / material state: 12
- Container / package identity: 15
- Plating / arrangement topology: 15
- Physical relationships: 8
- Ingredient completeness / topology-preserving completion: 7
- Food color identity: 5

### Interpretation

- 95–100: PASS, assuming no Critical Failure
- 90–94: retry if differences are noticeable
- <90: FAIL

A Critical Failure overrides the numeric score.

## Strong-fidelity questions

### Food identity
Would a reasonable viewer consider this the same specific serving/product, rather than a newly generated similar item?

### Ingredient map
Can each major visible source ingredient be mapped to the output without obvious addition/substitution/deletion?

### Geometry
Do identity-defining food shapes, cuts, widths, thicknesses, counts and layer relationships remain substantially stable?

### Surface / material state
Does the output preserve the same source-level browning, char, doneness, gloss/matte balance, moisture, sauce/oil coverage, crust/skin structure, cracking/scoring and color gradient?

Ask specifically:

> Is the property merely better photographed, or has the property itself become stronger?

If stronger → FAIL / retry.

### Plating / arrangement
Does the source topology remain intact, including central/peripheral placement, topping clusters, sauce/broth coverage, pile/layer structure and repeated-unit overlap?

### Completion
If the original was cropped or incomplete in-frame:
- was only the same serving/product naturally continued?
- did the continuation preserve ingredient identity, geometry, density, overlap, surface state and support relationship?
- was low-confidence unknown content left un-invented?

If not → FAIL.

### Vessel / package
Is it clearly the same vessel/package identity, material, geometry, color and scale?

### Physical relationships
Are hands, utensils, shelf, display case, tray, package and contact surfaces still logically consistent with the source?

## Photography score (100)

- Lighting quality: 20
- Material readability without mutation: 20
- Subject separation: 15
- Composition: 15
- Background/environment quality: 10
- Color grading: 10
- Physical realism: 10

### Interpretation

- 95+: hero output
- 90–94: strong commercial output
- 85–89: commercially acceptable
- <85: photographic upgrade insufficient

## Artifact / mutation check

Reject/retry for:

- warped bowl/plate/cup/package;
- malformed fork/chopsticks/spoon;
- extra/missing fingers affecting hand-food contact;
- food fused into vessel;
- duplicated ingredients;
- melted geometry;
- floating solids;
- impossible liquid surfaces;
- incorrect steam/smoke origin;
- excessive fake steam;
- plastic/waxy texture;
- extreme HDR;
- generic orange cast;
- inconsistent perspective;
- missing contact shadows;
- subject visibly pasted into background;
- source-light browning rendered as dark char;
- source-moderate gloss rendered as lacquer/mirror finish;
- source-natural cracks exaggerated into a different structure;
- added wetness, oil, sauce, sugar, powder, seeds, garnish or condensation unsupported by source;
- completion region that looks more idealized or more cooked than the visible source.

## Acceptance rule

Deliver only when:

```text
FIDELITY SCORE >= 95
AND
PHOTOGRAPHY SCORE >= 85
AND
NO CRITICAL FAILURE
```

A beautiful image with low food fidelity is a failure.

A faithful image with no meaningful photographic improvement is incomplete.

A more appetizing image achieved by changing the product's cooking/surface state is also a failure.

Target:

> HIGH FIDELITY × HIGH PHOTOGRAPHIC UPGRADE × SOURCE-TRUE SURFACE STATE