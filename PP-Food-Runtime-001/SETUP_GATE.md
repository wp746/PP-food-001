# Setup Gate

The runtime must not enter production until the host can prove the following declared capabilities.

## Required Configuration

```text
VISION_MODEL
IMAGE_MODEL
API_BASE_URL or equivalent connection route
CREDENTIAL_PRESENT = TRUE
REFERENCE_IMAGE_EDIT = TRUE
VISION_CAN_READ_USER_IMAGE = TRUE
VISION_CAN_READ_GENERATED_OUTPUT = TRUE
STAGE_A_OUTPUT_CAN_FEED_STAGE_B = TRUE
```

Do not ask for values already available in the host environment.
Do not echo full secrets in normal chat.

## Evidence Levels

```text
DECLARED = capability is configured / exposed by host
VERIFIED = capability succeeded in a real current runtime chain or matching verified private profile
```

A configured host may enter READY with `VERIFIED = PENDING`; the first real task becomes verification. Do not generate a separate wasteful smoke-test image.

## Block Conditions

Any of the following blocks production:
- non-visual host with no callable VISION_MODEL;
- IMAGE_MODEL cannot receive a real reference image;
- credential/connection missing;
- generated output cannot be read back for QC;
- B requested but Stage A output cannot be passed to Stage B.

Only ask the user for the missing configuration item(s).
