---
name: universal-food-commercial-photography
description: Use when editing a user-provided food photo into premium commercial or cinematic food photography while preserving exact food identity, ingredients, geometry, plating, vessel, packaging and physical relationships at high fidelity.
version: 5.2.1
---

# Universal Food Commercial Photography V5.2.1

V5.2.1 hotfix: 图像模型在「真实场所」语境下自发补足招牌字 / 人物污染 KV 排版。在 hero-shot-mandate.md §9 增加强负面清单与构图规避策略。

## Core Principle

> **Preserve the product. Upgrade the photography. Design the environment from the dish semantics.**

把用户真实美食随手拍升级成电影级 / 商业广告级摄影，同时保持原食物、主要食材、食材几何、摆盘、器皿、包装和物理关系高度稳定。

---

# 0. FIRST-RUN SETUP GATE｜首次安装先配置运行环境

首次安装、首次加载，或当前运行环境是否就绪未知时，**禁止直接进入生产**。

必须先读取根目录 `HANDOFF.md`，进入：

```text
RUNTIME_STATE = SETUP_GATE
```

向用户确认以下配置，只询问缺失项：

1. `VISION_MODEL`：用于识图、Food DNA/Fidelity Manifest、路由和生成后 QC；
2. `IMAGE_MODEL`：用于参考图编辑 / image-to-image / 最终商拍生成；
3. `API_BASE_URL`：模型服务或聚合平台地址；
4. API Key/Credential 已写入 Secret / Environment / Connection，而不是明文长期放在普通对话；
5. IMAGE_MODEL 确实支持上传参考图；
6. 生成结果可以继续被智能体读取/传递。

如果宿主默认模型没有视觉能力，**不得自行猜测用户图片内容**。必须调用已配置的 `VISION_MODEL`。

配置完成后必须告诉用户：

> **PP-food-001 已准备就绪。回复“启动”进入生产模式。**

状态切换：

```text
SETUP_GATE
→ READY_WAITING_FOR_START
→ 用户回复“启动”
→ PRODUCTION
```

进入 `PRODUCTION` 后，用户只需自然语言交流，不再反复询问模型配置，除非连接失效。

---

# 1. Runtime Model Roles｜模型角色分工

## VISION_MODEL

负责：
- 读取用户上传图片；
- 建立 Fidelity Manifest；
- 判断 food category / scene / dish semantics；
- 路由置信度；
- Fidelity QC；
- Semantic QC。

## IMAGE_MODEL

负责：
- 接收用户原始参考图；
- 高保真参考图编辑；
- 锁食物、食材、器皿、包装、摆盘与物理关系；
- 升级灯光、背景、环境、景深、材质和调色。

**会根据参考图出图 ≠ 能替代完整视觉分析与 QC。**

---

# 2. Source Truth｜源图事实优先

源图中的可见事实高于：
- 菜品惯例；
- 模型审美偏好；
- 高级餐饮刻板印象；
- 为了“更好看”而追加的食材或器皿。

> **Source pixels override assumptions.**

未知或不可见区域只允许 `Minimum Plausible Continuation / 最小合理延展`。

---

# 3. Perceptual Fidelity Targets

以下为感知验收目标，不是像素数学保证：

- Food identity fidelity: **>=95%**
- Ingredient geometry fidelity: **>=95%**
- Vessel/container identity fidelity: **>=98%**
- Plating fidelity: **>=95%**
- Physical relationship fidelity: **>=95%**

冲突时优先级：

1. Food identity
2. Major ingredient identity
3. Ingredient geometry
4. Vessel / packaging identity
5. Physical relationships
6. Plating topology
7. Material realism
8. Food color
9. Composition
10. Lighting
11. Semantic background
12. Props
13. Atmosphere

绝不能为了 9–13 牺牲 1–6。

---

# 4. Preservation Invariants

必须锁定：
- 食物类别和主食材；
- 清晰可见的重要辅料；
- 烹饪状态和份量感；
- 食材形状、切法、厚度、朝向、堆叠、分布与主要数量关系；
- 器皿/包装类型、材质、颜色、形状、花纹与比例；
- 摆盘拓扑；
- 手持、筷子/刀叉/勺子接触、货架、托盘、展示柜等物理关系。

禁止：
- 为了高级感让鱼片更大、肉更多、面更粗、虾更显眼；
- 白瓷换黑陶、塑料杯换玻璃杯、原包装重设计；
- 为了好看重摆盘；
- 添加不存在的高级配料。

---

# 5. Region Edit Budget

## Region A — Subject Core
食物、主要食材、器皿/包装、直接接触关系。

修改预算：**极低**。

## Region B — Subject Support
手、餐具、托盘、近桌面、直接货架区域。

修改预算：**低到中等**。

## Region C — Environment
背景、远桌面、墙面、无关杂物、环境灯、远处人群和弱化道具。

修改预算：**高**。

主要创意发生在 Region C。

---

# 6. Image Edit Prompt Hard Lock｜图片提示词首段硬锁

每次调用 IMAGE_MODEL 时，最终编辑指令前部必须明确包含同等强度的约束：

> **以用户上传的参考图为唯一产品真相。严格锁定原始食物主体、主要食材身份与几何、器皿/包装、摆盘拓扑和物理关系。不得为了“更高级”重做、替换、增减或重新摆放主体食材。主要创意只发生在灯光、环境、背景、景深、调色和摄影品质层。**

不能只写“参考原图”或“保持一致”而没有具体锁定对象。

---

# 7. User Dish Information Priority

如果用户明确提供：

```text
dish_name
cuisine_type
flavor_profile
main_highlights
desired_mood
```

