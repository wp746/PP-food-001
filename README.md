# PP-food-001

高保真美食商业摄影 Stage A Skill。

当前版本：**6.4.0**

## 这版解决什么

V6.4.0 不是继续堆 Prompt，而是针对跨智能体安装后常见的漂移做**运行时减法**：

- 正常生产不再把 tests 和全部 references 一次性读入上下文；
- 每张新图只加载当前任务需要的规则；
- 当前任务与上一任务严格隔离；
- Execution Contract 从超长字段表压缩成 6 个核心块；
- IMAGE_MODEL 只接收当前参考图 + 当前短合同 + 当前短 Prompt；
- 保留 Food DNA、Surface State、9:16、Background Architecture、Targeted Retry 等硬门槛。

核心原则：

> **少而明确的当前任务规则 > 大而全的仓库提示词。**

## Runtime Minimal Core

新智能体从 `BOOTSTRAP.md` 开始，正常生产只加载：

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

`tests/*` 只用于开发/升级/回归，不进入正常出图上下文。

## 执行A

用户上传图片说：

```text
执行A
```

默认：只做 Stage A 商拍，不要求 KV 文案。

链路：

```text
CURRENT USER IMAGE
→ VISION_MODEL
→ CURRENT_JOB_FACTS
→ Compact Execution Contract
→ IMAGE_MODEL reference edit
→ QC
→ targeted retry
→ Stage A PASS
```

## 硬门槛

```text
Output = EXACT 9:16
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container >=98
Plating / Arrangement >=95
Physical Relationship >=95
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
BACKGROUND_ARCHITECTURE > PROP_STYLING
```

## 防漂移

每张新图都建立新的 `CURRENT_JOB_FACTS`。上一任务品牌、产品、场景事实、背景皮肤和示例默认失效。

禁止把整仓库 Markdown 直接塞给图片模型。

## B 联动

`执行B` 仍然先完整执行当前任务 Stage A；只有当前 Stage A QC PASS 图可以交给 `PP-food-KV-001`。

## Security

仓库不保存真实 API Key、私有 Base URL、私有供应商配置或用户凭据。
