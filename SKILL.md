---
name: universal-food-commercial-photography
description: High-fidelity 9:16 world-class food commercial re-photography with exact product/surface-state preservation and category-native material-architecture Hero stages.
version: 6.2.0
---

# PP-food-001 V6.2.0

## Mandatory Entry

```text
READ BOOTSTRAP.md
→ Mandatory Read Order
→ PRE_FLIGHT_CHECKLIST.md
→ PRODUCTION_GATE must PASS
```

`RUNTIME_MANIFEST.md` is the P0 single source of truth.

## Role

```text
CURRENT USER IMAGE
→ VISION_MODEL
→ CURRENT_JOB_FACTS / Fidelity Manifest
→ Surface State Manifest
→ Topology Completion Plan
→ Scene Context Split
→ Category Route
→ Background Architecture Plan
→ Hero Reframe / Multi-Product Hero Plan
→ Execution Contract
→ IMAGE_MODEL reference edit
→ Fidelity + Semantic + Hero + Appetite + Aspect QC
→ targeted retry
→ Stage A PASS image
```

## V6.2 P0 Output Rule — Exact 9:16

```text
DEFAULT_ASPECT_RATIO = 9:16
OUTPUT_ASPECT_RATIO_EXACT = 9:16
NON_9_16_DELIVERY = CRITICAL_FAILURE
```

无论原图横/方/竖，Stage A 最终成片都必须是严格 9:16 竖版。

如果第一次 IMAGE_MODEL 返回非 9:16，不得交付，必须 canvas correction / outpaint / targeted retry 后重新 QC。

9:16 适配不能通过拉伸、裁坏产品或重做产品实现。

## V6.2 Background Architecture

本版本修正“Food DNA 锁住，但背景仍像普通店内/烘焙图库”的问题。

```text
PRODUCT_DERIVED_STAGE > GENERIC_PREMIUM_STYLE
BACKGROUND_ARCHITECTURE > PROP_STYLING
ONE_BIG_STAGE_IDEA > MANY_DECORATIVE_OBJECTS
```

每个 Stage A 任务必须读取并执行：

```text
references/hero-background-architecture.md
```

必须建立：
- `PRODUCT_DERIVATION_EVIDENCE >=3`；
- 一个明确 `BACKGROUND_BIG_IDEA`；
- 2–3 个主材质平面/体块；
- 近 / 中 / 深空间质量；
- 台面高差、遮挡与纵深；
- light cut / shadow architecture；
- reflective vs absorptive material relationship；
- 9:16 上方继续退进的设计型负空间；
- 道具可为 0，且永远从属。

删除所有辅助道具后，背景仍必须像世界级商业摄影舞台。否则 Background Architecture FAIL。

禁止用亚麻布、夹子、咖啡杯、陶罐、麦穗、香料碟、灯泡/bokeh 等道具包冒充高级感。

## Surface-State Fidelity

```text
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
REVEAL_EXISTING_PROPERTY = YES
AMPLIFY_PROPERTY_BEYOND_SOURCE = NO
```

锁定原图实际基础颜色、火候/熟度、烘烤/焦化、油亮/湿润、酱汁覆盖、皮肤/壳、裂纹/割口、奶油/糖霜、冷凝/透明度等状态。

食欲提升来自摄影读取能力，不来自重新烹饪产品。

## Topology-Preserving Completion

装盘/器皿因源图裁切没拍全时，可以补全**同一份产品**：

```text
HIGH confidence → natural continuation
MEDIUM → minimum conservative continuation
LOW / UNKNOWN → environment extension only
```

> Complete the same serving; do not design a better serving.

## Hero-Stage Rules

```text
Food DNA / Source Surface State / Direct Support
> World-Class Hero Stage
> Category Semantic Translation
> Generic Venue Appearance
```

- generic display case 不默认锁柜体/墙面；
- source camera coordinates 不是 Food DNA；
- 允许 Controlled Hero Reframe；
- 多产品必须 Primary Hero + Supporting Product Field；
- L1/L2/L3/L4 必须有可观察证据；
- Fake L4、普通展示柜感、道具包高级感直接 FAIL。

## A / B

- `A` → Stage A only；
- `B` → 仍先完整 Stage A，PASS 后 Stage B；
- 无 A/B 且无明显商业信息 → 默认 A；
- 无 A/B 但有明显 KV 商业信息 → 自动 B，但仍先 A。

## Runtime Protocol

必须使用：
- `BOOTSTRAP.md`
- `RUNTIME_MANIFEST.md`
- `REQUIRED_READ_SET.md`
- `PRE_FLIGHT_CHECKLIST.md`
- `EXECUTION_CONTRACT_TEMPLATE.md`
- `HANDOFF.md`

不要把整仓库 Markdown 原样塞给 IMAGE_MODEL。先读规则，再编译当前任务 Contract。

## Acceptance

必须满足：

```text
Output Aspect Ratio = EXACT 9:16
Food Fidelity >=95
Vessel Fidelity >=98
Source Surface State = PASS
Background Architecture = PASS
Photography >=85
Semantic >=85
Hero Spatial >=85
Appetite >=85
No Critical Failure
```

Mandatory Read、Pre-flight、Execution Contract、Surface State、Completion Plan、Background Architecture、Hero plans 任一无法确认：

```text
PRODUCTION_GATE = BLOCKED
```

## Security Boundary

仓库不得保存具体供应商名、私有聚合平台配置、实际 API Base URL、API Key、私有凭据或 Runtime Profile 真实运行值。