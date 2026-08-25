---
name: universal-food-commercial-photography
description: Use when editing a user-provided food photo into premium commercial or cinematic food photography while preserving the exact food identity, visible ingredients, geometry, plating, vessel, packaging and physical relationships at high fidelity, and designing a dish-specific semantic background from explicit or inferred dish information.
version: 5.0.0
---

# Universal Food Commercial Photography V5

## Purpose

把用户提供的真实美食随手拍，升级成高级商业摄影 / 电影级美食摄影，同时保持原食物身份、主要食材、食材几何、摆盘、器皿、包装与真实物理关系高度稳定。

V5 在 V4 的 95% 高保真基础上新增：

> **菜品语义驱动背景设计。**

核心命令：

> **Preserve the product. Upgrade the photography. Design the environment from the dish semantics.**
>
> **保留产品本身，升级摄影品质；根据具体菜品语义设计环境。**

## 最终成功条件

最终画面必须同时满足：

1. **HIGH FIDELITY** — 一眼仍然是原来那一份具体食物；
2. **HIGH PHOTOGRAPHY UPGRADE** — 摄影品质明显达到商业广告级；
3. **HIGH SEMANTIC RELEVANCE** — 背景、色彩、道具和氛围与具体菜品有关，而不是套统一模板。

如果结果很漂亮但食物被重做，失败。

如果食物很保真但摄影几乎没升级，不完整。

如果食物和摄影都很好，但“青花椒酸菜鱼、寿司、蛋糕、牛肉面”都使用同一套暗木桌暖黄灯背景，也不通过 V5。

---

# 1. Source Truth / 源图事实优先

源图中的可见事实高于：

- 菜品通常会有什么；
- 菜系刻板印象；
- 高级餐饮惯例；
- 模型审美偏好；
- 为了好看而追加的食材或器皿。

**Source pixels override assumptions.**

未知或不可见区域不是自由创作许可。

缺失区域只能使用：

> **Minimum Plausible Continuation / 最小合理延展。**

---

# 2. 用户提供的菜品信息优先

在编辑前检查用户是否明确提供：

```text
dish_name
cuisine_type
flavor_profile
main_highlights
desired_mood
```

如果用户明确提供菜名或菜系，这些信息是**语义背景设计的最高优先级事实**。

例如：

> 用户说“这是青花椒酸菜鱼”。

则系统必须围绕：

- 青花椒 / 藤椒
- 鲜麻
- 酸香
- 川味
- 热汤

设计背景与摄影氛围，而不能继续按普通热汤或通用黑金餐饮背景处理。

用户菜名只影响环境设计，不允许用来改变源图中的菜品结构。

---

# 3. 用户没有提供菜名时

调用 `references/dish-semantic-router.md` 进行内部推断。

推断字段至少包括：

```text
probable_dish_name
dish_confidence
cuisine_type
flavor_profile
primary_ingredients
cooking_method
temperature_state
dish_mood_keywords
semantic_route
```

置信度处理：

- `>= 0.85`：允许采用具体菜品级语义背景；
- `0.60–0.84`：只采用品类级语义背景；
- `< 0.60`：采用保守的类别级商业摄影环境。

自动猜菜只用于：

- 背景
- 色彩
- 道具
- 环境
- 摄影情绪

不得用于添加或删除菜品内容。

---

# 4. Perceptual Fidelity Targets / 高保真目标

以下百分比是感知验收目标，不是像素级数学保证：

- Food identity fidelity: **>=95%**
- Ingredient geometry fidelity: **>=95%**
- Vessel/container identity fidelity: **>=98%**
- Plating fidelity: **>=95%**
- Physical relationship fidelity: **>=95%**

## Preservation Priority

冲突时按以下顺序：

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

# 5. Preservation Invariants / 主体不变量

## Food Identity

保持：

- 食品类别；
- 主食材；
- 清晰可见的重要辅料；
- 烹饪状态；
- 份量感。

## Ingredient Geometry

保持：

