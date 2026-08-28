# PP-food-001 Bootstrap Protocol

本文件解决跨智能体最常见的失效：只读 `SKILL.md`、选择性漏读、上下文压缩后凭摘要继续生产。

## 1. Bootstrap Triggers

以下任一情况必须重新执行：
- 首次 clone / 安装 / 加载；
- 新智能体或新会话；
- `VERSION` 变化；
- 上下文被压缩、重置或恢复；
- 无法准确复述当前 P0 规则；
- 运行能力或连接状态未知。

## 2. Mandatory Read Order

任何生产动作之前按顺序读取：

```text
1. VERSION
2. RUNTIME_MANIFEST.md
3. SKILL.md
4. HANDOFF.md
5. REQUIRED_READ_SET.md
6. PRE_FLIGHT_CHECKLIST.md
7. REQUIRED_READ_SET.md 的 COLD_START_ALWAYS_LOAD references
8. tests/runtime-handoff-tests.md
9. tests/test-cases.md
10. EXECUTION_CONTRACT_TEMPLATE.md
```

禁止：
- 自行跳过 COLD_START_ALWAYS_LOAD；
- 用摘要代替正文；
- Mandatory Read 未完成就生成图片；
- 把旧会话记忆当当前仓库规则。

## 3. Rule Authority

```text
P0 runtime invariants: RUNTIME_MANIFEST.md
Stage role / entrypoint: SKILL.md
Runtime configuration: HANDOFF.md
Detailed methods: references/
Acceptance / regression: tests/
Current-job compilation: EXECUTION_CONTRACT_TEMPLATE.md
```

发现真实冲突：

```text
PRODUCTION_GATE = BLOCKED
```

指出冲突，不自行选一个版本继续。

## 4. Bootstrap Proof

Mandatory Read 后必须准确给出：

```text
REPO_VERSION = <VERSION>
DEFAULT_ASPECT_RATIO = 9:16
DEFAULT_INTENT_WITHOUT_BUSINESS_INFO = A
EXPLICIT_A_OVERRIDES_AUTO_B = TRUE
B_REQUIRES_STAGE_A_PASS = TRUE
FOOD_IDENTITY_TARGET = >=95
INGREDIENT_GEOMETRY_TARGET = >=95
VESSEL_TARGET = >=98
PLATING_TARGET = >=95
PHYSICAL_RELATIONSHIP_TARGET = >=95
HERO_SPATIAL_TARGET = >=85
APPETITE_TARGET = >=85
RETRY_MODE = TARGETED_NOT_RANDOM
```

任一答不准 → 重读对应文件，不能 READY。

## 5. Runtime Gate

Bootstrap Proof 后执行 `PRE_FLIGHT_CHECKLIST.md`。

只有：

```text
BOOTSTRAP_READ = PASS
RUNTIME_CAPABILITIES = PASS
PRODUCTION_GATE = PASS
```

才允许：

```text
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

等待用户“启动”后进入 PRODUCTION。

## 6. Production Refresh

每个新任务必须：

1. 刷新 `RUNTIME_MANIFEST.md`；
2. 读取 `REQUIRED_READ_SET.md` 的 `A_JOB_ALWAYS_LOAD`；
3. 加载当前品类需要的 `CATEGORY_CONDITIONAL_LOAD`；
4. 新建 `CURRENT_JOB_FACTS`；
5. 按 `EXECUTION_CONTRACT_TEMPLATE.md` 编译合同；
6. Contract 未完成不得调用 IMAGE_MODEL。

长对话后无法证明 Cold-Start Core 仍在活跃上下文 → 重新 Bootstrap。