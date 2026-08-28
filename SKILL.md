---
name: universal-food-commercial-photography
description: Use when turning a user-provided food photo into a high-fidelity world-class commercial Food Hero image while preserving exact product truth, source surface/material state, and plating topology.
version: 6.1.1
---

# PP-food-001 V6.1.1

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
→ Surface State Manifest
→ Topology Completion Plan
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

> **锁产品结构，也锁产品当前表面/火候/熟度状态；摄影升级不能重新烹饪产品。**

> **装盘没拍全时允许补全，但只能延续同一份产品拓扑，不能借补全重新摆盘。**

## V6.1.1 Surface-State Fidelity Patch

本版本修正“食材结构锁住了，但为了食欲感把表皮、烘烤色、焦化、油亮、湿润或酱汁状态推过头”的问题。

全品类硬规则：

```text
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
REVEAL_EXISTING_PROPERTY = YES
AMPLIFY_PROPERTY_BEYOND_SOURCE = NO
```

必须锁定源图已有的：
- 基础颜色与梯度；
- 烘烤/焦化程度；
- 熟度；
- 油亮/哑光等级；
- 湿润度；
- 酱汁/油覆盖；
- 脆壳/皮肤状态；
- 裂纹/割口；
- 奶油/糖霜；
- 冷凝/冰霜/透明度等可见状态。

允许通过灯光、曝光、显色、镜面高光控制、微对比、纹理解析和色彩分级让这些属性**更清楚**；不允许把它们**变得更强**。

### Topology-Preserving Completion

源图因裁切或取景没有拍全时：

```text
HIGH confidence → natural continuation
MEDIUM confidence → minimum conservative continuation
LOW / UNKNOWN → do not invent product content
```

补全必须延续同一食材身份、几何/切法、尺度、方向、层级、重叠、密度、表面状态、酱汁状态和器皿/承载关系。

> **Complete the same serving; do not design a better serving.**

## V6.1 Hero-Stage Stabilization

```text
Food DNA / Source Surface State / Direct Support
> World-Class Hero Stage
> Category Semantic Translation
> Generic Venue Appearance
```

- generic `DISPLAY_CASE` 只锁产品与直接托盘/承载，不默认锁整个柜体/墙面；
- `CONTROLLED_HERO_REFRAME_ALLOWED = TRUE`，锁产品视图几何，不锁源相机坐标；
- 多产品建立 `PRIMARY_HERO_UNIT / CLUSTER + SUPPORTING_PRODUCT_FIELD`，只用光学手段做层级；
- L4 必须有至少两个可感知的后退材质/光影线索；
- 面包主体强制加载 `references/bakery-bread-route.md`；
- 高保真但仍像店内库存/展示照，Hero Spatial QC 必须 FAIL 并定向重试。

## Runtime Protocol

必须使用：
- `BOOTSTRAP.md`
- `RUNTIME_MANIFEST.md`
- `REQUIRED_READ_SET.md`
- `PRE_FLIGHT_CHECKLIST.md`
- `EXECUTION_CONTRACT_TEMPLATE.md`
- `HANDOFF.md`

`references/surface-state-lock.md` 属于 Cold-Start Core，不能跳过。

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

Stage A 始终执行：锁结构 + 锁表面状态 + 商拍 Hero + QC。

当前意图为 B 时，必须先完成 Stage A；只有当前任务 Stage A PASS 图才能交给 `PP-food-KV-001`。

## Acceptance

必须执行 `tests/runtime-handoff-tests.md` 和 `tests/test-cases.md`。

Mandatory Read、Pre-flight、Execution Contract、Surface State、Completion Plan、Hero plans 或 declared runtime ability 任一无法确认：

```text
PRODUCTION_GATE = BLOCKED
```

禁止先出图再补规则。

## Security Boundary

仓库不得保存具体供应商名、私有聚合平台配置、实际 API Base URL、API Key、私有凭据或 Runtime Profile 真实运行值。运行值由宿主 Secret / Environment / Connection / 私有持久状态提供。