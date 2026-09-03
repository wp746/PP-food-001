# Installation / Host Integration

## Preferred
Install this Skill directory as the single production runtime.

Do not install the two research Skills as active production controllers at the same time unless the host explicitly supports dependency resolution without merging their prompts. If both research repositories are present for reference, this Runtime Pack remains the production authority.

## Host Setup
1. Configure a visual model.
2. Configure a reference-image capable image model.
3. Configure connection/base URL and credential in the host's secret/connection system.
4. Ensure generated images can be read by the visual model.
5. Ensure Stage A PASS can be passed as Stage B reference.
6. Load `SKILL.md` and follow the Runtime Minimal Core.
7. When READY, wait for `启动`.

## Production Commands
```text
执行A
执行B
```

## Important
The host should not merge full contents of PP-food-001 and PP-food-KV-001 into runtime context. They are research/source repositories. This Runtime Pack contains the production contract needed for stable execution.
