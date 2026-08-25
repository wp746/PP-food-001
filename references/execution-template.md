# Execution Template V5

Use this as the final image-edit instruction after building the fidelity manifest, resolving dish semantics, and selecting the relevant food, scene and semantic modules.

Replace placeholders with concise, source-specific content. Do not load unrelated modules.

---

Use the uploaded image as the authoritative source of truth and strict high-fidelity visual reference for the exact real food shown.

This is a professional re-photography task, **not a food redesign task**.

The primary objective is to preserve the exact food subject while substantially improving the photography and designing an environment that is semantically appropriate to the specific dish.

## Locked source facts

Preserve with extremely high perceptual fidelity:

{{FIDELITY_MANIFEST_SUMMARY}}

Treat all visible source information as authoritative. Do not infer additional food content simply because it is common for this type of dish. Unknown or hidden content is not permission to invent.

Target preservation:

- Food identity >=95%
- Ingredient geometry >=95%
- Vessel/container identity >=98%
- Plating topology >=95%
- Physical relationships >=95%

These are perceptual targets enforced by preserving the listed source invariants.

## Dish semantic identity

Use the following dish information as semantic direction for the environment, NOT as permission to alter the food:

```text
Dish name: {{DISH_NAME}}
Dish-name source: {{DISH_NAME_SOURCE}}
Confidence if inferred: {{DISH_CONFIDENCE}}
Cuisine: {{CUISINE_TYPE}}
Flavor profile: {{FLAVOR_PROFILE}}
Primary ingredients: {{PRIMARY_INGREDIENTS}}
Cooking method / temperature: {{COOKING_METHOD_AND_TEMPERATURE}}
Semantic route: {{SEMANTIC_ROUTE}}
Mood keywords: {{DISH_MOOD_KEYWORDS}}
```

If the dish name or cuisine was explicitly provided by the user, that information overrides automatic inference.

If dish identity was inferred with low confidence, use only conservative category-level semantic cues.

The dish semantic layer may affect only:

- background;
- surrounding environment;
- restrained supporting props;
- color direction;
- lighting character;
- photographic mood.

It must NOT cause ingredient invention, ingredient removal, re-plating, vessel replacement or product redesign.

## Subject edit policy

The food, its major ingredients, vessel/package and meaningful contact areas are low-edit regions.

Use **minimum necessary subject change**.

Do not reorganize, redesign, beautify, re-plate or luxury-upgrade the food.

Do not replace the vessel or package.

Do not invent ingredients.

Do not remove clearly visible major ingredients.

Do not enlarge ingredients or create more expensive-looking ingredients for visual impact.

Do not alter the hand-food, utensil-food, shelf-product, display-product or other meaningful physical relationship.

If the source is cropped or the requested aspect ratio requires expansion, reconstruct only the natural continuation of the same food, same vessel, same hand, same packaging, same support plane or contextually compatible environment.

**Continuation, not reinvention.**

## Food material treatment

{{PRIMARY_FOOD_MODULE}}

{{SECONDARY_FOOD_MODULES}}

Improve the visibility and photographic rendering of appetizing physical properties that already exist in the source. Do not manufacture unsupported wetness, juice, steam, smoke, gloss, char, garnish or luxury cues.

## Scene treatment

{{SCENE_MODULE}}

Environment changes may be substantially stronger than food changes when appropriate.

If the original environment has meaningful identity, enhance it instead of replacing it.

If the original environment has little contextual value and visually harms the subject, redesign or replace only the environment with a believable commercial setting appropriate to the exact food and source context.

Any new environment must match the subject's camera angle, perspective, scale, contact plane, depth and lighting direction. Maintain realistic contact shadows and environmental reflections. The subject must never appear pasted into the scene.

## Semantic background treatment

{{SEMANTIC_BACKGROUND_DIRECTION}}

Supporting props:

{{SEMANTIC_PROP_DIRECTION}}

Color direction:

{{SEMANTIC_COLOR_DIRECTION}}

Lighting character:

{{SEMANTIC_LIGHTING_CHARACTER}}

Do not default to dark wood + warm amber lighting + ceramic props simply because the subject is hot food.

The environment must feel specific to this dish. Ask internally: if the food were replaced by a semantically different dish such as sushi, strawberry cake or iced tea, would the same background still work unchanged? If yes, the background is too generic and must be redesigned.

