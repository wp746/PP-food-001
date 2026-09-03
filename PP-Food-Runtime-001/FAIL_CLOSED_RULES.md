# Fail-Closed Rules

Production must stop rather than improvise when a required invariant is missing.

## Block Production When

- current user image is missing for A/B;
- VISION_MODEL cannot read current image;
- IMAGE_MODEL cannot accept a real reference image;
- generated output cannot be read back for QC;
- credential/connection is unavailable;
- B is requested but current Stage A PASS image is missing;
- B copy gate is incomplete and default copy is not authorized;
- current category route is unresolved beyond a conservative fallback;
- compact current-job contract is incomplete;
- previous-job contamination is detected;
- P0 rules conflict;
- retry limit is exhausted without passing hard gates.

## Required Behavior

```text
PRODUCTION_GATE = BLOCKED
```

Then ask only for the smallest missing user/runtime input, or report the specific technical failure. Do not generate a speculative fallback image and call it production.
