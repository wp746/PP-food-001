# PP-food-001

高保真美食商业摄影 Stage A Skill。

当前版本：**6.0.1**

## 目标

把用户真实随手拍升级成 9:16 电影级/商业级 Food Hero，同时锁定真实产品身份、主要食材几何、器皿/包装、摆盘和物理关系。

## V6.0 架构

跨智能体 fail-closed runtime protocol：

```text
AGENTS.md
→ BOOTSTRAP.md
→ RUNTIME_MANIFEST.md
→ REQUIRED_READ_SET.md
→ PRE_FLIGHT_CHECKLIST.md
→ EXECUTION_CONTRACT_TEMPLATE.md
→ Stage A
→ QC / targeted retry
```

核心：P0 规则单一真相源、Mandatory Read、读取证明、每任务 Execution Contract、上下文压缩后重新 Bootstrap、Codex 根目录 AGENTS 自动入口。

## V6.0.1 稳定性补丁

修正“宿主声明支持就被误判成端到端已验证”的问题：

```text
RUNTIME_CAPABILITIES_DECLARED
!=
RUNTIME_CAPABILITIES_VERIFIED
```

- 静态 schema / 配置只能得到 `DECLARED = PASS`；
- 真实调用成功或匹配 verified Runtime Profile 才能得到 `VERIFIED = PASS`；
- 无 verified profile 时允许 READY，但必须标记 `VERIFIED = PENDING`；
- 第一笔真实业务调用兼任一次性验证，不额外浪费测试图；
- verified profile 存在宿主私有持久状态，配置 fingerprint 不变即可跨会话复用；
- 配置变化或真实调用失败立即使 profile 失效；
- fingerprint 和仓库均不得保存 API Key、完整私有 URL 或凭据。

## 用户入口

生产状态下：
- `A` → 只做 Stage A 商拍；
- `B` → 仍先做 Stage A，PASS 后再交给 KV Skill；
- 未说 A/B 且无明显商业信息 → 默认 A；
- 未说 A/B 但给出明显 KV 商业信息 → 自动 B，但仍先 A。

具体硬规则以 `RUNTIME_MANIFEST.md` 为准。

## 与 KV Skill 联动

推荐同时安装 `wp746/wp746-PP-food-KV-001`。

```text
原始图
→ PP-food-001 Stage A
→ Stage A QC
→ Stage A PASS 图
→ PP-food-KV-001 Stage B
```

Stage B 不得回退原始随手拍。

## 首次安装

从 `BOOTSTRAP.md` 开始。运行模型和 Credential 按 `HANDOFF.md` 配置。Pre-flight 的 Declared 能力通过后进入 READY；Verified 状态按 Runtime Profile / 首次真实调用证据决定。