# PP-food-001

高保真美食商业摄影 Stage A Skill。

当前版本：**6.1.1**

## 目标

把用户真实随手拍升级成 9:16 世界级商业 Food Hero，同时锁定真实产品身份、主要食材/材质几何、器皿/包装、排列、物理关系，以及**原产品当前的表面/火候/熟度状态**。

## Runtime 架构

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

## V6.1.1 Surface-State Fidelity Patch

解决“食材结构锁住，但为了更有食欲把表皮、烘烤色、焦化、油亮、湿润、酱汁状态推过头”的问题。

全品类硬规则：

```text
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
REVEAL_EXISTING_PROPERTY = YES
AMPLIFY_PROPERTY_BEYOND_SOURCE = NO
```

新增 `references/surface-state-lock.md`，对所有食品统一约束：
- 原图烘烤深浅、焦化、熟度不可被重新强化；
- 原图油亮/哑光、湿润度、酱汁覆盖不可凭“高级感”放大；
- 原图裂纹/割口/表皮结构只能被更好的光线读出来，不能重做；
- Appetite Score 必须来自摄影提升，而不是把食物重新烹饪一遍。

### Topology-Preserving Completion

如果原图装盘/器皿因为裁切没拍全，允许补全，但只能延续**同一份产品**：

```text
HIGH confidence → natural continuation
MEDIUM confidence → minimum conservative continuation
LOW / UNKNOWN → environment extension / crop, do not invent food
```

补全必须继承原食材身份、几何/切法、尺度、方向、层级、重叠、密度、表面状态、酱汁状态和直接承载关系。

> Complete the same serving; do not design a better serving.

## V6.1 Hero-Stage Stabilization

解决跨 Agent 中“产品锁住了，但只生成更漂亮的店内展示照”的问题。

```text
Food DNA / Source Surface State / Direct Support
> World-Class Hero Stage
> Category Semantic Translation
> Generic Venue Appearance
```

核心：
- 普通 `DISPLAY_CASE` 不再锁死柜体/墙面；
- Controlled Hero Reframe 锁产品视图几何，不锁随手拍相机坐标；
- 多产品必须建立 Primary Hero + Supporting Product Field；
- Hero QC 对 L1/L2/L3/L4 使用可观察证据；
- 面包类使用 `BAKERY_BREAD_HERO`，避免咖啡 Lifestyle 模板；
- 高保真但仍像普通门店/展示柜照片，必须 Hero Retry。

## Runtime Evidence

```text
RUNTIME_CAPABILITIES_DECLARED
!=
RUNTIME_CAPABILITIES_VERIFIED
```

静态 schema/配置只证明 Declared；真实调用或匹配 verified Runtime Profile 才能证明 Verified。第一笔真实业务可兼任验证。

## 用户入口

生产状态下：
- `A` → 只做 Stage A；
- `B` → 仍先做 Stage A，PASS 后交给 KV Skill；
- 未说 A/B 且无明显商业信息 → 默认 A；
- 未说 A/B 但给出明显 KV 商业信息 → 自动 B，但仍先 A。

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

从 `BOOTSTRAP.md` 开始。模型和 Credential 按 `HANDOFF.md` 配置。具体私有平台、URL、Key、Runtime Profile 值不写入仓库。