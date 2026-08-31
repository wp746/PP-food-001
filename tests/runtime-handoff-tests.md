# PP-food-001 Runtime / Handoff Regression Tests

这些测试用于 **Skill 开发、升级和回归审计**。它们不是正常生产任务的 Mandatory Runtime Read。

## R01｜冷启动从 BOOTSTRAP 开始
PASS：新智能体先读 `BOOTSTRAP.md`。
FAIL：只读 `SKILL.md` 摘要后直接出图。

## R02｜Runtime Minimal Core
正常生产冷启动只允许加载 Minimal Core：

```text
VERSION
RUNTIME_MANIFEST.md
SKILL.md
SOP-A.md
HANDOFF.md
REQUIRED_READ_SET.md
PRE_FLIGHT_CHECKLIST.md
EXECUTION_CONTRACT_TEMPLATE.md
```

PASS：tests 不进入生产上下文；references 按当前任务条件加载。
FAIL：冷启动把 tests + 全部 references 一次性塞入上下文。

## R03｜Tests = Development Only
PASS：仅在版本升级、Skill 审计、回归验证时读取 `tests/*`。
FAIL：每张图生产前都读取 tests。

## R04｜禁止整仓库 Prompt Dump
PASS：Agent 读取规则后，只为当前任务编译短 `EXECUTION_CONTRACT` 和短 IMAGE_MODEL Prompt。
FAIL：把整个仓库、SOP、tests、references 原文拼给 IMAGE_MODEL。

## R05｜当前任务隔离
PASS：每张新图新建 `CURRENT_JOB_FACTS`；上一任务产品、品牌、文案、背景皮肤默认失效。
FAIL：继承上一任务 Food Entity / visual skin。

## R06｜不允许猜图
宿主默认 LLM 无视觉能力时，必须调用 VISION_MODEL 读取当前图。

## R07｜Declared != Verified
静态能力只证明 `RUNTIME_CAPABILITIES_DECLARED = PASS`。无真实调用证据时：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

## R08｜首次真实任务兼任验证
不额外生成测试图；第一笔真实业务验证 VISION read → reference edit → output readback。B 任务额外验证 A→B pass-through。

## R09｜A 任务五大锁
必须保持：

```text
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container >=98
Plating / Arrangement >=95
Physical Relationship >=95
```

## R10｜Surface State 不得被“食欲化”重做
PASS：只提升已有属性的摄影可读性。
FAIL：把烘烤、焦化、熟度、油亮、湿润、酱汁覆盖、裂口等强度推高。

## R11｜Background Architecture > Prop Pack
PASS：高级感来自空间、材质、光影、纵深；删除道具后舞台仍成立。
FAIL：主要靠亚麻、麦穗、咖啡杯、陶罐、夹子、bokeh 等道具包。

## R12｜Reference Lock 必须在 IMAGE_MODEL Prompt 首段
FAIL：只写“参考原图”或把锁定规则放到 Prompt 尾部。

## R13｜Exact 9:16
非严格 9:16 最终 Stage A 输出 = CRITICAL FAILURE。

## R14｜Targeted Retry Only
PASS：先诊断具体失败项再重试。
FAIL：随机整张重抽、同时改变产品和背景。

## R15｜B 必经当前 Stage A PASS
显式 B：当前原图 → 当前 Stage A → QC PASS → 当前 Stage A PASS 图 → Stage B。

## R16｜Context Budget
每个 A 任务只加载当前任务真正需要的 reference。若一个规则与当前品类/场景无关，不得为了“保险”全部加载。

## R17｜连接失效 Fail Closed
VISION / IMAGE reference-edit / Credential / 图片传递失败 → 回 `SETUP_GATE`，不得假装正常生产。
