---
name: universal-food-commercial-photography
description: Use when turning a user-provided food photo into a high-fidelity world-class commercial Food Hero image while preserving exact product truth and rebuilding only the photography, stage, light and spatial hierarchy.
version: 6.1.0
---

# PP-food-001 V6.1.0

## Mandatory Entry

**Do not start production from this file alone.**

Before any food analysis, prompt building or image generation:

```text
READ BOOTSTRAP.md
→ complete Mandatory Read Order
→ run PRE_FLIGHT_CHECKLIST.md
→ PRODUCTION_GATE must PASS
```

`RUNTIME_MANIFEST.md` is the canonical P0 runtime rule source. If a summary, old conversation, host default behavior or another file appears to weaken a P0 rule, do not silently override the manifest.

## Role

本 Skill 是 **Stage A / World-Class Commercial Re-photography Engine**：

```text
CURRENT USER IMAGE
→ VISION_MODEL analysis
→ CURRENT_JOB_FACTS / Fidelity Manifest
→ Scene Context Split
→ Category Route
→ Hero Reframe / Multi-Product Hero Plan
→ Stage A Execution Contract
→ IMAGE_MODEL reference-image edit
→ Stage A Fidelity + Semantic + Hero + Appetite QC
→ targeted retry if needed
→ Stage A PASS image
```

核心原则：

> **锁产品，不锁偶然的随手拍相机和普通门店背景。**

产品、直接承载、排列和物理关系必须高保真；普通柜体、墙面、门店背景和偶然相机坐标不能以“保真”为理由压掉 Hero Stage。

## V6.1 Hero-Stage Stabilization

本版本修正跨 Agent 中“Food DNA 对，但商拍仍像普通展示照”的问题：

```text
Food DNA / Direct Support
> World-Class Hero Stage
> Category Semantic Translation
> Generic Venue Appearance
```

新增硬行为：
- generic `DISPLAY_CASE` 只锁产品与直接托盘/承载，不默认锁整个柜体/墙面；
- `CONTROLLED_HERO_REFRAME_ALLOWED = TRUE`，锁产品视图几何，不锁源相机坐标；
- 多产品场景必须建立 `PRIMARY_HERO_UNIT / CLUSTER + SUPPORTING_PRODUCT_FIELD`，只用光学手段做层级；
- L4 必须有至少两个可感知的后退材质/光影线索，单一虚墙/渐变/bokeh 不算四层空间；
- 面包主体强制加载 `references/bakery-bread-route.md`，不再默认继承咖啡 Lifestyle 皮肤；
- 高保真但仍像店内库存/展示照，Hero Spatial QC 必须判 FAIL 并定向重试。

## Runtime Protocol

必须使用：
- `BOOTSTRAP.md` — 冷启动与恢复；
- `RUNTIME_MANIFEST.md` — P0；
- `REQUIRED_READ_SET.md` — Cold Start / A Job / Category 条件加载；
- `PRE_FLIGHT_CHECKLIST.md` — READY 与每任务生产门禁；
- `EXECUTION_CONTRACT_TEMPLATE.md` — 当前任务短合同；
- `HANDOFF.md` — 模型能力、凭据与 Runtime Profile。

生产时不要把整仓库 Markdown 原样拼进图片 Prompt。先读取规则，再编译当前 `EXECUTION_CONTRACT`，最后生成短而明确的 IMAGE_MODEL 指令。

## Capability Evidence Rule

READY 不等于端到端已验证：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS / BLOCKED
RUNTIME_CAPABILITIES_VERIFIED = PASS / PENDING / BLOCKED
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE / FALSE
```

若当前配置没有匹配的 verified Runtime Profile，第一笔真实业务调用兼任验证；不要额外生成无业务价值测试图。

## A / B Relationship

A/B 优先级以 `RUNTIME_MANIFEST.md` 为唯一真相。

Stage A 始终执行：锁产品 → 世界级商拍 Hero → QC。

当前意图为 B 时，必须先完成 Stage A；只有当前任务 Stage A PASS 图才能交给 `PP-food-KV-001`。

## Detailed Methods

不要自行挑文件。按 `REQUIRED_READ_SET.md` 执行。

核心详细规则：
- Fidelity Manifest / QC；
- Hero Shot Mandate；
- Semantic Router / Background / QC；
- Scene Modules；
- Cuisine / Food Modules；
- `bakery-bread-route.md`；
- Execution Template；
- Targeted Retry。

References 解释“怎么做”；`RUNTIME_MANIFEST.md` 决定“什么绝不能违反”。

## Acceptance

必须执行 `tests/runtime-handoff-tests.md` 和 `tests/test-cases.md`。

Mandatory Read、Pre-flight、Execution Contract、Hero plans 或 declared runtime ability 任一无法确认：

```text
PRODUCTION_GATE = BLOCKED
```

禁止先出图再补规则。

## Security Boundary

仓库不得保存具体供应商名、私有聚合平台配置、实际 API Base URL、API Key、私有凭据或 Runtime Profile 真实运行值。运行值由宿主 Secret / Environment / Connection / 私有持久状态提供。