- 形状；
- 切法；
- 厚度；
- 宽度；
- 长度关系；
- 卷曲；
- 朝向；
- 堆叠；
- 分层；
- 分布；
- 主要数量关系。

不得因为“更高级”让鱼片更大、肉更多、面更粗、虾更显眼。

## Vessel / Package

器皿、包装属于产品身份。

尽量 98% 以上保持：

- 类型；
- 材质；
- 颜色；
- 形状；
- 深浅；
- 边缘；
- 表面纹理；
- 花纹；
- 相对比例。

禁止：白瓷碗换黑陶、塑料杯换玻璃杯、纸盒换瓷盘、原包装重新设计。

## Plating Topology

保持：

- 上下关系；
- 中央与边缘分布；
- 汤汁 / 酱汁覆盖；
- 配料集中位置；
- 整体堆叠逻辑。

禁止为了美观重新摆盘。

## Physical Relationships

保持：

- 手持关系；
- 筷子 / 刀叉 / 勺子接触；
- 包装关系；
- 货架关系；
- 展示柜关系；
- 托盘 / 桌面 / 柜台接触关系。

---

# 6. Region Edit Budget / 区域修改预算

## Region A — Subject Core

包括：食物、主要食材、器皿/包装、食物与手/餐具接触处。

修改预算：**极低**。

只允许主要通过：

- 曝光；
- 白平衡；
- 光线融合；
- 已有材质显现；
- 受控高光；
- 不改变身份的微小清理。

## Region B — Subject Support

包括：手、餐具、托盘、主体附近桌面、直接货架区域。

修改预算：**低到中等**。

## Region C — Environment

包括：背景、远桌面、墙面、无关杂物、环境灯、远处人群、弱化道具。

修改预算：**高**。

V5 的主要创意发生在 Region C。

---

# 7. Minimum Necessary Subject Change

主体只允许进行获得专业摄影效果所必需的最小修改。

正确：增强已有汤汁反射。

错误：把清汤改成红油。

正确：让已有鱼片纹理更清晰。

错误：重新生成更厚更规则的鱼片。

正确：增强已有炸物酥脆纹理。

错误：重新做一个更大更金黄的炸物。

---

# 8. Food Material Routing

读取 `references/food-modules.md`。

每张图通常只加载：

- 1 个 primary food module；
- 0–2 个 secondary material modules。

不要加载全部模块。

例：

- 青花椒酸菜鱼 -> SEAFOOD + HOT_SOUP；
- 牛肉汤面 -> NOODLES + HOT_SOUP + MEAT；
- 炸鸡 -> FRIED + MEAT；
- 草莓蛋糕 -> DESSERT/CAKE + FRUIT；
- 手持冰咖啡 -> COLD_DRINK。

---

# 9. Scene Routing

读取 `references/scene-modules.md`。

只选择一个主场景：

- TABLETOP
- HANDHELD
- RESTAURANT
- CAFE
- RETAIL_SHELF
- DISPLAY_CASE
- STREET_FOOD
- CLEAN_COMMERCIAL_STUDIO

场景路由解决“食物在哪里”。

菜品语义路由解决“这个环境应该是什么气质”。

两者不要混淆。

---

# 10. Dish Semantic Routing / V5 核心

读取：

- `references/dish-semantic-router.md`
- `references/cuisine-style-map.md`
- `references/semantic-background-rules.md`

V5 采用：

> **Scene Context × Dish Semantics × Food Material × Photography Mode**

共同决定最终背景。

例如：

```text
青花椒酸菜鱼
= RESTAURANT/TABLETOP
× SICHUAN_FRESH_PEPPER
× SEAFOOD + HOT_SOUP
× CINEMATIC_EDITORIAL
```

得到的背景应具有：

- 鲜麻川味语义；
- 藤椒绿 / 酸菜黄绿 / 汤汁暖金的环境呼应；
- 高级川菜馆或现代川味餐饮气质；
- 少量相关失焦辅助意象；
- 克制热气；
- 不改变鱼片、青花椒、汤、器皿和摆盘。

---

# 11. Anti-Template Background Rule

