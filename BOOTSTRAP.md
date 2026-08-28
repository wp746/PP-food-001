# PP-food-001 Bootstrap Protocol

本文件解决跨智能体最常见的失效：只读 `SKILL.md`、选择性跳过 references、上下文压缩后凭摘要继续生产。

## 1. Bootstrap Triggers

以下任一情况必须重新执行本流程：

- 首次 clone / 安装 / 加载；
- 新智能体或新会话；
- `VERSION` 发生变化；
- 上下文被压缩、重置或恢复；
- 智能体不能准确复述当前 P0 规则；
- 运行能力或连接状态未知。

## 2. Mandatory Read Order

在任何生产动作之前，按顺序读取：

```text
1. VERSION
2. RUNTIME_MANIFEST.md
3. SKILL.md
4. HANDOFF.md
5. REQUIRED_READ_SET.md
6. PRE_FLIGHT_CHECKLIST.md
7. REQUIRED_READ_SET.md 中的 ALWAYS_LOAD references
8. tests/runtime-handoff-tests.md
9. tests/test-cases.md
10. EXECUTION_CONTRACT_TEMPLATE.md
```

禁止：
- 根据自己的判断跳过 ALWAYS_LOAD；
- 只读文件摘要代替正文；
- 在 Mandatory Read 完成前生成图片；
- 把旧会话记忆当作当前仓库规则。

## 3. Rule Authority

```text
P0 runtime invariants: RUNTIME_MANIFEST.md
Stage role / entrypoint: SKILL.md
Runtime configuration: HANDOFF.md
Detailed methods: references/
Acceptance / regression: tests/
Current-job compilation: EXECUTION_CONTRACT_TEMPLATE.md
```

如果发现这些文件存在真实冲突，不得自行猜测优先级并继续生产；应 `PRODUCTION_GATE = BLOCKED`，指出冲突并等待修复。

## 4. Bootstrap Proof

Mandatory Read 完成后，智能体必须能准确给出以下事实；不能只说“已阅读”：

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

任一项答不准 → 重新读取对应文件，不能进入 READY。

## 5. Runtime Gate

Bootstrap Proof 通过后执行 `PRE_FLIGHT_CHECKLIST.md`。

只有：

```text
BOOTSTRAP_READ = PASS
RUNTIME_CAPABILITIES = PASS
PRODUCTION_GATE = PASS
```

才允许进入：

```text
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

收到用户“启动”后才进入 `PRODUCTION`。

## 6. Production Refresh

进入 PRODUCTION 后不必每张图重读全部仓库，但每个新任务必须：

1. 以当前 `RUNTIME_MANIFEST.md` 为 P0 规则；
2. 根据 `REQUIRED_READ_SET.md` 加载本任务 CONDITIONAL references；
3. 建立新的 `CURRENT_JOB_FACTS`；
4. 按 `EXECUTION_CONTRACT_TEMPLATE.md` 编译当前任务合同；
5. 合同未完成不得调用 IMAGE_MODEL。

如果长对话后无法确认 P0 规则仍在活跃上下文，重新 Bootstrap，而不是依赖压缩摘要。