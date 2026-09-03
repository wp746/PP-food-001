# Model Configuration Contract

PP-Food-Runtime-001 separates interpretation from image generation.

## Required Roles

### VISION_MODEL
Must be able to:
- read current user image;
- extract current-job visible facts;
- identify category/temperature/packaging/serving mode;
- read Stage A and Stage B generated outputs;
- perform fidelity, category, typography and product-dominance QC.

### IMAGE_MODEL
Must be able to:
- receive the actual current reference image;
- perform reference-image editing / image-to-image generation;
- preserve product identity while changing lighting/background/commercial finish;
- accept Stage A PASS image as Stage B reference.

## Host Agent
The host agent orchestrates tools, fills compact contracts and handles user dialogue. It must not substitute its own visual guesses when VISION_MODEL is required.

## Configuration Data
Runtime secrets and provider routes live in host Secret / Environment / Connection state, not in this repository.
