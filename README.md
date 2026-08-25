# PP-food-001

Reusable agent skill for transforming a user-provided food photo into premium commercial / cinematic food photography while preserving the original food and product identity at very high perceptual fidelity.

## Core principle

**Preserve the product. Upgrade the photography.**

The source food is not raw material for creative reinterpretation. Treat it as the real physical product on a commercial set: camera, light, background and environment may change; the product itself does not.

## Intended use

Use this skill when:

- the food subject is clearly identifiable;
- the user wants a premium studio/commercial result;
- the original ingredients, geometry, plating, vessel, packaging, hand/product relationship or retail context must remain highly faithful;
- the image may be tabletop, handheld, on a shelf, in a display case, at a stall, in a café/restaurant, or another realistic food context.

The skill is model-neutral and is suitable for source-image editing workflows, including GPT Image 2.

## Target thresholds

These are perceptual acceptance targets enforced by invariants and QC, not literal pixel-similarity guarantees:

- Food identity fidelity: **>=95%**
- Ingredient geometry fidelity: **>=95%**
- Vessel/container identity fidelity: **>=98%**
- Plating fidelity: **>=95%**
- Physical-relationship fidelity: **>=95%**
- Photography quality score: **>=85/100**

## Repository structure

```text
PP-food-001/
├── README.md
├── SKILL.md
├── VERSION
├── references/
│   ├── execution-template.md
│   ├── fidelity-manifest.md
│   ├── fidelity-qc.md
│   ├── food-modules.md
│   ├── retry-policy.md
│   └── scene-modules.md
└── tests/
    └── test-cases.md
```

## Runtime pattern

1. Read `SKILL.md`.
2. Build the source-truth/fidelity manifest.
3. Load only the relevant food module(s).
4. Load one primary scene module.
5. Select an appropriate photography mode.
6. Assemble the final edit instruction using `references/execution-template.md`.
7. Generate/edit the image.
8. Run `references/fidelity-qc.md`.
9. If necessary, apply a targeted retry from `references/retry-policy.md`.

Do not load every module into every request. Constraint overload reduces stability.
