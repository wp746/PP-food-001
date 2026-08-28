# PP-food-001 Execution Contract Template

每个新任务在调用 IMAGE_MODEL 前，先在内部编译一份当前任务合同。用户不需要填写 JSON，也不需要看到内部字段。

## Contract

```text
JOB_MODE = A | B_UPSTREAM_STAGE_A
ASPECT_RATIO = 9:16
OUTPUT_ASPECT_RATIO_EXACT = 9:16
NON_9_16_DELIVERY = CRITICAL_FAILURE

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

SURFACE_STATE_LOCK =
- base color / gradient:
- browning level:
- char level:
- cooking doneness:
- gloss / matte level:
- moisture level:
- sauce / oil coverage:
- crust / skin state:
- crack / scoring state:
- cream / frosting / powder state if applicable:
- condensation / frost / translucency if applicable:
- rule: REVEAL_EXISTING_PROPERTY_ONLY

TOPOLOGY_COMPLETION_PLAN =
- applicable: YES / NO
- completion confidence: HIGH / MEDIUM / LOW
- cropped / incomplete target:
- identity to continue:
- geometry / cut / scale to continue:
- orientation / layer / overlap to continue:
- density / count relationship to continue:
- source surface state to continue:
- direct support / container continuation:
- unsupported content forbidden:
- LOW confidence => ENVIRONMENT_EXTENSION_ONLY

REGION_BUDGET =
- Region A Subject Core + Surface State: VERY_LOW
- Region B Direct Support: LOW
- Region C Generic Environment: HIGH

LOCK_TARGETS =
- Food Identity >=95
- Ingredient Geometry >=95
- Vessel / Container >=98
- Plating / Arrangement >=95
- Physical Relationship >=95
- Source Surface / Material State = LOCKED

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

BACKGROUND_ARCHITECTURE_PLAN =
- category_material_logic:
- food-derived_color_logic:
- primary_material_planes: 2-3
- L1_near_spatial_mass:
- L3_mid_spatial_mass:
- L4_deep_spatial_masses: >=2 depth cues
- height_variation:
- depth_variation:
- occlusion_relationship:
- light_cut_and_shadow_architecture:
- reflective_vs_absorptive_material_relationship:
- negative_space_zone:
- props_required?: YES / NO
- if props: subordinate role only

HERO_REFRAME_PLAN =
- source camera is accidental snapshot?: YES / NO
- strict portrait canvas = 9:16
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
- strict 9:16 portrait canvas extension / composition
- topology-preserving completion when evidence supports it
- controlled Hero Reframe
- professional lighting
- four-layer depth / subject separation
- category-native background architecture
- background translation
- color grading around source-true food color
- realistic appetite readability, not appetite mutation

FORBIDDEN =
- deliver any non-9:16 Stage A final image
- add/remove/replace major ingredients
- change identity-defining geometry
- change browning / char / doneness / gloss / moisture / sauce coverage / crust state beyond source
- exaggerate cracks / scoring / burst openings
- replace vessel/package/direct support without permission
- redesign package text/logo
- re-plate/re-stack/move product units
- use completion as permission to beautify or invent food
- change count / overlap order
- change meaningful physical relationships
- invent unsupported heat/steam/gloss/condensation/garnish
- adapt 9:16 by distorting or rebuilding product
- preserve a generic venue merely because it exists in source
- create a premium look primarily from linen / tongs / cups / pottery / wheat / spice bowls / bokeh props
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
1. Exact 9:16 Output Contract
2. Subject / Direct-Support Lock
3. Surface / Material State Lock
4. Topology Completion Plan
5. Scene Context Split
6. Category Route
7. Background Architecture Plan
8. Hero Reframe Plan
9. Multi-Product Hero Plan
10. Four-Layer Hero Stage
11. Appetite / Lighting / Color
12. Strict Negatives
```

不得直接把整仓库 Markdown 原样拼进 IMAGE_MODEL Prompt。

`source camera coordinates` 不属于默认锁定项；锁定的是产品视图几何、排列、直接承载和可信透视。

`generic venue context` 不属于默认锁定项；除非 identity-critical，否则转译为品类原生高级材质舞台。

`background architecture` 必须先于 props 设计；删除 props 后背景仍必须成立。

`appetite rendering` 不得提高源产品属性强度；只允许让源图已有属性在更好的摄影下更易读。

`topology completion` 只允许延续同一份产品，不提供重新摆盘或重新烹饪权限。

若第一次 IMAGE_MODEL 返回非 9:16，不得交付，必须针对画布比例进行修正后重新 QC。

## B Handoff Fields

如果 `JOB_MODE = B_UPSTREAM_STAGE_A`，Stage A PASS 后追加：

```text
STAGE_A_PASS_IMAGE = <current job output reference>
STAGE_A_QC = PASS
STAGE_A_ASPECT_RATIO = 9:16
HANDOFF_TO_STAGE_B = ALLOWED
```

若 Stage A 未 PASS：

```text
HANDOFF_TO_STAGE_B = BLOCKED
```

先定向重试 Stage A。