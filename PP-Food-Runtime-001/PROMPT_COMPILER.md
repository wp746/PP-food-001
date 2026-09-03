# Fixed Prompt Compiler

The host agent may populate current-job values. It may not change block order, add repository dumps, or append unrelated examples.

## A Compiler — Exactly 6 Blocks

```text
A1 REFERENCE LOCK
- current user image is product truth
- lock identity, key geometry, vessel/package, arrangement, physical relationships, visible surface/material state

A2 CURRENT PRODUCT DNA
- only current visible facts + current explicit user facts
- list the smallest set of identity-critical locks

A3 SURFACE / SUPPORT LOCK
- preserve browning/doneness/gloss/moisture/sauce/crust/condensation/packaging state
- preserve direct support and topology

A4 COMMERCIAL HERO UPGRADE
- strict 9:16 hero composition
- lighting, depth, material readability, separation, professional camera language

A5 CURRENT CATEGORY BACKGROUND
- one product-derived Big Idea
- 2–3 dominant material planes/masses
- near/mid/deep depth and category-native atmosphere

A6 HARD NEGATIVES
- no product redesign
- no ingredient/product add/remove/replace
- no vessel/package redesign
- no surface-state mutation
- no unsupported steam/condensation/garnish
- no previous-job skin
- no generic prop-pack premium look
```

A prompt should be concise. If a rule is not current-job relevant, do not include it.

## B Compiler — Exactly 6 Blocks

```text
B1 STAGE A PRODUCT LOCK
- reference = current Stage A PASS image
- preserve product/packaging/vessel/plating/physical truth

B2 CURRENT CATEGORY PROFILE
- activate one primary profile + optional weak auxiliary profile
- include only current typography/material/layout traits

B3 COPY TRUTH
- exact headline/subtitle/brand/store/business info from allowlist
- generated soft copy only when authorized
- hard-fact blocklist remains active

B4 PRODUCT HERO + SPATIAL TEXT
- product visual priority #1
- headline priority #2
- headline/subtitle/slogan form one category-native spatial text system
- controlled occlusion only

B5 ONE BIG IDEA + CAMPAIGN WORLD
- one thumbnail-readable concept
- category-native background, materials, perspective, information density and campaign finish

B6 HARD NEGATIVES
- no raw snapshot reference after Stage A PASS
- no previous-job image/facts/skin
- no product redesign
- no unsupported facts
- no headline dominance
- no cross-category skin
- no flat generic PPT text stack
```

## Payload Rule

IMAGE_MODEL receives only:
```text
reference image
+ compact contract
+ compiled 6-block prompt
```

Do not send tests, README, runtime setup text, unused profiles, historical examples, or full repository content.
