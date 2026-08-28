# PP-food-001

高保真美食商业摄影 Stage A Skill。

当前版本：**6.1.0**

## 目标

把用户真实随手拍升级成 9:16 世界级商业 Food Hero，同时锁定真实产品身份、主要食材/材质几何、器皿/包装、排列和物理关系。

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

核心：P0 单一真相源、Mandatory Read、读取证明、每任务 Execution Contract、上下文压缩后重新 Bootstrap、Codex 根目录 AGENTS 自动入口。

## V6.1 Hero-Stage Stabilization

解决跨 Agent 中“产品锁住了，但只生成更漂亮的店内展示照”的问题。

核心关系：

```text
Food DNA / Direct Support
> World-Class Hero Stage
> Category Semantic Translation
> Generic Venue Appearance
```

新增：
- 普通 `DISPLAY_CASE` 不再默认锁死柜体/墙面；只锁产品与直接托盘/承载关系；
- 允许 Controlled Hero Reframe：锁产品视图几何，不锁随手拍相机坐标；
- 多产品必须建立 Primary Hero + Supporting Product Field，禁止库存式等权陈列；
- Hero QC 对 L1/L2/L3/L4 使用可观察证据；单一虚墙、渐变或一团 bokeh 不算 L4；
- 面包类增加 `BAKERY_BREAD_HERO` 专属路线，避免默认咖啡馆 Lifestyle / 原木+亚麻+黄铜模板；
- 高保真但仍像普通门店/展示柜照片，必须 Hero Retry，不能交付。

## V6.0.1 Runtime Evidence

```text
RUNTIME_CAPABILITIES_DECLARED
!=
RUNTIME_CAPABILITIES_VERIFIED
```

静态 schema/配置只证明 Declared；真实调用或匹配 verified Runtime Profile 才能证明 Verified。第一笔真实业务可兼任验证，不额外浪费测试图。

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