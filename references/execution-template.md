# Execution Template V6.1.1

Use this as the final image-edit instruction after building the Fidelity Manifest, resolving food semantics, selecting the scene/category route, and creating the current `EXECUTION_CONTRACT`.

Replace placeholders with concise, source-specific content. Do not load unrelated examples into the IMAGE_MODEL prompt.

---

Use the uploaded image as the authoritative source of truth and strict high-fidelity visual reference for the exact real food shown.

This is a professional **re-photography** task, not a food redesign task, not a re-cooking task, and not a simple venue cleanup.

The objective is dual and non-negotiable:

1. preserve the exact product truth — including structure **and source surface/material state**;
2. re-photograph it as a world-class Food Hero on a category-native premium material stage.

If these goals conflict, preserve product truth and reduce only the risky design move.

## Locked source facts

Preserve with extremely high perceptual fidelity:

{{FIDELITY_MANIFEST_SUMMARY}}

Target preservation:

```text
Food identity >=95
Ingredient geometry >=95
Vessel/container identity >=98
Plating/arrangement topology >=95
Physical relationships >=95
Source surface/material state = LOCKED
```

Visible source pixels are authoritative. Unknown or hidden content is not permission to invent.

## Surface / Material State Lock — mandatory

Current source surface state:

```text
{{SURFACE_STATE_MANIFEST}}
```

The following principle overrides any category appetite instruction:

```text
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
```

Improve **photographic readability**, not the underlying food state.

Allowed:
- better exposure and white balance;
- accurate color recovery;
- controlled specular highlights on gloss already present;
- improved micro-contrast and texture legibility;
- better rim/key light revealing existing crust, moisture, sauce, skin, crumb, translucency or freshness;
- commercial grading that preserves the source's actual browning/doneness/material intensity.

Forbidden:
- making bread darker, more charred or more lacquered than source;
- making meat more cooked/less cooked or more caramelized than source;
- increasing sauce/oil/wetness beyond source;
- turning matte/semimatte surfaces into mirror gloss;
- exaggerating cracks/scoring/burst openings;
- adding condensation, sugar, powder, sesame, garnish, butter, sauce or droplets not supported by source;
- changing source-level color gradient, browning level, char level, doneness, moisture level or gloss level to create appetite.

Core command:

> **REVEAL THE EXISTING PROPERTY. DO NOT AMPLIFY THE PROPERTY BEYOND SOURCE IDENTITY.**

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

Semantics may affect background/stage, supporting props outside the product, material palette, color direction, lighting character and photographic mood.

Semantics must never add/remove ingredients, re-plate, replace vessel/package, change cooking state or redesign the product.

## Subject edit policy

The food, major ingredients, package/vessel, direct support areas, source surface state and meaningful physical contacts are low-edit regions.

Do not:
- reorganize or beautify product geometry;
- replace vessel/package;
- invent ingredients/garnish;
- remove visible major components;
- enlarge or standardize product units;
- change count relationships;
- change cooking/surface state;
- change hand/utensil/direct-support relationships.

**Direct support is locked; generic venue context is not automatically locked.**

For open/unpackaged food in a generic display cabinet, preserve the food, tray/board/liner, count, arrangement, contact logic and source surface state; the cabinet body, shop wall and generic store environment may be translated into a premium Hero Stage unless identity-critical.

## Topology-Preserving Completion — only when needed

Current completion plan:

```text
{{TOPOLOGY_COMPLETION_PLAN}}
```

If the source image does not fully show the serving because of crop/edge framing, you MAY complete only the **same serving/product** when visible evidence supports it.

Completion must preserve:
- ingredient/product identity;
- geometry/cut/scale;
- orientation;
- layer and overlap order;
- density and count relationship;
- source surface/material state;
- sauce/oil/broth state;
- tray/container/support relationship.

Use:

```text
HIGH confidence → natural continuation allowed
MEDIUM confidence → minimum conservative continuation only
LOW / UNKNOWN → do not invent product content; extend environment/crop instead
```

Core command:

> **COMPLETE THE SAME SERVING; DO NOT DESIGN A BETTER SERVING.**

Do not use completion as permission to re-plate, standardize, beautify, add luxury ingredients or create a more dramatic cooking state.

## Food material treatment

{{PRIMARY_FOOD_MODULE}}

{{SECONDARY_FOOD_MODULES}}

Every material/appetite instruction must be filtered through the Surface State Lock. If a module says “glossy / juicy / crisp / charred / caramelized,” apply only to the intensity already visible in the current source.

## Scene treatment

{{SCENE_MODULE}}

Apply scene rules with this precedence:

```text
Food DNA / Source Surface State / Direct Support
> World-Class Hero Stage
> Semantic Material Translation
> Generic Source Venue Appearance
```

If the original environment is identity-critical, preserve what carries identity.

If it is merely a generic display case, counter, wall, cabinet or room, translate it into a category-native premium material stage instead of simply cleaning or warming the venue.

The output must not read as “the same shop photo but nicer” when a Hero Stage is allowed.

## Controlled Hero Reframe

Source camera coordinates are not product DNA.

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

Preserve visible-face proportions, product geometry, count and arrangement, overlap order, direct support/contact plane, believable foreshortening and vessel/tray shape.

Forbidden: extreme low angle, extreme wide-angle distortion, unsupported rotation/viewpoint or moving/removing/duplicating product units.

