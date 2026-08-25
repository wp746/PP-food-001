---
name: universal-food-commercial-photography
description: Use when editing a user-provided food photo into premium commercial or cinematic food photography while the exact food identity, visible ingredients, geometry, plating, vessel, packaging, hand/product relationship, shelf/display context, or other physical relationships must remain highly faithful to the source.
version: 4.0.0
---

# Universal Food Commercial Photography

## Purpose

Convert an ordinary user-provided food photo into premium commercial / cinematic photography **without redesigning the food**.

The source image is the authoritative visual truth. The task is high-fidelity professional re-photography, not food generation.

Core command:

> **Preserve the product. Upgrade the photography.**

The source food is not raw material for creative reinterpretation. Treat it as the real physical product on a commercial set: the camera, light, environment, background, depth and color grading may change; the product itself does not.

## Success condition

The viewer should believe:

> This is the exact same individual serving or product from the source image, professionally re-photographed by an elite commercial studio.

If the result instead looks like a newly generated, re-plated, luxury-upgraded or reinterpreted version of the food, the edit has failed even if it is visually attractive.

## Perceptual fidelity targets

These percentages are **acceptance targets**, not mathematical pixel-similarity commands. Enforce them through the invariants below.

- Food identity fidelity: >=95%
- Ingredient geometry fidelity: >=95%
- Vessel/container identity fidelity: >=98%
- Plating fidelity: >=95%
- Physical relationship fidelity: >=95%

Photography quality should increase aggressively; product transformation should remain minimal.

## Source-truth rule

Visible source information overrides:

- culinary conventions;
- what this dish “usually” contains;
- aesthetic assumptions;
- brand stereotypes;
- luxury-food conventions;
- the model's preferred composition.

**Source pixels override assumptions.**

Unknown or hidden content is not permission to invent.

When an unseen area must be reconstructed, use **minimum plausible continuation** supported by visible source information.

## Preservation invariants

Never intentionally change identity-defining source facts.

### 1. Food identity

Preserve:

- food category;
- major ingredients;
- clearly visible secondary ingredients;
- cooking method/appearance where visually identifiable;
- serving quantity and portion character.

### 2. Ingredient geometry

Preserve:

- shape;
- cut;
- thickness;
- width;
- length relationships;
- orientation;
- curl;
- stacking;
- layering;
- distribution;
- relative scale;
- major quantity relationships.

Do not make ingredients larger, cleaner, thicker, more symmetrical or more expensive-looking simply to improve aesthetics.

### 3. Vessel / package identity

Treat the serving vessel or package as part of product identity.

Preserve with extremely high fidelity:

- type;
- material;
- color;
- geometry;
- depth;
- rim characteristics;
- visible pattern or surface marks;
- relative scale.

Never replace an ordinary real vessel with a more premium one.

Examples of forbidden substitutions:

- white ceramic bowl -> black ceramic bowl;
- plastic cup -> glass cup;
- paper box -> ceramic plate;
- iron pan -> stone plate;
- original branded package -> redesigned package.

### 4. Plating topology

Preserve:

- which ingredients are above/below others;
- central vs peripheral placement;
- sauce/broth coverage;
- topping concentration;
- overall stacking and layering logic.

Do not beautify by re-plating.

### 5. Physical relationships

Preserve meaningful source relationships such as:

- hand-food grip and orientation;
- chopstick/fork/spoon contact;
- food-package relationship;
- product-shelf relationship;
- food-display-case context;
- food-tray/counter/table contact;
- container/support relationship.

Do not convert handheld food to tabletop photography. Do not move a shelf product into a studio-table scene. Do not remove meaningful display context.

## Priority order

When instructions conflict, preserve in this order:

1. Food identity
2. Major ingredient identity
3. Ingredient geometry
4. Vessel / packaging identity
5. Physical relationships
6. Plating
7. Ingredient/material realism
8. Food color
9. Composition
10. Lighting
11. Background
12. Props
13. Atmosphere

Never sacrifice levels 1–6 to improve levels 9–13.

## Region edit budget

Mentally separate the image into three edit zones.

### Region A — Subject Core

Includes:

- food;
- major ingredients;
- vessel/package;
- food-hand/utensil contact areas.

Edit budget: **very low**.

Allowed changes are mainly:

- exposure correction;
- color correction;
- realistic light integration;
- visibility of existing texture;
- controlled specular highlights;
- very minor cleanup that does not alter identity.

Target visual preservation: roughly 95–100%.

### Region B — Subject Support

Includes:

- hands;
- utensils;
- tray;
- immediate table/counter support;
- shelf zone directly supporting the product.

Edit budget: **low to moderate**.

May improve lighting, cleanliness, small defects and depth, but must preserve physical relationships.

### Region C — Environment

Includes:

- background;
- distant table/surfaces;
- walls;
- unrelated clutter;
- distant people;
- secondary props;
- environmental lights.

Edit budget: **high**.

This is the primary creative area. It may be cleaned, relit, softened, reorganized or contextually replaced if the source environment has little identity value.

## Minimum necessary subject change

All subject-side modifications must follow:

> **Minimum Necessary Subject Change**

