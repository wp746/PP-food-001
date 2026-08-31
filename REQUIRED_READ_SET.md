# PP-food-001 Required Read Set

目标：**当前任务需要什么就读什么。防止全仓库加载造成规则稀释、示例串台和 Prompt 过载。**

## A_JOB_CORE｜每个 Stage A 任务必读

只固定加载：

```text
references/fidelity-manifest.md
references/surface-state-lock.md
references/hero-background-architecture.md
references/execution-template.md
```

这 4 个文件负责：产品锁定、表面状态、Hero 背景架构、当前 IMAGE_MODEL 指令编译。

## POST_GENERATION_CORE｜生成后按需

```text
references/fidelity-qc.md
references/semantic-qc.md
references/retry-policy.md
```

只在 QC / Retry 阶段读取；不要提前把完整 QC/Retry 文档塞入生成 Prompt。

## CONDITIONAL_LOAD｜当前任务才加载

### 1. 菜品/风味语义需要细化

```text
references/dish-semantic-router.md
references/cuisine-style-map.md
references/semantic-background-rules.md
```

用户已明确菜名/品类且基础语义足够时，不必为了“完整”全部加载。

### 2. 面包本体

贝果、碱水、恰巴塔、欧包、酸种、法棍、餐包等：

```text
references/bakery-bread-route.md
SELECTED_STAGE_A_ROUTE = BAKERY_BREAD_HERO
```

### 3. 原场景/直接承载关系复杂

手持、托盘、展示柜、货架、街头、桌面关系需要判断时：

```text
references/scene-modules.md
```

### 4. 食物材质确实需要专项解析

```text
references/food-modules.md
```

只选 1 个主模块 + 最多 2 个必要辅模块。

## Anti-Overload Rules

```text
LOAD_ALL_REFERENCES = FORBIDDEN
LOAD_ALL_CATEGORIES = FORBIDDEN
LOAD_ALL_EXAMPLES = FORBIDDEN
TESTS_DURING_NORMAL_PRODUCTION = FORBIDDEN
```

每个任务的 active reference 只保留当前任务相关规则。若多个长 reference 都可能有用，先抽取当前条目，不把整份长文档同时放进工作上下文。

## A-Job Proof

调用 IMAGE_MODEL 前只需确认：

```text
CURRENT_JOB_FACTS = CREATED
SOURCE_SURFACE_STATE = RESOLVED
TOPOLOGY_COMPLETION = RESOLVED_OR_NA
SEMANTIC_ROUTE = RESOLVED_OR_CONSERVATIVE
BACKGROUND_BIG_IDEA = CREATED
BACKGROUND_ARCHITECTURE_PLAN = CREATED
HERO_REFRAME = CREATED_OR_NA
EXECUTION_CONTRACT = COMPACT_AND_CURRENT_JOB_ONLY
```

如果这些字段无法建立，`PRODUCTION_GATE = BLOCKED`。

## Production Refresh

每张新图重新建立 `CURRENT_JOB_FACTS`，重新选择 conditional refs。上一任务的品类/场景 reference 不自动延续。
