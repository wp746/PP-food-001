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
- shelf/display context incorrectly removed;
- food becomes physically implausible;
- container visibly warped or replaced;
- generated output no longer reads as the same specific serving/product.

## Fidelity score (100)

Score conservatively:

- Food identity: 25
- Ingredient geometry: 20
- Container / package identity: 15
- Plating topology: 15
- Physical relationships: 10
- Ingredient completeness: 10
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

### Plating
Does the source topology remain intact, including central/peripheral placement, topping clusters, sauce/broth coverage and pile/layer structure?

### Vessel / package
Is it clearly the same vessel/package identity, material, geometry, color and scale?

### Physical relationships
Are hands, utensils, shelf, display case, tray, package and contact surfaces still logically consistent with the source?

## Photography score (100)

- Lighting quality: 20
- Material realism: 20
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

## Artifact check

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
- CGI/3D-render look;
- extreme HDR;
- generic orange cast;
- inconsistent perspective;
- missing contact shadows;
- subject visibly pasted into background.

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

Target:

> HIGH FIDELITY × HIGH PHOTOGRAPHIC UPGRADE
