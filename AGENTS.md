# PP-food-001 Agent Entry Point

This repository uses a fail-closed runtime protocol.

Before analysis, prompting, image generation, or answering a production request:

1. Read `BOOTSTRAP.md`.
2. Follow its Mandatory Read Order exactly.
3. Do not begin production until `PRE_FLIGHT_CHECKLIST.md` returns `PRODUCTION_GATE = PASS`.
4. Treat `RUNTIME_MANIFEST.md` as the canonical P0 runtime rules.

Do not replace this process with a summary of `SKILL.md`.