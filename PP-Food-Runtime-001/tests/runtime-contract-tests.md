# PP-Food-Runtime-001 Runtime Contract Tests

These are release-gate tests for cross-agent production behavior. They are not normal runtime context.

## T01 — Explicit A is A only
PASS: `执行A` routes to Stage A only. No KV copy gate, no Stage B.
FAIL: business info or previous state silently upgrades A to B.

## T02 — Explicit B must traverse current A
PASS: current user image → current Stage A → QC PASS → current Stage A PASS image → Stage B.
FAIL: Stage B uses raw snapshot, previous-job image, or an unverified Stage A output.

## T03 — Current-job isolation
PASS: every new image resets product, brand, copy, category skin, address, phone, price, slogan and visual skin unless user explicitly continues them.
FAIL: any previous-job entity or skin leaks into the new contract.

## T04 — Runtime minimalism
PASS: normal production loads Runtime Core + selected executor + current category profile only.
FAIL: tests, all references, all category profiles, historical examples or full repository are sent into production context.

## T05 — Image model prompt compiler is fixed
PASS: A and B prompts follow the exact compiler block order defined by PROMPT_COMPILER.md.
FAIL: host agent invents extra prompt sections, dumps repository text, or rewrites the execution protocol ad hoc.

## T06 — Vision/image role separation
PASS: VISION_MODEL reads user image and generated outputs; IMAGE_MODEL performs reference-image generation/editing.
FAIL: non-visual host guesses image content or IMAGE_MODEL alone is treated as the full reasoning/QC stack.

## T07 — B copy gate
PASS: without `DEFAULT_COPY_AUTHORIZED`, Stage B requires headline + subtitle + at least one auxiliary field and asks only for the minimum missing copy.
FAIL: missing subtitle or auxiliary information is silently invented.

## T08 — Default copy authorization
PASS: phrases such as `按默认文案来` authorize only safe non-factual campaign copy.
FAIL: system invents phone, address, price, certification, awards, history, origin, unverified ingredient, process or health claim.

## T09 — Product Hero
PASS: product remains visual priority #1; headline is #2.
FAIL: headline, typography architecture or background becomes the first visual hero.

## T10 — Category isolation
PASS: one primary category profile + optional one weak auxiliary profile is active.
FAIL: all category skins are simultaneously active or previous category skin is reused by default.

## T11 — Targeted retry only
PASS: failures map to a specific retry type; unchanged successful dimensions remain locked.
FAIL: whole image is randomly regenerated after a localized failure.

## T12 — Fail closed
PASS: missing visual ability, reference editing, credential, current image, current Stage A PASS for B, unresolved category, incomplete contract or unresolved conflict blocks production.
FAIL: agent generates anyway.

## T13 — Prompt payload boundary
PASS: IMAGE_MODEL receives only current reference image + compact current contract + compact current prompt.
FAIL: it receives full repository Markdown, test cases, unused category profiles or previous-job data.

## T14 — Setup state machine
PASS: SETUP_GATE → READY_WAITING_FOR_START → user says `启动` → PRODUCTION.
FAIL: the system starts image production before setup is complete or keeps re-asking configuration every job after startup.

## T15 — Fidelity over design aggression
PASS: when visual ambition conflicts with product truth, design aggression is reduced.
FAIL: food/packaging/vessel/plating is redesigned to achieve a prettier poster.

## Release Gate
V1.0.0 must not ship unless all T01–T15 are represented by explicit runtime rules and executor behavior.
