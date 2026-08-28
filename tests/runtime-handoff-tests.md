# PP-food-001 Runtime / Handoff Regression Tests

这些测试定义跨智能体冷启动的硬行为。任何新智能体、上下文重置、版本升级或规则不确定时都必须满足。

## R01｜冷启动必须从 BOOTSTRAP 开始

PASS：优先读取 `BOOTSTRAP.md`，按其 Mandatory Read Order 完成加载。
FAIL：只看 `SKILL.md` 摘要、凭经验挑几个 references 后直接生产。

## R02｜必读集不得选择性跳过

PASS：`REQUIRED_READ_SET.md` 中 ALWAYS_LOAD 的文件全部读取完成，并通过读取证明。
FAIL：因为“看起来不相关”自行跳过 fidelity / hero / retry / semantic / tests 中任一必读项。

## R03｜读取证明不是一句“已读完”

PASS：Pre-flight 能准确返回：当前 VERSION、默认 9:16、A/B 路由、五项 Fidelity 阈值、Hero/Appetite 阈值、B 必经 A、定向重试原则。
FAIL：只能泛化总结“高保真商拍”，无法复述硬门槛。

## R04｜Mandatory Read 未完成则 Fail Closed

PASS：任一必读项缺失、不可访问或无法确认时 `PRODUCTION_GATE = BLOCKED`。
FAIL：先出一张试试看，再补读规则。

## R05｜运行能力未确认则 Fail Closed

READY 前必须确认：
- VISION_MODEL 能读用户图与生成结果；
- IMAGE_MODEL 支持 reference-image edit / image-to-image；
- Credential 已配置；
- 图片可从宿主传给 IMAGE_MODEL；
- IMAGE_MODEL 输出可继续被宿主读取/传递。

任一 UNKNOWN/MISSING → BLOCKED。

## R06｜不允许猜图

宿主默认 LLM 无视觉能力时，上传图必须交给 VISION_MODEL。
不得根据文件名、用户一句话或常识自行猜 Food DNA。

## R07｜仓库不得保存私有运行配置

PASS：仓库只声明能力变量和接口要求。
FAIL：写入具体供应商名、私有聚合平台名、实际 API Base URL、API Key、私有模型凭据。

## R08｜READY 后等待“启动”

PASS：配置与 Pre-flight 均通过后输出：

```text
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

并等待用户“启动”。

## R09｜启动后不反复询问配置

用户“启动”后进入 `PRODUCTION`。除非连接失效，不得每张图都重新询问模型名、URL、Key。

## R10｜每个任务必须建立 Execution Contract

PASS：生成前根据 `EXECUTION_CONTRACT_TEMPLATE.md` 建立当前任务合同，锁定 JOB_MODE、9:16、CURRENT_JOB_FACTS、Food DNA、创意边界和禁止项。
FAIL：直接把几万字仓库规则原样丢给图片模型自由解释。

## R11｜显式 B 必经 Stage A

PASS：原图 → Stage A → Fidelity QC → Stage A PASS 图 → Stage B。
FAIL：B 直接使用原始随手拍做 KV。

## R12｜上下文压缩/恢复必须重新引导

如果智能体无法在活跃上下文中证明当前 `RUNTIME_MANIFEST.md` 版本和 P0 规则仍被保留，应重新执行 BOOTSTRAP / Pre-flight，而不是凭摘要继续生产。

## R13｜连接失效回 SETUP_GATE

Key/模型/参考图编辑/视觉读取/图片传递能力失效时，退出 PRODUCTION，回到 SETUP_GATE，只修复缺失项。