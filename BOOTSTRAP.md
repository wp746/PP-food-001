# PP-food-001 Bootstrap Protocol

目标：跨智能体冷启动时既不漏掉 P0，又避免“读太多 → 规则互相稀释 → Prompt 过载 → 出图漂移”。

## 1. Bootstrap Triggers

以下任一情况重新执行：首次安装/新会话、VERSION 变化、上下文压缩/恢复、运行能力未知、无法准确复述当前 P0。

## 2. Runtime Minimal Core｜正常生产必读

按顺序读取：

```text
1. VERSION
2. RUNTIME_MANIFEST.md
3. SKILL.md
4. SOP-A.md
5. HANDOFF.md
6. REQUIRED_READ_SET.md
7. PRE_FLIGHT_CHECKLIST.md
8. EXECUTION_CONTRACT_TEMPLATE.md
```

正常生产 **不要** 在冷启动读取：

```text
tests/*
全部 references/*
README.md
历史案例/旧对话总结
```

`tests/*` 只在 Skill 开发、版本升级、审计、回归验证时读取。

## 3. Authority

```text
P0 invariants              → RUNTIME_MANIFEST.md
A 操作流程                  → SOP-A.md
模型/连接能力               → HANDOFF.md
当前任务加载策略            → REQUIRED_READ_SET.md
生产门禁                    → PRE_FLIGHT_CHECKLIST.md
当前任务编译                → EXECUTION_CONTRACT_TEMPLATE.md
细节方法                    → references/（按需）
开发/回归                   → tests/（非生产）
```

真实冲突未解决：`PRODUCTION_GATE = BLOCKED`。

## 4. Bootstrap Proof｜只证明关键不变量

必须确认：

```text
REPO_VERSION = <VERSION>
DEFAULT_ASPECT_RATIO = EXACT 9:16
EXPLICIT_A = STAGE_A_ONLY
B_REQUIRES_CURRENT_STAGE_A_PASS = TRUE
SOURCE_TRUTH = CURRENT_USER_IMAGE
FOOD_IDENTITY_TARGET >=95
VESSEL_TARGET >=98
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
BACKGROUND_ARCHITECTURE > PROP_STYLING
RETRY_MODE = TARGETED_NOT_RANDOM
```

并能解释：
- 默认宿主不识图时必须显式调用 VISION_MODEL；
- IMAGE_MODEL Prompt 第一段必须锁参考图；
- “更有食欲”不能重新烹饪/重做表面状态；
- 当前任务不能继承上一任务产品事实或视觉皮肤。

答不准 → 重读 Minimal Core 对应文件。

## 5. Context Budget｜防漂移硬规则

正常生产：

```text
FULL_REPO_DUMP = FORBIDDEN
TESTS_IN_RUNTIME_CONTEXT = FORBIDDEN
PREVIOUS_JOB_SKIN_IMPORT = OFF
```

每个任务只按 `REQUIRED_READ_SET.md` 加载当前真正需要的 references。不要因为“保险”把所有品类、所有场景、所有示例一起读入当前任务。

IMAGE_MODEL 永远只收到：

```text
当前参考图
+ 当前任务短 Execution Contract
+ 当前任务短 Prompt
```

不得收到整个仓库 Markdown。

## 6. Runtime Gate

完成 Bootstrap Proof 后运行 `PRE_FLIGHT_CHECKLIST.md`。

静态能力完整即可：

```text
RUNTIME_STATE = READY_WAITING_FOR_START
```

若无真实端到端证据，准确标注 `RUNTIME_CAPABILITIES_VERIFIED = PENDING`；第一笔真实业务兼任验证，不额外生成测试图。

用户说“启动”后进入 `PRODUCTION`。

## 7. Production Refresh｜每张新图

每个新 A 任务：

```text
new CURRENT_JOB_FACTS
→ refresh RUNTIME_MANIFEST P0
→ load A_JOB_CORE
→ load only current conditional refs
→ compile compact EXECUTION_CONTRACT
→ IMAGE_MODEL
→ QC
→ targeted retry if needed
```

不要每张图重新完整 Bootstrap，除非版本/能力/上下文状态发生变化。
