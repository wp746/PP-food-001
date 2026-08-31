# PP-food-001 Pre-Flight Checklist

目标：只拦真正会导致漂移/失败的问题，不把生产门禁本身变成上下文负担。

## 1. Bootstrap Status

必须：

```text
VERSION_READ = PASS
RUNTIME_MANIFEST_READ = PASS
SKILL_READ = PASS
SOP_A_READ = PASS
HANDOFF_READ = PASS
REQUIRED_READ_SET_READ = PASS
EXECUTION_CONTRACT_TEMPLATE_READ = PASS
```

`tests/*` 不属于正常生产 pre-flight。

## 2. Runtime Capability Gate

必须静态确认：

```text
VISION_MODEL_CAN_READ_IMAGE = PASS
IMAGE_MODEL_REFERENCE_EDIT = PASS
CREDENTIAL = PASS
USER_IMAGE_TO_IMAGE_MODEL = PASS
IMAGE_MODEL_OUTPUT_READBACK = PASS
```

任一 UNKNOWN/MISSING：`PRODUCTION_GATE = BLOCKED`。

静态能力只代表：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
```

没有真实证据时保持：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

## 3. Current Job Gate

每张图调用 IMAGE_MODEL 前只检查：

```text
CURRENT_JOB_FACTS = CREATED
SOURCE_REFERENCE = CURRENT_USER_IMAGE
OUTPUT_ASPECT_RATIO = EXACT 9:16
A_JOB_CORE = LOADED
CURRENT_CONDITIONAL_REFS = ONLY_RELEVANT_ONES
EXECUTION_CONTRACT = COMPACT_AND_COMPLETE

PRODUCT_LOCK = PASS
SOURCE_SURFACE_STATE = PASS
TOPOLOGY_COMPLETION_PLAN = RESOLVED_OR_NA
BACKGROUND_BIG_IDEA = PASS
BACKGROUND_ARCHITECTURE_PLAN = PASS
HERO_REFRAME_PLAN = PASS_OR_NA
```

面包本体额外：

```text
BAKERY_BREAD_ROUTE = LOADED
```

B 上游 Stage A 额外：

```text
HANDOFF_TO_STAGE_B_ONLY_AFTER_STAGE_A_QC_PASS = TRUE
```

## 4. Prompt Sanity Gate

IMAGE_MODEL Prompt 必须：

```text
FIRST_BLOCK = REFERENCE_LOCK
CURRENT_JOB_ONLY = TRUE
PREVIOUS_JOB_CONTENT = NONE
FULL_REPO_DUMP = FALSE
TEST_CONTENT = NONE
CONFLICTING_CATEGORY_SKINS = NONE
```

Prompt 只保留当前任务可执行信息，不复制规则解释、历史案例和长测试文本。

## 5. Post-Generation Gate

QC 至少判断：

```text
Aspect = EXACT 9:16
Food Identity >=95
Vessel / Container >=98
Surface State Drift = FALSE
Unsupported Completion = FALSE
Background Architecture = PASS
Photography >=85
Semantic >=85
Hero Spatial >=85
Appetite >=85
Critical Failure = NONE
```

失败 → 读取对应 QC/Retry reference → 定向重试。

## 6. READY / Production

Minimal Core + declared capability PASS：

```text
RUNTIME_STATE = READY_WAITING_FOR_START
```

用户“启动”后进入 PRODUCTION。

若首次 live verification 尚未完成，第一笔真实业务兼任验证，不额外生成测试图。

## 7. Recovery

VISION/IMAGE/Credential/图片传递失败、配置 fingerprint 变化、P0 状态丢失 → 回 `SETUP_GATE`。只修具体缺失项。
