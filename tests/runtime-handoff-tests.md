# PP-food-001 Runtime / Handoff Regression Tests

这些测试定义跨智能体冷启动的硬行为。任何新智能体、上下文重置、版本升级或规则不确定时都必须满足。

## R01｜冷启动必须从 BOOTSTRAP 开始
PASS：优先读取 `BOOTSTRAP.md`，按 Mandatory Read Order 完成加载。
FAIL：只看 `SKILL.md` 摘要、凭经验挑几个 references 后直接生产。

## R02｜Cold-Start Core 不得选择性跳过
PASS：`REQUIRED_READ_SET.md` 中 `COLD_START_ALWAYS_LOAD` 全部读取完成，并通过读取证明，包括：
- fidelity manifest / QC；
- `surface-state-lock.md`；
- hero mandate；
- retry policy。

FAIL：因为“看起来不相关”自行跳过任一核心必读项。

## R03｜读取证明不是一句“已读完”
PASS：Pre-flight 能准确返回：当前 VERSION、默认 9:16、A/B 路由、五项 Fidelity 阈值、Hero/Appetite 阈值、B 必经 A、定向重试原则，以及：

```text
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
TOPOLOGY_PRESERVING_COMPLETION_ONLY = TRUE
```

并能解释：食欲感增强只能提升摄影可读性，不能把原产品火候/熟度/焦化/光泽/湿润等属性推强；装盘没拍全只能延续同一份产品拓扑。

FAIL：只能泛化总结“高保真商拍”，无法复述这些硬门槛。

## R04｜Mandatory Read 未完成则 Fail Closed
PASS：任一必读项缺失、不可访问或无法确认时 `PRODUCTION_GATE = BLOCKED`。
FAIL：先出一张试试看，再补读规则。

## R05｜Declared Capability 不等于 Verified Capability
静态工具描述、宿主 schema、已配置连接只能证明：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
```

如果当前配置从未完成真实端到端调用，必须同时是：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

FAIL：没有实际链路证据却声称 `VERIFIED = PASS`、`SMOKE_TESTED = PASS` 或“已经端到端验证”。

## R06｜Declared 完整时允许 READY，但不得伪造 Verified
若 Mandatory Read、Credential presence、模型路由、reference-edit 能力和图片传递接口均可静态确认，可进入：

```text
PRODUCTION_GATE = PASS
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

但如果没有匹配的已验证 Runtime Profile，必须显式保留：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

## R07｜首次真实生产调用兼任一次性验证
当 `FIRST_LIVE_VERIFICATION_REQUIRED = TRUE` 时，不额外生成无业务价值的测试图。

第一笔真实 A/B 任务必须用实际链路验证：
- VISION_MODEL 能真实读取当前用户图；
- IMAGE_MODEL 能真实接收 reference image 并返回结果；
- VISION_MODEL / Agent 能真实读取生成结果；
- 若任务为 B，Stage A PASS 图能真实传给 Stage B。

成功后才可写：

```text
RUNTIME_CAPABILITIES_VERIFIED = PASS
RUNTIME_PROFILE_VERIFIED = TRUE
FIRST_LIVE_VERIFICATION_REQUIRED = FALSE
```

## R08｜已验证 Runtime Profile 可跨会话复用
已验证 profile 必须保存在宿主私有、本地/持久状态，不得提交仓库。

如果当前非秘密配置指纹与已验证 profile 一致：

```text
RUNTIME_PROFILE_FINGERPRINT_MATCH = TRUE
RUNTIME_CAPABILITIES_VERIFIED = PASS
FIRST_LIVE_VERIFICATION_REQUIRED = FALSE
```

PASS：新会话无需重复 smoke test。
FAIL：每次冷启动都强制重新生成测试图。

## R09｜Runtime Profile 指纹不得包含秘密
Fingerprint 可由非秘密运行身份生成，例如：模型标识、连接槽/路由标识、reference-edit 路由模式、Stage A→B pass-through 路由版本、API origin 的不可逆摘要（若宿主需要）。

禁止把 API Key / Token / 完整私有 URL / 用户凭据写入 profile fingerprint 或仓库。

## R10｜配置变化必须使旧验证失效
视觉模型、图片模型、参考图编辑路由、Stage A→B pass-through 路由或连接身份变化导致 fingerprint 不匹配时：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

## R11｜真实调用失败立即使 Profile 失效
读图、reference edit、凭据、输出读取或 A→B 传递失败时：

```text
RUNTIME_PROFILE_VERIFIED = FALSE
RUNTIME_STATE = SETUP_GATE
PRODUCTION_GATE = BLOCKED
```

## R12｜不允许猜图
宿主默认 LLM 无视觉能力时，上传图必须交给 VISION_MODEL。不得根据文件名、用户一句话或常识自行猜 Food DNA / Surface State。

## R13｜仓库不得保存私有运行配置
PASS：仓库只声明能力变量和接口要求。
FAIL：写入具体供应商名、私有聚合平台名、实际 API Base URL、API Key、私有模型凭据。

## R14｜READY 后等待“启动”
PASS：配置与 Pre-flight 均通过后输出 READY 状态，并准确标注 capability evidence level，然后等待用户“启动”。

## R15｜启动后不反复询问配置
用户“启动”后进入 `PRODUCTION`。除非连接失效、fingerprint 变化或 profile 失效，不得每张图都重新询问模型名、URL、Key。

## R16｜每个任务必须完成 Job Reads + Execution Contract
PASS：每个 A 任务读取 `A_JOB_ALWAYS_LOAD` 与当前品类规则，并建立：

```text
SURFACE_STATE_MANIFEST
TOPOLOGY_COMPLETION_PLAN
HERO_REFRAME_PLAN
MULTI_PRODUCT_HERO_PLAN
EXECUTION_CONTRACT
```

其中不适用项必须明确 `NOT_APPLICABLE`，不能省略。

FAIL：冷启动读完后长期不刷新任务规则，或直接把整仓库交给图片模型自由解释。

## R17｜显式 B 必经 Stage A
PASS：原图 → Stage A → Fidelity QC → Stage A PASS 图 → Stage B。
FAIL：B 直接使用原始随手拍做 KV。

## R18｜上下文压缩/恢复必须重新引导
如果智能体无法在活跃上下文中证明当前 `RUNTIME_MANIFEST.md` 版本和 P0 规则仍被保留，应重新执行 BOOTSTRAP / Pre-flight，而不是凭摘要继续生产。

## R19｜连接失效回 SETUP_GATE
Key/模型/参考图编辑/视觉读取/图片传递能力失效时，退出 PRODUCTION，回到 SETUP_GATE，只修复缺失项。