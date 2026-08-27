---
name: universal-food-commercial-photography
description: Use when turning a user-provided food photo into a high-fidelity premium commercial food image while preserving the exact product, ingredient geometry, vessel/packaging, plating and physical relationships.
version: 5.5.0
---

# PP-food-001 V5.5.0

## Core Principle

> **Source truth first. Lock the product. Upgrade only the photography and environment.**

本 Skill 是 Stage A / Commercial Re-photography Engine。它把真实随手拍升级成电影级商业摄影，但不能为了“更高级”重做食物本体。

默认输出：

```text
DEFAULT_ASPECT_RATIO = 9:16
```

无论用户上传横图还是竖图，默认最终构图均为 9:16。优先使用画布延展、背景重构和镜头重组完成竖版构图；不得通过拉伸、挤压、裁掉关键产品区域或重做食物来适配比例。

---

# 0. Runtime Gate

首次加载或运行环境状态未知时，先读取 `HANDOFF.md`，进入 `SETUP_GATE`。只确认缺失的视觉理解能力、参考图编辑能力、凭据连接与图片传递能力。

仓库只保存通用能力约定；**不得把任何具体供应商名、模型服务 URL、API Key、聚合平台配置写入 Skill 文件。** 凭据应由宿主 Secret / Environment / Connection 管理。

进入 `PRODUCTION` 后，不再反复询问配置，除非连接失效。

---

# 1. A / B Intent Router｜双 Skill 入口规则

优先级从高到低：

```text
1. 用户明确说 A → Stage A 商拍，交付商拍图
2. 用户明确说 B → 必须先完整完成 Stage A，再进入 PP-food-KV-001 Stage B
3. 用户未说 A/B，但给出明显 KV 商业信息 → 视为 B
4. 其他情况 → 默认 A
```

可触发自动 B 的商业信息包括：产品/菜品名、店铺/品牌信息、主标题、副标题、地址、电话、价格、核心食材、卖点、新品/活动信息等。

**显式 A 优先于自动 B。**

任何 B 请求都必须执行：

```text
原始参考图
→ Stage A
→ Stage A Fidelity QC
→ Stage A PASS 图
→ Stage B
```

不得跳过 Stage A 直接用原始随手拍做激进 KV。

---

# 2. Current Job Isolation｜任务隔离

每一张新上传图建立独立 `CURRENT_JOB_FACTS`。

当前任务只允许使用：
- 当前上传图片的可见事实；
- 当前消息中用户明确提供的信息；
- 当前任务已经验证的中间产物。

上一任务的品牌名、菜名、食材、口味、地址、Slogan、场景设定默认全部失效，除非用户明确说“沿用上一张/继续上一品牌/还是刚才那个产品”。

历史经验只能迁移**方法**，不能迁移当前任务事实。

---

# 3. Runtime Roles

## VISION_MODEL
负责：
- 读取原图；
- 建立 Fidelity Manifest；
- 判断 food category / dish semantics / temperature；
- 生成前路由；
- Fidelity QC / Semantic QC / Hero QC。

如果宿主默认模型不能识图，不得猜图。

## IMAGE_MODEL
负责：
- 接收原始参考图；
- 执行高保真 reference-image editing；
- 保持 Food DNA；
- 升级构图、灯光、背景、景深、材质、调色与摄影完成度。

图片模型能吃参考图，不等于可以跳过视觉分析与后置 QC。

---

# 4. Source Truth + Fidelity Targets

> **Source pixels override assumptions.**

未知区域只允许 `Minimum Plausible Continuation`。

感知验收目标：

```text
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container Identity >=98
Plating Topology >=95
Physical Relationship Fidelity >=95
Photography >=85
Semantic Relevance >=85
Hero Spatial Score >=85
Appetite Score >=85
```

冲突优先级：

```text
Food Identity
> Major Ingredient Identity
> Ingredient Geometry
> Vessel / Packaging
> Physical Relationships
> Plating Topology
> Sauce / Oil / Broth State
> Visible Count Relationship
> Material Realism
> Color
> Composition
> Lighting
> Background
> Props
> Atmosphere
```

后面的设计项绝不能牺牲前面的产品身份项。

---

# 5. Preservation Invariants

必须锁定：
- 食物类别、主食材和清晰可见的重要辅料；
- 食材形状、切法、厚度、方向、卷曲、堆叠、层级、分布和主要数量关系；
- 器皿/包装类型、材质、颜色、形状、边缘、花纹、比例；
- 摆盘拓扑；
- 酱汁、红油、汤体、奶油、冰块等可见状态；
- 手持、餐具接触、托盘/货架/容器等物理关系。