这些信息优先用于**背景语义设计**，但不允许据此改变源图食材结构。

如果用户没提供菜名，读取：
- `references/dish-semantic-router.md`
- `references/cuisine-style-map.md`
- `references/semantic-background-rules.md`

置信度：
- `>=0.85`：可采用具体菜品级语义背景；
- `0.60–0.84`：只采用品类级语义背景；
- `<0.60`：保守类别级商业环境。

自动猜菜只服务于背景、色彩、道具、环境和摄影情绪，不用于增删食材。

---

# 8. Food / Scene Routing

读取：
- `references/food-modules.md`
- `references/scene-modules.md`

通常只加载：
- 1 个 primary food/material module；
- 0–2 个 secondary modules；
- 1 个 primary scene module。

场景解决“食物在哪里”；菜品语义解决“这个环境应该是什么气质”。

---

# 9. Photography Modes

选择一个：

### NATURAL_EDITORIAL
适合：清鲜、轻食、日料、蛋糕、烘焙、咖啡、水果、沙拉。

### CINEMATIC_EDITORIAL
默认。适合多数中餐、堂食、热菜、主食。

### DRAMATIC_FOOD_CAMPAIGN
适合：火锅、烧烤、红油麻辣、夜市和强刺激热菜。

**Cinematic does not mean dark.** 主体保真在任何模式下都不能放松。

---

# 10. Anti-Template & Hero-Grade Spatial Background｜背景硬规则

## 10.1 反模板（原有规则，继续生效）

禁止所有热食统一使用：
- dark wood
- warm amber
- generic ceramic props
- heavy bokeh
- dark restaurant
- excessive steam

不同菜品必须有真实语义差异。

每次生成前问：

> 如果把主体换成完全不同的菜，这个背景仍毫无变化也能用吗？

如果答案是“是”，背景过于模板化，应重做。

## 10.2 Hero Shot Mandate｜英雄定妆照硬规则（V5.2 起新增强制项）

读取并强制执行 `references/hero-shot-mandate.md`。要点：

1. **禁止平背景**——背景必须是「空间舞台」而非「背景板」，画面必须读出四层景深（前景 / 中景光池 / 中后景语义道具 / 远景纵深），缺层即 Semantic Critical Failure；
2. **空间感按食材属性与调性设计**——面食在面馆、蛋糕在明亮展台，环境结构由这道菜的身份推导；
3. **必须有现场感**——环境要像真实运营中的制作/出品现场，核心作料围铺在盘外台面并虚化，不喧宾夺主；
4. **氛围与食材调性匹配**——冷食冷调零热气、热食暖调允许克制蒸汽，温度错配即失败；
5. **世界级英雄定妆照调性**——主体是全场唯一英雄：光池聚焦、轮廓光雕刻、低机位纪念碑感；
6. **工业级商拍质量**——每一张都达到商业投放标准，不是抽卡式偶发好图；
7. **所有品类强制遵循**——品类只改变语境映射，不改变空间与英雄标准，无豁免类别。

验收新增：

```text
Hero Spatial Score >= 85
```

平背景 / 两层平面感 / 语境与食物无关 / 作料抢主体 / 温度错配，任一出现按 `hero-shot-mandate.md` §7 的定向方向重试。

---

# 11. Physical Realism

保持：
- gravity
- liquid behavior
- steam/smoke origin
- condensation
- contact shadows
- environmental reflections
- utensil/hand contact
- perspective
- scale

热食才允许克制蒸汽；冷饮禁止热气；飞舞食材默认禁用。

---

# 12. Production Workflow

在 `PRODUCTION` 状态固定执行：

```text
1. User uploads source image
2. VISION_MODEL reads the source image
3. Read explicit user dish information
4. Build Fidelity Manifest
5. Resolve dish semantics / confidence
6. Select food module(s)
7. Select one scene module
8. Select semantic route
9. Select photography mode
10. Build hero-grade spatial background direction（执行 hero-shot-mandate.md 四层空间 + 品类语境映射）
11. Assemble references/execution-template.md
12. IMAGE_MODEL receives original reference image + edit instruction
13. Generate / edit
14. VISION_MODEL runs Fidelity QC
15. VISION_MODEL runs Semantic QC
16. Targeted retry when required
```

如果宿主智能体无法把用户图片传给 IMAGE_MODEL，或无法让 VISION_MODEL读取图片，不得宣称生产环境就绪。

---

# 13. Quality Control

读取：
- `references/fidelity-qc.md`
- `references/semantic-qc.md`
- `references/retry-policy.md`

最终通过条件：

```text
Fidelity Score >= 95
Photography Score >= 85
Semantic Score >= 85
Hero Spatial Score >= 85
No Fidelity Critical Failure
No Semantic Critical Failure
No Flat-Background Failure（平背景/空间层次缺失）
```

失败必须按具体错误定向重试，不要随机重抽。

---

# 14. PP-food-KV-001 Integration

如果同时安装 `PP-food-KV-001`：

- 本 Skill = **Stage A / High-Fidelity Commercial Re-photography Engine**；
- KV Skill = Stage B；
- **Stage A 输出必须作为 Stage B 的输入参考图**；
- 一次完成 VISION_MODEL / IMAGE_MODEL / API 配置即可供两个 Skill 共用。

不要绕过 Stage A 直接从随手拍做激进 KV，除非用户明确接受更低的保真稳定性。

---

# Final Command

> **The source food is the real product, not creative raw material.**
>
> **Change the photography, not the product.**
>
> **If runtime readiness is unknown: read HANDOFF.md, configure first, wait for “启动”, then produce.**
