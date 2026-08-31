# PP-food-001 Compact Execution Contract

每个 A 任务在调用 IMAGE_MODEL 前，只编译**当前任务专属、短而无冲突**的合同。不要把整个仓库翻译进合同。

## Contract

```text
JOB_MODE = A | B_UPSTREAM_STAGE_A
SOURCE_REFERENCE = CURRENT_USER_IMAGE
OUTPUT = EXACT 9:16

1) PRODUCT_LOCK
- identity:
- major ingredients/materials:
- geometry / count / arrangement:
- vessel / package / direct support:
- plating topology / physical relationships:
- source surface state:

2) COMPLETION
- cropped/incomplete?: YES / NO
- confidence: HIGH / MEDIUM / LOW / NA
- allowed continuation:
- forbidden invention:

3) CURRENT_ROUTE
- food_category:
- dish/product semantics:
- temperature logic:
- scene/direct-support split:
- selected Stage A route:

4) HERO_STAGE
- PRIMARY_HERO:
- controlled reframe:
- product-derived evidence: >=3
- BACKGROUND_BIG_IDEA:
- primary materials: 2–3
- near / mid / deep architecture:
- light-cut / shadow / reflect-vs-absorb logic:
- negative space:

5) HARD_NEGATIVES
- no product redesign
- no ingredient add/remove/replace
- no vessel/package redesign
- no re-plating / re-stacking
- no surface-state amplification
- no unsupported steam/condensation/garnish
- no previous-job facts/skin
- no generic prop-pack premium styling
- no non-9:16 delivery

6) QC_TARGETS
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container >=98
Plating / Arrangement >=95
Physical Relationship >=95
Photography >=85
Semantic >=85
Hero Spatial >=85
Appetite >=85
```

## Compilation Rule

IMAGE_MODEL Prompt 固定只编译为 6 个短块：

```text
A. Reference Lock — 必须第一段
B. Current Product DNA
C. Allowed Completion / Hero Reframe
D. Current Category + Background Big Idea
E. Lighting / Materials / 9:16 Hero Composition
F. Hard Negatives
```

禁止加入：
- tests 原文；
- 旧任务信息；
- 全部品类示例；
- 仓库结构说明；
- Runtime Profile 说明；
- 重复三遍以上的同义约束。

## Reference Lock Canonical Opening

Prompt 第一段必须表达同等强度含义：

> 以当前用户上传参考图为唯一产品真相。严格锁定原始食物/产品身份、主要食材或材质、几何与数量关系、器皿/包装、摆盘/阵列拓扑、源表面状态和直接物理关系。不得为了更高级、更饱满或更有食欲而重做、替换、增减、重排或重新烹饪主体。创意主要发生在灯光、背景、环境、景深、Hero 构图和商业摄影品质层。

## Anti-Drift Rule

如果当前合同里出现上一任务品牌/产品/地址/口味/视觉皮肤，且用户未明确要求沿用：

```text
CONTRACT_CONTAMINATION = TRUE
PRODUCTION_GATE = BLOCKED
```

## B Handoff

若 `JOB_MODE = B_UPSTREAM_STAGE_A`：

```text
STAGE_A_QC = PASS
STAGE_A_PASS_IMAGE = CURRENT_JOB_OUTPUT
HANDOFF_TO_STAGE_B = ALLOWED
```

否则 Stage B BLOCKED。