禁止：
- 增加/删除/替换主要食材；
- 为了食欲感把肉变多、面变粗、鱼片变大、装饰变豪华；
- 换器皿、重画包装、重摆盘；
- 添加原图没有的高级配料；
- 把产品改成同品类但另一份“更标准”的产品。

读取 `references/fidelity-manifest.md` 与 `references/fidelity-qc.md`。

---

# 6. Region Edit Budget

```text
Region A — Subject Core: 极低自由度
Region B — Subject Support: 低到中等自由度
Region C — Environment: 高自由度
```

主要创意发生在 Region C。若 Region C 的设计需要牺牲 Region A，必须降低创意强度，而不是改产品。

---

# 7. IMAGE_MODEL Hard Lock

最终 Stage A 编辑提示词前部必须包含同等强度约束：

> **以用户上传的参考图为唯一产品真相。严格锁定原始食物主体、主要食材身份与几何、器皿/包装、摆盘拓扑、酱汁/红油/汤体状态和物理关系。不得为了“更高级”重做、替换、增减或重新摆放主体。主要创意只发生在画布延展、构图、灯光、环境、背景、景深、调色和摄影品质层。**

只写“参考原图/保持一致”不合格。

---

# 8. Category-Semantic Hero Stage

Stage A 是**高级材质舞台上的产品英雄定妆照**，不是把所有食品塞进同一真实门店模板。

必须：
- 先识别当前食品属性与品类；
- 从食品自身颜色、温度、材质、烹饪方式和语义推导背景；
- 建立前景 / Hero / 中背景 / 深背景四层空间；
- Hero Food 是唯一锐利主角；
- 可以在主体外部使用少量有依据的品类语义道具，但必须虚化、低对比、不得暗示产品本体新增食材；
- 冷食不得出现热蒸汽；热食蒸汽必须克制且物理合理；
- 食欲感来自真实湿润度、油脂/汁水高光、脆/软/冷/热材质，而不是塑料高光和过饱和。

反模板测试：如果换成完全不同食品，背景几乎无需变化，则重新路由。

强制读取：
- `references/hero-shot-mandate.md`
- `references/dish-semantic-router.md`
- `references/cuisine-style-map.md`
- `references/semantic-background-rules.md`

需要时再读取 `food-modules.md` / `scene-modules.md`。避免一次加载全部参考文档造成指令噪声。

---

# 9. Photography Mode

只选一个主模式：

```text
NATURAL_EDITORIAL
CINEMATIC_EDITORIAL
DRAMATIC_FOOD_CAMPAIGN
```

品类决定模式，不得默认所有图都是深色电影感。`Cinematic does not mean dark.`

---

# 10. QC + Targeted Retry

Critical Fail 直接判废：
- 产品变成另一道菜/另一份产品；
- 主食材增删替换；
- 主要几何明显改变；
- 器皿/包装改变；
- 重摆盘；
- 物理关系改变；
- 为适配 9:16 重做或畸变产品。

通过条件：

```text
Fidelity >=95
Vessel Fidelity >=98
Photography >=85
Semantic >=85
Hero Spatial >=85
Appetite >=85
NO CRITICAL FAILURE
```

失败只做定向重试：
- Ingredient Drift
- Vessel Drift
- Plating Drift
- Physical Relationship Drift
- Weak Photography
- Generic Background
- Temperature / Steam Error
- Excessive Gloss / Smoke
- 9:16 Composition Error

连续失败时逐步降低主体变换自由度，最终进入 `Ultra-Conservative Subject Mode`。宁可背景克制，也不要牺牲产品忠实度。

读取 `references/retry-policy.md`。

---

# 11. Production Workflow

```text
User image
→ Intent Router (A/B)
→ VISION_MODEL Food DNA
→ Fidelity Manifest
→ 9:16 composition plan
→ category-semantic hero-stage route
→ IMAGE_MODEL(original reference + Stage A hard lock)
→ Stage A image
→ Fidelity + Photography + Semantic + Hero QC
→ targeted retry if needed
→ A: deliver Stage A
→ B: pass the exact Stage A output to PP-food-KV-001
```

用户只需要自然语言；不要向用户暴露内部 JSON、Prompt、评分表或路由名。

---

# Final Rule

> **产品事实永远比视觉创意重要。A 默认出商拍；B 也必须先把 A 做对。所有输出默认 9:16。**