Goal: **preserve product view geometry, not the accidental snapshot camera position.**

## Multi-product Hero hierarchy

If multiple same-product units are visible, use:

```text
{{MULTI_PRODUCT_HERO_PLAN}}
```

Choose an already-existing foreground unit/cluster as `PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER`; all remaining unchanged units become `SUPPORTING_PRODUCT_FIELD`.

Create hierarchy only with light pool, local sharpness, rim light, contrast, depth-of-field and crop/reframe. Do not physically re-arrange the products.

## Hero spatial stage treatment — mandatory

Build four visibly distinct depth layers:

1. **L1 near-camera foreground** — heavily defocused stage edge / paper / compatible tool edge / restrained identity cue;
2. **L2 Hero plane** — product or primary Hero unit/cluster, tack sharp, inside a clean light pool;
3. **L3 mid-background** — softly defocused category-native premium materials/objects clearly separated behind the Hero;
4. **L4 deep background** — at least two perceptible receding material/light cues, progressive falloff and clean negative space. A single blurred wall/gradient/bokeh field does not count.

Defocus must progress continuously. “Sharp subject + uniformly blurred wall” is a failure.

Treat the Hero with portrait logic: large controlled 45° soft key, precise rear/side rim where materially useful, physically correct contact shadows, visible brightness/color-temperature separation and light falloff away from Hero.

Hero lighting must reveal source materials without changing their actual state.

## Ingredient / tool dressing

Use only restrained category-supported elements outside the food/direct support area. They must be few, low contrast, softly defocused, incapable of being misread as added ingredients and specific to current category.

## Temperature logic

Cold food: zero hot steam; clean/cool material logic where appropriate.

Hot/freshly baked food: warm volume only; steam/smoke/heat haze only if physically supported. “Freshly baked” does not authorize darker browning or more char.

## Appetite rendering

Atmosphere comes from making the **source-true state** more legible.

Correct:
- show existing sauce sheen with better highlight placement;
- show existing moisture with better micro-contrast;
- show existing crust/scoring with side/rim light;
- show existing translucency/condensation if present;
- preserve source color and doneness while improving separation.

Incorrect:
- making the product wetter, darker, crispier, more caramelized, more charred, more glossy or more heavily sauced than source.

The image should trigger appetite because the photography is better, not because the product was changed.

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

Ask internally: if this exact food were replaced by a completely different category, would the stage still work nearly unchanged? If yes, redesign the environment before generating.

## Photography mode

```text
{{PHOTOGRAPHY_MODE}}
```

Cinematic quality is camera/light/material control, not a fixed dark-orange filter.

## Composition and camera

Target aspect ratio:
```text
{{ASPECT_RATIO}}
```

Use commercial Hero composition. You may substantially improve framing and spatial hierarchy while keeping product geometry and source surface state credible.

Avoid extreme lens distortion, warped vessel/tray edges and unsupported viewpoints.

## Color and material realism

Preserve accurate base food colors and source-level material intensity.

Grade the environment around the food, not the food into the environment.

Avoid generic orange warmth, oversaturation, clipped highlights, crushed blacks and obvious filter looks.

Maintain believable gravity, contact shadows, environmental reflections, material response and depth.

## Final quality target

The final image must feel like:
- the exact same individual product/serving from the source;
- the same cooking/doneness/browning/gloss/moisture/surface state;
- re-photographed by an elite commercial food studio;
- on a stage designed specifically for this food category/material character;
- with visible L1/L2/L3/L4 spatial depth;
- with deliberate Hero hierarchy;
- with campaign-grade light sculpting and appetite rendering;
- with any missing in-frame serving area completed only by topology-preserving continuation;
- with the quality jump coming from photography, environment, light, material readability and spatial direction — never re-cooking or product redesign.

## Strict negatives

Strictly avoid:
- changed food/category;
- ingredient substitution/invention/removal;
- changed geometry/count/arrangement;
- changed browning/char/doneness/gloss/moisture/sauce coverage/surface state;
- exaggerated cracking/scoring;
- redesigned plating;
- unsupported completion/invented unseen food;
- vessel/tray/package replacement;
- changed hand/utensil/direct-support relationship;
- invented garnish/luxury ingredients;
- flat backdrop / fake L4;
- generic venue cleanup presented as Hero photography;
- equal-weight inventory look in multi-product scenes;
- café/coffee props automatically applied to bread;
- repetitive generic prop kits;
- excessive steam/smoke;
- pasted-product integration;
- CGI/plastic/waxy/over-lacquered texture;
- extreme HDR/saturation;
- random text/logo/watermark/UI.

CORE COMMAND:

**PRESERVE THE PRODUCT.**

**PRESERVE ITS STRUCTURE AND ITS CURRENT SURFACE / COOKING STATE.**

**MAKE EXISTING APPETITE SIGNALS MORE LEGIBLE; DO NOT MAKE THEM STRONGER THAN THE SOURCE.**

**COMPLETE CROPPED SERVING TOPOLOGY ONLY WHEN EVIDENCE SUPPORTS IT; NEVER RE-PLATE.**

**DESIGN THE STAGE FROM THE FOOD'S OWN MATERIAL CHARACTER.**

**CHANGE THE PHOTOGRAPHY, NOT THE PRODUCT.**