Supporting props must remain few, subtle, softly defocused and clearly outside the food itself. Never allow semantic props to become new ingredients in the dish.

## Photography mode

{{PHOTOGRAPHY_MODE}}

Cinematic quality does not automatically mean dark, amber, smoky, teal-orange or highly dramatic. Choose the photographic language according to the actual food, cuisine, flavor profile and context.

## Lighting

Upgrade lighting aggressively while preserving product geometry.

Use professional commercial-photography principles appropriate to the subject:

- large controlled soft directional key light;
- subtle fill preserving shadow detail;
- restrained rim/back light only when materially useful;
- realistic practical environmental light;
- controlled specular reflections;
- realistic contact shadows;
- natural three-dimensional depth;
- clear but believable subject-background separation.

Any steam, smoke, condensation, liquid reflection or surface gloss must be physically justified.

Hot food may have restrained natural steam originating from the food. Cold food/cold drinks must not steam. Grilled food may use restrained smoke only if context supports it. Flying ingredients are disabled unless explicitly requested by the user.

## Composition and camera

Target aspect ratio: {{ASPECT_RATIO}}

Improve composition only as much as necessary for professional balance while protecting product identity and geometry.

Use a natural professional food-photography perspective. Avoid extreme wide-angle distortion, warped vessel edges or exaggerated product scale.

Use shallow-to-moderate depth of field. Keep identity-defining food structure readable.

## Color and material realism

Preserve accurate base food colors.

Apply sophisticated commercial color grading appropriate to the actual subject and semantic scene direction.

Semantic colors should support the food, not contaminate it. Do not recolor the actual ingredients merely to match a cuisine palette.

Avoid generic orange warmth, extreme teal-orange grading, oversaturation, extreme HDR, clipped highlights, crushed blacks and obvious filter effects.

Maintain realistic:

- food materials;
- liquid behavior;
- gravity;
- steam/smoke origin;
- condensation;
- hand/utensil contact;
- contact shadows;
- environmental reflections.

## Final quality target

The final image should feel like:

- photorealistic premium commercial food photography;
- elite studio craft;
- dish-specific cinematic or editorial art direction;
- professional advertising lighting;
- realistic material rendering;
- controlled highlights;
- deep but readable shadows;
- accurate texture;
- believable environmental depth;
- semantically relevant restaurant/retail/lifestyle atmosphere;
- high-end campaign photography;
- 4K visual quality.

The viewer must believe this is the **same individual serving or product from the uploaded source**, professionally re-photographed by an elite commercial photography studio in an environment that genuinely belongs to this specific dish.

The perceived quality increase must come from photography, lighting, composition, environment, depth, material rendering, color grading and semantic art direction — **not from changing the product itself**.

## Strict negatives

Strictly avoid:

- different food;
- changed food category;
- ingredient substitution;
- invented major ingredients;
- missing visible major ingredients;
- invented garnish;
- luxury ingredient invention;
- duplicated major ingredients;
- changed ingredient cuts;
- changed ingredient dimensions;
- changed ingredient geometry;
- changed ingredient quantity relationships;
- reorganized stacking/layering;
- redesigned plating;
- different bowl/plate/cup/tray/pot/container;
- different vessel material;
- different package or redesigned packaging;
- changed hand-food relationship;
- changed utensil-food relationship;
- incorrect retail/display context;
- floating ingredients or vessel;
- impossible liquids;
- incorrect contact shadows;
- inconsistent perspective;
- excessive or physically incorrect steam/smoke;
- semantic props entering the dish as new ingredients;
- cuisine-inappropriate generic background;
- repetitive dark-wood amber-light template;
- plastic/waxy food texture;
- fake wet gloss;
- CGI or 3D-render appearance;
- extreme HDR;
- excessive saturation;
- generic orange cast;
- unnecessary props;
- cheap e-commerce/menu photography;
- random text;
- invented packaging text;
- random logo;
- watermark;
- UI elements.

CORE COMMAND:

**PRESERVE WHAT THE FOOD IS.**

**PRESERVE HOW THE FOOD IS BUILT.**

**PRESERVE WHAT HOLDS THE FOOD.**

**PRESERVE HOW THE FOOD INTERACTS WITH THE REAL WORLD.**

**USE THE DISH SEMANTICS TO DESIGN THE ENVIRONMENT, NOT TO REDESIGN THE FOOD.**

**CHANGE THE PHOTOGRAPHY, NOT THE PRODUCT.**