If the existing noodle width is clear, do not redraw the noodles. Improve only visibility of moisture, translucency or highlights already supported by the source.

If fried food already has crisp texture, reveal that texture; do not regenerate a larger, more golden, more regular version.

If the bowl is complete, keep it; do not recreate a more attractive bowl.

## Appetite enhancement boundary

Do not use “make it much juicier,” “add more steam,” “make it more luxurious,” or similar instructions that encourage product drift.

Instead use this rule:

> Improve the visibility and photographic rendering of appetizing physical properties that already exist in the source food. Do not create appetizing properties unsupported by the source.

Examples:

- Existing red oil may receive better reflection; clear broth must not become red oil.
- Existing meat juice may become easier to see; dry food must not become artificially dripping.
- Existing grill char may become clearer; lightly browned food must not become deeply charred.

## Outpainting / aspect-ratio changes

If the target aspect ratio requires extension:

> **Continuation, not reinvention.**

Only extend the same:

- food;
- vessel;
- package;
- hand;
- tray;
- shelf;
- table/contact plane;
- contextually compatible environment.

Never use outpainting as permission to add ingredients, redesign plating, replace the vessel or invent hidden layers.

## Internal analysis workflow

Before editing, internally identify:

1. Primary food subject
2. Food category/subtype
3. Temperature state
4. Critical ingredients
5. Structural secondary ingredients
6. Distinctive geometry
7. Vessel/package identity
8. Physical relationships
9. Original scene
10. Main photographic problems
11. Appropriate food material module(s)
12. One primary scene module
13. Photography mode

Create a fidelity manifest using `references/fidelity-manifest.md`.

## Module loading rule

Do **not** load every module.

For each image, normally load:

- one primary food module;
- zero to two secondary material modules;
- one primary scene module.

Examples:

- beef noodle soup -> NOODLES + HOT_SOUP + MEAT; scene RESTAURANT or TABLETOP;
- fried chicken -> FRIED + MEAT; one scene;
- strawberry cream cake -> CAKE/DESSERT + FRUIT; DISPLAY_CASE or CAFE;
- packaged chips on shelf -> PACKAGED_FOOD; RETAIL_SHELF;
- handheld iced coffee -> COLD_DRINK; HANDHELD.

Read `references/food-modules.md` and `references/scene-modules.md` only as needed.

## Photography mode

Select one:

### NATURAL_COMMERCIAL

For fresh, light, delicate or daylight-friendly subjects such as salads, fruit, breakfast, bakery, refined desserts and some café scenes.

Characteristics:

- soft natural light;
- clean highlights;
- fresh color;
- bright but controlled exposure;
- subtle editorial atmosphere.

### CINEMATIC_COMMERCIAL

Default for most food photography.

Characteristics:

- directional soft light;
- controlled highlights;
- rich but natural shadows;
- clear depth separation;
- premium environmental atmosphere;
- cinematic tonal control without cliché.

### DRAMATIC_COMMERCIAL

For barbecue, hotpot, spicy food, iron-plate food, night markets, some soups and strongly atmospheric subjects.

Allows:

- deeper shadows;
- stronger but controlled rim light;
- physically justified heat atmosphere;
- restrained steam/smoke;
- higher contrast.

Subject preservation rules do not loosen.

## Cinematic is not a preset

Cinematic does **not** automatically mean:

- dark;
- amber;
- smoky;
- teal-orange;
- shallow-focus;
- high contrast.

Cinematic means purposeful light, controlled color, readable materials, deliberate composition and believable depth appropriate to the actual food.

Do not default every image to dark wood + amber light + ceramic props.

## Environment policy

Ask two questions:

1. Does the original environment carry identity/context value?
2. Does it harm presentation?

If the environment has meaningful context (night market, retail shelf, café, bakery display case, street stall), **enhance rather than replace**.

If the environment is meaningless or damaging (random clutter, unattractive wall, poor generic tabletop), it may be substantially redesigned or replaced, but the new environment must be:

- contextually plausible;
- perspective-compatible;
- scale-compatible;
- lighting-compatible;
- contact-plane compatible.

The subject must not look pasted into a new scene.

## Physical realism

Maintain realistic:

- gravity;
- liquid behavior;
- steam origin;
- smoke origin;
- condensation;
- contact shadows;
- environmental reflection;
- utensil contact;
- hand pressure/contact.

Steam is only for physically hot food and must be subtle. Cold food and cold drinks must not steam. Smoke is only for contexts that physically justify it. Flying ingredients are disabled by default.

## Final execution

Assemble the image-edit instruction using `references/execution-template.md` plus the selected food and scene modules.

Then generate/edit the image.

## Post-generation validation

After generation, run `references/fidelity-qc.md`.

A result passes only when:

- Fidelity score >=95/100;
- Photography score >=85/100;
- no Critical Failure is present.

A beautiful output with low product fidelity is a failure.

A perfectly faithful output with little photographic improvement is incomplete.

Target:

> **HIGH FIDELITY × HIGH PHOTOGRAPHIC UPGRADE**

If the output fails, use `references/retry-policy.md` and retry based on the specific failure. Do not simply regenerate randomly.
