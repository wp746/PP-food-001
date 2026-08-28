# PP-food-001

高保真美食商业摄影 Stage A Skill。

当前版本：**6.2.1**

## 目标

把用户真实随手拍升级成**严格 9:16**世界级商业 Food Hero，同时锁定真实产品身份、食材/产品几何、器皿/包装、排列、物理关系，以及原产品当前表面/火候/熟度状态。

## Runtime

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

## V6.2.1 核心

### 1. Exact 9:16

```text
OUTPUT_ASPECT_RATIO_EXACT = 9:16
NON_9_16_DELIVERY = CRITICAL_FAILURE
```

无论源图比例，Stage A 最终交付必须为严格 9:16。非 9:16 不得作为 PASS 图。

### 2. Product-Derived Background Architecture

```text
PRODUCT_DERIVED_STAGE > GENERIC_PREMIUM_STYLE
BACKGROUND_ARCHITECTURE > PROP_STYLING
ONE_BIG_STAGE_IDEA > MANY_DECORATIVE_OBJECTS
```

每任务必须：
- `PRODUCT_DERIVATION_EVIDENCE >=3`；
- 定义一个明确 `BACKGROUND_BIG_IDEA`；
- 用 2–3 个主材质平面/体块建立近/中/深空间；
- 使用高差、遮挡、反射/吸光关系、light cut 和深度递进；
- 9:16 上方继续有设计型空间，不允许大面积虚墙；
- 道具可为 0，删除道具后背景仍必须成立。

核心文件：

```text
references/hero-background-architecture.md
```

### 3. Surface-State Fidelity

```text
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
REVEAL_EXISTING_PROPERTY = YES
AMPLIFY_PROPERTY_BEYOND_SOURCE = NO
```

食欲提升来自摄影，不来自重新烹饪产品。

### 4. Topology-Preserving Completion

装盘/器皿因裁切没拍全时，只允许延续同一份产品拓扑：

```text
HIGH confidence → natural continuation
MEDIUM → minimum conservative continuation
LOW / UNKNOWN → environment extension only
```

> Complete the same serving; do not design a better serving.

### 5. Hero Stage

```text
Food DNA / Source Surface State / Direct Support
> World-Class Hero Stage
> Category Semantic Translation
> Generic Venue Appearance
```

普通展示柜/墙面不默认锁定；允许 Controlled Hero Reframe；多产品建立 Primary Hero + Supporting Product Field；Fake L4、普通店内感、道具包高级感直接 FAIL。

## A / B

- `A` → Stage A only；
- `B` → 仍先完整 Stage A，PASS 后进入 KV；
- 无 A/B 且无明显商业信息 → 默认 A；
- 有明显 KV 商业信息 → 自动 B，但仍先 A。

## Security

仓库不保存具体供应商、私有聚合平台、实际 API Base URL、API Key、私有凭据或 Runtime Profile 运行值。