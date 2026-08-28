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
- direct support identity:
- venue context identity-critical?: YES / NO

VISIBLE_FACTS =
- major ingredients/materials:
- ingredient/product geometry / cuts / widths / thickness / orientation:
- visible count / arrangement relationships:
- vessel / packaging / tray identity:
- plating / product-field topology:
- sauce / oil / broth / cream / ice / crust state:
- physical contacts / supports:

REGION_BUDGET =
- Region A Subject Core: VERY_LOW
- Region B Direct Support: LOW
- Region C Generic Environment: HIGH

LOCK_TARGETS =
- Food Identity >=95
- Ingredient Geometry >=95
- Vessel / Container >=98
- Plating / Arrangement >=95
- Physical Relationship >=95

CATEGORY_SEMANTICS =
- food_category:
- cuisine_family if supported:
- temperature logic:
- semantic confidence:
- selected material-stage direction:
- selected Stage A category route:

SCENE_CONTEXT_SPLIT =
- DIRECT_SUPPORT_TO_LOCK:
- GENERIC_VENUE_CONTEXT_TO_TRANSLATE:
- IDENTITY_CRITICAL_CONTEXT_TO_PRESERVE:

HERO_REFRAME_PLAN =
- source camera is accidental snapshot?: YES / NO
- crop / canvas extension:
- focal-length feel:
- allowed camera-height / pitch adjustment:
- visible-face proportions to preserve:
- support-plane / overlap / foreshortening constraints:

MULTI_PRODUCT_HERO_PLAN =
- applicable: YES / NO
- PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER:
- SUPPORTING_PRODUCT_FIELD:
- hierarchy by light / sharpness / rim / contrast / DOF only:
- no move / remove / duplicate / re-stack: TRUE

HERO_STAGE_PLAN =
- L1 near-camera entry:
- L2 Hero + light pool:
- L3 category-native material depth:
- L4 deep recession with >=2 perceptible depth cues:
- negative space:
- rim / subject-background separation:

CREATIVE_SCOPE =
- canvas extension / 9:16 composition
- controlled Hero Reframe
- professional lighting
- four-layer depth / subject separation
- category-semantic material stage
- background translation
- color grading
- realistic appetite rendering

FORBIDDEN =
- add/remove/replace major ingredients
- change identity-defining geometry
- replace vessel/package/direct support without permission
- redesign package text/logo
- re-plate/re-stack/move product units
- change count / overlap order
- change meaningful physical relationships
- invent unsupported heat/steam/gloss
- adapt 9:16 by distorting or rebuilding product
- preserve a generic venue merely because it exists in the source
- treat exact source camera coordinates as Food DNA
- create extreme unsupported low-angle / wide-angle views
- give every product unit equal visual weight when multi-product Hero hierarchy is possible
- import previous-job food facts or visual skin

STAGE_A_QC_REQUIRED = TRUE
TARGETED_RETRY_ONLY = TRUE
```

## IMAGE_MODEL Compilation Rule

最终图像编辑指令必须从本合同编译，顺序固定：

```text
1. Subject / Direct-Support Lock
2. Scene Context Split
3. Category Route
4. Hero Reframe Plan
5. Multi-Product Hero Plan
6. Four-Layer Hero Stage
7. Appetite / Lighting / Color
8. Strict Negatives
```

不得直接把整仓库 Markdown 原样拼进 IMAGE_MODEL Prompt。

`source camera coordinates` 不属于默认锁定项；锁定的是产品视图几何、排列、直接承载和可信透视。

`generic venue context` 不属于默认锁定项；除非 identity-critical，否则转译为品类原生高级材质舞台。

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