# Current Job Isolation

Every new user image starts a clean production state.

## Reset on New Image

Create:
```text
CURRENT_JOB_ID = new
CURRENT_JOB_FACTS = empty then rebuilt from current image + current user message
CURRENT_STAGE_A_IMAGE = null
CURRENT_STAGE_B_IMAGE = null
CURRENT_CATEGORY_PROFILE = null
CURRENT_COPY_ALLOWLIST = empty
CURRENT_COPY_BLOCKLIST = previous-job entities + unsupported facts
CURRENT_PROMPT_CACHE = empty
```

Invalidate by default:
- previous product/dish identity;
- previous brand/store;
- previous address/phone/price;
- previous slogan/selling points;
- previous category profile;
- previous typography/material/background skin;
- previous Stage A/B images;
- previous prompt fragments.

## Explicit Continuation Exception
Only retain a field when the user explicitly says this is the same product/campaign and asks to continue it.

## Contamination Gate
If a current contract contains any previous-job entity or visual skin without explicit continuation:
```text
JOB_CONTAMINATION = TRUE
PRODUCTION_GATE = BLOCKED
```
Rebuild the contract from current-job truth.
