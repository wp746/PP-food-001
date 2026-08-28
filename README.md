# PP-food-001

高保真美食商业摄影 Stage A Skill。

当前版本：**6.0.0**

## 目标

把用户真实随手拍升级成 9:16 电影级/商业级 Food Hero，同时锁定真实产品身份、主要食材几何、器皿/包装、摆盘和物理关系。

## V6.0 的重点

V6.0 不再依赖“智能体自觉把所有文件读全”。新增跨智能体 fail-closed runtime protocol：

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

核心变化：
- P0 规则只在 `RUNTIME_MANIFEST.md` 定义一次；
- 冷启动必须完成 Mandatory Read 与读取证明；
- 漏读 / 能力未知 / Contract 缺失时禁止生产；
- 每个新任务先编译短 Execution Contract，再调用图片模型；
- 上下文压缩后无法证明 P0 规则仍在时重新 Bootstrap；
- Codex 可通过根目录 `AGENTS.md` 自动进入 Bootstrap；
- 仓库不保存任何具体聚合平台、URL、Key 或私有模型配置。

## 用户入口

生产状态下：
- `A` → 只做 Stage A 商拍；
- `B` → 仍先做 Stage A，PASS 后再交给 KV Skill；
- 未说 A/B 且无明显商业信息 → 默认 A；
- 未说 A/B 但给出明显 KV 商业信息 → 自动 B，但仍先 A。

具体硬规则以 `RUNTIME_MANIFEST.md` 为准。

## 与 KV Skill 联动

推荐同时安装：

```text
wp746/wp746-PP-food-KV-001
```

完整链路：

```text
原始图
→ PP-food-001 Stage A
→ Stage A QC
→ Stage A PASS 图
→ PP-food-KV-001 Stage B
```

Stage B 不得回退原始随手拍。

## 首次安装

从 `BOOTSTRAP.md` 开始。运行模型和 Credential 按 `HANDOFF.md` 配置，全部通过后等待用户说“启动”。