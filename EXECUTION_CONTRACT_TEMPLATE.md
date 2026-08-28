# PP-food-001 Execution Contract Template

每个新任务在调用 IMAGE_MODEL 前，先在内部编译一份当前任务合同。用户不需要填写 JSON，也不需要看到内部字段。

## Contract

```text
JOB_MODE = A | B_UPSTREAM_STAGE_A
ASPECT_RATIO = 9:16

CURRENT_JOB_FACTS =
- user_visible_facts:
- user_explicit_facts:
- legacy_facts_allowed: NO, unless user explicitly requests continuation

SOURCE_PRODUCT =
- food/product identity:
- temperature/cooking state:
- serving mode:

VISIBLE_FACTS =
- major ingredients:
- ingredient geometry / cuts / widths / thickness / orientation:
- visible count / arrangement relationships:
- vessel / packaging identity:
- plating topology:
- sauce / oil / broth / cream / ice state:
- physical contacts / supports:

REGION_BUDGET =
- Region A Subject Core: VERY_LOW
- Region B Subject Support: LOW_TO_MEDIUM
- Region C Environment: HIGH

LOCK_TARGETS =
- Food Identity >=95
- Ingredient Geometry >=95
- Vessel / Container >=98
- Plating >=95
- Physical Relationship >=95

CATEGORY_SEMANTICS =
- food_category:
- cuisine_family if supported:
- temperature logic:
- semantic confidence:
- selected material-stage direction:

CREATIVE_SCOPE =
- canvas extension / 9:16 composition
- professional lighting
- depth / subject separation
- category-semantic material stage
- background
- color grading
- realistic appetite rendering

FORBIDDEN =
- add/remove/replace major ingredients
- change identity-defining geometry
- replace vessel/package
- redesign package text/logo
- re-plate product
- change physical relationships
- invent unsupported heat/steam/gloss
- adapt 9:16 by distorting or rebuilding product
- import previous-job food facts

STAGE_A_QC_REQUIRED = TRUE
TARGETED_RETRY_ONLY = TRUE
```

## IMAGE_MODEL Compilation Rule

最终图像编辑指令必须从本合同编译，且第一段先写 Subject Lock，再写摄影/环境升级。

不得直接把整仓库 Markdown 原样拼进 IMAGE_MODEL Prompt；仓库负责约束与路由，Contract 负责把当前任务编译成短、明确、可执行的指令。

## B Handoff Fields

如果 `JOB_MODE = B_UPSTREAM_STAGE_A`，Stage A PASS 后追加：

```text
STAGE_A_PASS_IMAGE = <current job output reference>
STAGE_A_QC = PASS
HANDOFF_TO_STAGE_B = ALLOWED
```

若 Stage A 未 PASS：

```text
HANDOFF_TO_STAGE_B = BLOCKED
```

先定向重试 Stage A。