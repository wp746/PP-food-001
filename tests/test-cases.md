# Universal Food Fidelity Baseline Tests

Use a diverse fixed test set. The purpose is to detect product drift, not merely judge beauty.

For every case record:

- source photo;
- selected food module(s);
- selected scene module;
- photography mode;
- fidelity score;
- photography score;
- Critical Failures;
- retry type if needed.

## Test 01 — Hot noodle soup, white ceramic bowl, ordinary table

Expected:

- noodles, toppings, broth and white bowl remain substantially unchanged;
- background/light improve strongly;
- subtle realistic steam allowed.

FAIL examples:

- bowl replaced;
- noodle width changes;
- extra meat added;
- toppings reorganized.

## Test 02 — Handheld burger, street background

Expected:

- exact layer structure and hand grip remain;
- street/lifestyle background may become cleaner and more cinematic.

FAIL:

- converted to tabletop;
- bacon/egg/second patty invented;
- burger stack rebuilt.

## Test 03 — Handheld milk tea / iced drink in plastic cup

Expected:

- same plastic cup, straw, liquid color, inclusions and grip;
- condensation/material clarity may improve.

FAIL:

- plastic cup -> glass;
- different straw;
- new fruit/foam toppings;
- steam added.

## Test 04 — Strawberry cream cake in display case

Expected:

- cake geometry, layer count and strawberry count/placement remain;
- case lighting/glass reflections improve.

FAIL:

- extra berries/chocolate/gold leaf;
- cake layers redesigned;
- display context removed.

## Test 05 — Packaged chips on supermarket shelf

Expected:

- same package identity and retail context;
- improved local lighting, shelf organization and separation.

FAIL:

- package redesigned;
- random logo/text invented;
- product moved to wood tabletop.

## Test 06 — Night-market skewers / BBQ

Expected:

- skewer count relationship, meat geometry and sequence remain;
- practical night light and restrained smoke may improve atmosphere.

FAIL:

- more skewers added;
- meat chunks enlarged;
- heavy fake smoke obscures product.

## Test 07 — Sashimi / sliced fish platter

Expected:

- visible slice count relationship, thickness and arrangement remain;
- moisture/material/restaurant lighting improve.

FAIL:

- lobster/caviar/gold leaf added;
- slices become thicker/more numerous;
- new luxury plate used.

## Test 08 — Fruit salad / fresh salad

Expected:

- fresh, clean, natural commercial treatment;
- fruit/vegetable identity and cuts remain;
- no steam.

FAIL:

- dramatic dark hot-food treatment;
- ingredients substituted;
- artificial wet gloss.

## Test 09 — Ice cream

Expected:

- scoop count, colors/flavors, cup/cone and arrangement remain;
- texture/cold feel improve.

FAIL:

- flavors/colors change;
- fruit garnish added;
- scoop count changes.

## Test 10 — Cropped bowl/plate

Expected:

- missing edge reconstructed as natural continuation of the same vessel;
- food structure not redesigned.

FAIL:

- a new bowl/plate appears;
- new ingredients are invented in outpainted area.

## Test 11 — Fried chicken / fried snack

Expected:

- piece geometry/count relationship and coating remain;
- crisp texture/readability improve.

FAIL:

- larger/more regular pieces;
- greasy plastic highlights;
- extreme orange saturation.

## Test 12 — Coffee in café

Expected:

- same cup, liquid level and visible foam/crema;
- café context may become more refined;
- subtle steam only if hot and supported.

FAIL:

- cup replaced;
- latte art invented when absent;
- dramatic dark restaurant background replacing meaningful café context.

## Test 13 — Takeaway food in paper box

Expected:

- box identity, food-box relationship and visible food layout remain;
- lighting/background may improve.

FAIL:

- moved to ceramic plate;
- food re-plated;
- box material changed.

## Test 14 — Food held by chopsticks/fork

Expected:

- same lifted food and utensil contact relationship;
- main plate/bowl remains coherent;
- background/light improve.

FAIL:

- different food is lifted;
- contact geometry impossible;
- utensil shape malformed.

## Test 15 — Bakery item on tray

Expected:

- pastry shape/layers and tray identity remain;
- texture and bakery lighting improve.

FAIL:

- pastry decoration added;
- tray replaced;
- flaky structure exaggerated into a different pastry.

## Acceptance matrix

| Product fidelity | Photography upgrade | Result |
|---|---|---|
| High | High | Target |
| High | Low | Incomplete: ordinary retouch |
| Low | High | Failure: AI reinterpretation |
| Low | Low | Failure |

Only **High Fidelity × High Photography Upgrade** is the intended endpoint.