禁止将所有热食统一处理成：

- dark wood
- warm amber
- generic ceramic props
- heavy bokeh
- dark restaurant
- excessive steam

**Cinematic does not mean dark.**

不同语义的菜品不得使用完全同构的背景：

- 青花椒酸菜鱼 ≠ 牛肉面
- 牛肉面 ≠ 草莓蛋糕
- 草莓蛋糕 ≠ 寿司
- 寿司 ≠ 夜市烧烤

每次生成前问：

> 如果把主体换成完全不同的菜，这个背景仍然毫无变化也能用吗？

如果答案是“是”，背景过于通用，重新设计。

---

# 12. Semantic Props Boundary

背景允许使用少量与菜品相关的环境提示，例如：

- 青花椒鲜麻类：远处失焦青花椒意象、酸菜/腌菜陶罐、小料碟；
- 烧烤：摊位、烤具、暖灯、炭火环境；
- 日料：极简原木/石材、少量小碟；
- 甜点：咖啡馆、甜品店环境；
- 包装食品：原货架与零售环境。

但这些道具必须：

- 少；
- 弱；
- 失焦；
- 不抢主体；
- 不进入主菜；
- 不让人误以为新增食材。

---

# 13. Semantic Color Engine

色彩优先级：

1. 真实食物颜色；
2. 用户明确菜品/品牌信息；
3. 风味/菜系语义；
4. 环境协调色。

语义颜色只能用于支持背景，不能为了匹配主题而重新染色主食材。

例如青花椒酸菜鱼可使用：

- 藤椒绿；
- 酸菜黄绿；
- 汤汁暖金；
- 深灰 / 克制深木；
- 少量暖铜环境光。

但不得把鱼肉染绿、汤变荧光黄或制造赛博霓虹。

---

# 14. Photography Modes V5

选择一个：

## NATURAL_EDITORIAL

适合：粤式清鲜、轻食、日料、蛋糕、烘焙、咖啡、水果、沙拉。

## CINEMATIC_EDITORIAL

默认。适合多数中餐、堂食、热菜、主食。

## DRAMATIC_FOOD_CAMPAIGN

适合：火锅、烧烤、红油麻辣、夜市、强刺激热菜。

主体保真规则在任何模式下都不能放松。

---

# 15. Physical Realism

保持真实：

- gravity
- liquid behavior
- steam origin
- smoke origin
- condensation
- contact shadows
- environmental reflections
- utensil contact
- hand pressure/contact
- perspective
- scale

热食才允许克制蒸汽；冷饮禁止热气；烧烤只有物理合理时才允许轻烟。

飞舞食材默认禁用。

---

# 16. Execution Workflow

固定执行顺序：

```text
1. Read source image
2. Read explicit user dish information
3. Build Fidelity Manifest
4. Resolve dish semantics / confidence
5. Select food module(s)
6. Select one scene module
7. Select semantic route
8. Select photography mode
9. Build semantic background direction
10. Apply low edit budget to subject, high edit budget to environment
11. Assemble `references/execution-template.md`
12. Generate / edit
13. Run Fidelity QC
14. Run Semantic QC
15. Targeted retry when required
```

---

# 17. Quality Control

先运行 `references/fidelity-qc.md`。

再运行 `references/semantic-qc.md`。

最终通过条件：

```text
Fidelity Score >= 95
Photography Score >= 85
Semantic Score >= 85
No Fidelity Critical Failure
No Semantic Critical Failure
```

语义背景再好，只要食材、器皿、摆盘发生明显漂移，仍然失败。

主体再保真，只要背景仍是明显无差别模板，也不算 V5 完成。

失败时使用 `references/retry-policy.md` 与 `references/semantic-qc.md` 中的定向重试，不要随机重生成。

---

# 18. Final Command

> **The source food is the real product, not creative raw material.**
>
> **Preserve the product physically.**
>
> **Use explicit or inferred dish semantics to design the environment.**
>
> **Communicate flavor through light, color, environment and restrained context — never by inventing ingredients.**
>
> **Change the photography, not the product.**
