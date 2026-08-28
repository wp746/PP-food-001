# Execution Template V6.1

Use this as the final image-edit instruction after building the Fidelity Manifest, resolving food semantics, selecting the scene/category route, and creating the current `EXECUTION_CONTRACT`.

Replace placeholders with concise, source-specific content. Do not load unrelated examples into the IMAGE_MODEL prompt.

---

Use the uploaded image as the authoritative source of truth and strict high-fidelity visual reference for the exact real food shown.

This is a professional **re-photography** task, not a food redesign task and not a simple venue cleanup.

The objective is dual and non-negotiable:

1. preserve the exact product truth;
2. re-photograph it as a world-class Food Hero on a category-native premium material stage.

If these goals conflict, preserve product truth and reduce only the risky design move — do not collapse the whole image back into an ordinary snapshot.

## Locked source facts

Preserve with extremely high perceptual fidelity:

{{FIDELITY_MANIFEST_SUMMARY}}

Target preservation:

```text
Food identity >=95
Ingredient geometry >=95
Vessel/container identity >=98
Plating topology >=95
Physical relationships >=95
```

Visible source pixels are authoritative. Unknown or hidden content is not permission to invent.

## Semantic identity

```text
Dish / product name: {{DISH_NAME}}
Name source: {{DISH_NAME_SOURCE}}
Confidence if inferred: {{DISH_CONFIDENCE}}
Category / cuisine: {{CUISINE_TYPE}}
Flavor / material character: {{FLAVOR_PROFILE}}
Primary visible ingredients/materials: {{PRIMARY_INGREDIENTS}}
Cooking method / temperature: {{COOKING_METHOD_AND_TEMPERATURE}}
Semantic route: {{SEMANTIC_ROUTE}}
Mood keywords: {{DISH_MOOD_KEYWORDS}}
```

User-provided identity overrides inference. Low-confidence inference may guide only conservative category-level environment decisions.

Semantics may affect:
- background/stage;
- supporting props outside the product;
- material palette;
- color direction;
- lighting character;
- photographic mood.

Semantics must never add/remove ingredients, re-plate, replace vessel/package, or redesign the product.

## Subject edit policy

The food, major ingredients, package/vessel, direct support areas and meaningful physical contacts are low-edit regions.

Do not:
- reorganize or beautify the product geometry;
- replace vessel/package;
- invent ingredients/garnish;
- remove visible major components;
- enlarge or standardize product units;
- change count relationships;
- change hand/utensil/direct-support relationships.

**Direct support is locked; generic venue context is not automatically locked.**

For open/unpackaged food in a generic display cabinet, preserve the food, tray/board/liner, count, arrangement and contact logic; the cabinet body, shop wall and generic store environment may be translated into a premium Hero Stage unless the venue itself is identity-critical.

## Food material treatment

{{PRIMARY_FOOD_MODULE}}

{{SECONDARY_FOOD_MODULES}}

Enhance only appetizing properties already supported by the source: crust sheen, sauce cling, moisture, crumb texture, translucency, crisp edges, condensation, etc. Do not manufacture unsupported gloss, steam, char, garnish or luxury cues.

## Scene treatment

{{SCENE_MODULE}}

Apply scene rules with this precedence:

```text
Food DNA / direct support
> world-class Hero Stage
> semantic material translation
> generic source venue appearance
```

If the original environment is identity-critical, preserve what carries identity.

If it is merely a generic display case, counter, wall, cabinet or room, translate it into a category-native premium material stage instead of simply cleaning or warming the venue.

The output must not read as “the same shop photo but nicer” when a Hero Stage is allowed.

## Controlled Hero Reframe

Source camera coordinates are not product DNA.

Create a `HERO_REFRAME_PLAN`:

```text
{{HERO_REFRAME_PLAN}}
```

Allowed when fidelity remains credible:
- 9:16 canvas extension;
- crop/recomposition;
- focal-length feel adjustment;
- light-to-moderate camera-height or pitch change;
- stronger foreground/background separation;
- optical emphasis on an existing foreground unit/cluster.

Preserve:
- visible-face proportions;
- product geometry;
- count and arrangement;
- overlap order;
- direct support/contact plane;
- believable foreshortening;
- vessel/tray shape.

Forbidden:
- extreme low angle that invents unseen sides;
- extreme wide-angle distortion;
- unsupported rotation/viewpoint;
- moving/removing/duplicating product units.

Goal: **preserve product view geometry, not the accidental snapshot camera position.**

## Multi-product Hero hierarchy

If multiple same-product units are visible, use:

```text
{{MULTI_PRODUCT_HERO_PLAN}}
```

Choose an already-existing foreground unit or cluster as:

```text
PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER
```

All remaining unchanged units become:

```text
SUPPORTING_PRODUCT_FIELD
```

Create hierarchy only with light pool, local sharpness, rim light, contrast, depth-of-field and crop/reframe. Do not physically re-arrange the products.

The final image must read as **one Hero supported by a product field**, not flat inventory/display stock.

## Hero spatial stage treatment — mandatory

The environment is a deliberately crafted premium material stage, never a flat backdrop and never a generic working venue.

Build four **visibly distinct** depth layers:

1. **L1 near-camera foreground** — heavily defocused stage edge / paper / compatible tool edge / restrained identity cue creating a real spatial entrance;
2. **L2 Hero plane** — product or primary Hero unit/cluster, tack sharp, inside a clean light pool;
3. **L3 mid-background** — softly defocused category-native premium materials/objects clearly separated behind the Hero;
4. **L4 deep background** — at least two perceptible receding material/light cues, progressive falloff and clean negative space. A single blurred wall, one gradient, or one undifferentiated bokeh field does NOT count as L4.

Defocus must progress continuously across layers. “Sharp subject + uniformly blurred wall” is a failure.

Treat the Hero with portrait logic:
- large controlled 45° soft key;
- precise rear/side rim where materially useful;
- physically correct contact shadows;
- visible brightness or color-temperature separation;
- light falloff away from the Hero;
- no stage element competing with the product.

The product should feel monumental and deliberately photographed, not merely well-lit inside a display cabinet.

## Ingredient / tool dressing

Use only restrained category-supported elements outside the food/direct support area.

They must be:
- few;
- low contrast;
- softly defocused;
- incapable of being misread as added ingredients;
- specific to the current product/category, not a generic prop kit.

Do not treat “linen + brass tongs + stone block” or any other recurring trio as automatic premium styling.

## Temperature logic

Cold food: zero hot steam; clean/cool material logic where appropriate.

Hot / freshly baked food: warm volume, restrained physically plausible heat cues only if supported; never smoke merely to signal “premium”.

## Appetite rendering

Render the product's existing appetite signals as the first language of atmosphere.

Examples by property, only when source-supported:
- sauces/oils: controlled mirror highlights;
- fresh surfaces: moisture and micro-texture;
- bread: crust sheen, scoring/crack relief, caramelized shell, readable crumb/soft interior contrast;
- cold drinks: condensation and transparency;
- grilled food: crisp caramelized edges and micro oil reflections.

The food must trigger an immediate “I want to eat this” reaction without becoming plastic, waxy, over-glossed or oversaturated.

## Semantic background treatment

```text
{{SEMANTIC_BACKGROUND_DIRECTION}}
```

Supporting props:

```text
{{SEMANTIC_PROP_DIRECTION}}
```

Color direction:

```text
{{SEMANTIC_COLOR_DIRECTION}}
```

Lighting character:

```text
{{SEMANTIC_LIGHTING_CHARACTER}}
```

Ask internally:

> If this exact food were replaced by a completely different category, would the stage still work nearly unchanged?

If yes, redesign the environment before generating.

## Photography mode

```text
{{PHOTOGRAPHY_MODE}}
```

Cinematic quality is camera/light/material control, not a fixed dark-orange filter. Choose the visual language from the current food category and material character.

## Composition and camera

Target aspect ratio:

```text
{{ASPECT_RATIO}}
```

Use commercial Hero composition, not merely “minimum necessary cleanup”.

You may substantially improve framing and spatial hierarchy while keeping product geometry credible.

Avoid extreme lens distortion, warped vessel/tray edges and unsupported viewpoints.

## Color and material realism

Preserve accurate base food colors.

Grade the environment around the food, not the food into the environment.

Avoid:
- generic orange warmth;
- extreme teal-orange;
- oversaturation;
- clipped highlights;
- crushed blacks;
- obvious filter looks.

Maintain believable gravity, contact shadows, environmental reflections, material response and depth.

## Final quality target

The final image must feel like:
- the exact same individual product / serving from the source;
- re-photographed by an elite commercial food studio;
- on a stage designed specifically for this food category and material character;
- with visible L1/L2/L3/L4 spatial depth;
- with a deliberate primary Hero hierarchy;
- with campaign-grade light sculpting and appetite rendering;
- with enough negative space and depth to support later Stage B KV;
- with a quality jump coming from photography, environment, light, material and spatial direction — never product redesign.

## Strict negatives

Strictly avoid:
- changed food/category;
- ingredient substitution/invention/removal;
- changed geometry/count/arrangement;
- redesigned plating;
- vessel/tray/package replacement;
- changed hand/utensil/direct-support relationship;
- invented garnish/luxury ingredients;
- flat backdrop;
- one blurred wall pretending to be depth;
- two-layer sharpness flatness;
- generic venue cleanup presented as Hero photography;
- equal-weight inventory look in multi-product scenes;
- café/coffee props automatically applied to bread;
- repetitive linen + tongs + stone styling;
- real venue structures unless identity-critical;
- excessive steam/smoke;
- pasted-product integration;
- CGI/plastic/waxy texture;
- extreme HDR/saturation;
- random text/logo/watermark/UI.

CORE COMMAND:

**PRESERVE THE PRODUCT.**

**PRESERVE HOW IT IS BUILT AND SUPPORTED.**

**DO NOT PRESERVE AN ACCIDENTAL SNAPSHOT CAMERA OR GENERIC SHOP BACKGROUND AT THE EXPENSE OF HERO PHOTOGRAPHY.**

**DESIGN THE STAGE FROM THE FOOD'S OWN MATERIAL CHARACTER.**

**CREATE A TRUE HERO HIERARCHY WITHOUT MOVING THE PRODUCT.**

**CHANGE THE PHOTOGRAPHY, NOT THE PRODUCT.**