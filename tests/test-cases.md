# Universal Food Fidelity + Semantic Background Baseline Tests

Use a diverse fixed test set. The purpose is to detect product drift **and** generic-background drift, not merely judge beauty.

For every case record:

- source photo;
- explicit dish information from the user, if any;
- inferred dish semantics and confidence, if required;
- selected food module(s);
- selected scene module;
- semantic route;
- photography mode;
- fidelity score;
- photography score;
- semantic score;
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
- case lighting/glass reflections improve;
- background should feel like bakery/dessert retail, not a dark hot-food restaurant.

FAIL:

- extra berries/chocolate/gold leaf;
- cake layers redesigned;
- display context removed;
- dark wood + amber hot-food template.

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
- practical night light and restrained smoke may improve atmosphere;
- semantic environment should remain street-food/night-market.

FAIL:

- more skewers added;
- meat chunks enlarged;
- heavy fake smoke obscures product;
- converted to luxury fine dining.

## Test 07 — Sashimi / sliced fish platter

Expected:

- visible slice count relationship, thickness and arrangement remain;
- moisture/material/restaurant lighting improve;
- environment should be clean, restrained and Japanese/minimal if context supports it.

FAIL:

- lobster/caviar/gold leaf added;
- slices become thicker/more numerous;
- new luxury plate used;
- generic spicy-food dark amber background.

## Test 08 — Fruit salad / fresh salad

Expected:

- fresh, clean, natural commercial treatment;
- fruit/vegetable identity and cuts remain;
- no steam;
- natural/editorial semantic environment.

FAIL:

- dramatic dark hot-food treatment;
- ingredients substituted;
- artificial wet gloss.

## Test 09 — Ice cream

Expected:

- scoop count, colors/flavors, cup/cone and arrangement remain;
- texture/cold feel improve;
- soft dessert/lifestyle environment.

FAIL:

- flavors/colors change;
- fruit garnish added;
- scoop count changes;
- steam or hot-food visual language.

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
- subtle steam only if hot and supported;
- NATURAL_EDITORIAL or restrained CINEMATIC_EDITORIAL.

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
- texture and bakery lighting improve;
- bakery/café semantics remain appropriate.

FAIL:

- pastry decoration added;
- tray replaced;
- flaky structure exaggerated into a different pastry.

# V5 Semantic Background Tests

## Test 16 — 用户明确：青花椒酸菜鱼

Source characteristics:

- fish slices;
- green chili rings;
- green Sichuan pepper / fresh pepper cluster;
- pale yellow hot broth;
- red serving vessel.

User explicitly says:

`dish_name = 青花椒酸菜鱼`

Expected semantic route:

`SICHUAN_FRESH_PEPPER`

Expected:

- fish slices, green pepper, pepper cluster, broth and red vessel remain highly faithful;
- background communicates fresh-pepper Sichuan character through restrained green/yellow-green accents, refined Sichuan restaurant context and controlled warm heat atmosphere;
- dark gray stone or restrained Chinese dining surface may be used;
- subtle pepper/pickle semantic props may exist only in distant background;
- food remains the hero.

FAIL:

- becomes red-oil Sichuan fish;
- new pickled vegetables or pepper are added to the dish;
- vessel replaced;
- generic black-and-gold Western restaurant;
- identical dark-wood amber background used for unrelated noodle/soup tests.

## Test 17 — 用户明确：粤式清蒸鱼

Expected:

- bright, clean, restrained Chinese dining environment;
- natural/editorial light;
- no heavy smoke or dark red spicy atmosphere.

FAIL:

- hotpot-style background;
- aggressive rim light and smoke;
- red spicy visual language.

## Test 18 — 用户明确：草莓奶油蛋糕

Expected:

- same strawberry count/placement and cake geometry;
- soft dessert/café semantic environment;
- milk-white, strawberry-red and neutral supporting palette.

FAIL:

- dark Sichuan restaurant treatment;
- extra strawberries, gold leaf or chocolate added.

## Test 19 — 用户未提供菜名，识别置信度中等

Example: visually ambiguous fish soup.

Expected:

- use category-level `hot fish soup / Chinese fish dish` semantic environment;
- avoid overly specific regional props;
- preserve food exactly.

FAIL:

- assert a specific cuisine and aggressively decorate the environment from an uncertain guess;
- add ingredients consistent with the guess.

## Test 20 — 同场景不同菜品反模板测试

Use four tabletop images:

1. 青花椒酸菜鱼
2. 牛肉面
3. 寿司
4. 草莓蛋糕

PASS:

- all four maintain comparable commercial photography quality;
- all four preserve their source food;
- backgrounds differ meaningfully in color, lighting character, materials and semantic context.

FAIL:

- all four become dark wood + amber practical lights + ceramic jar + bokeh.

## Acceptance matrix

| Product fidelity | Photography upgrade | Semantic relevance | Result |
|---|---|---|---|
| High | High | High | **V5 Target** |
| High | High | Low | Failure: generic/template background |
| High | Low | High | Incomplete: weak photography upgrade |
| Low | High | High | Failure: AI reinterpretation |
| Low | Low | Low | Failure |

Final V5 pass requires:

- **Fidelity >=95**
- **Photography >=85**
- **Semantic >=85**
- no Fidelity Critical Failure
- no Semantic Critical Failure
