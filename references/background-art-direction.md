# Background Art Direction｜全品类世界级 Hero 背景设计总则

本文件适用于 Stage A 的**所有食品品类**。

目标不是“给食物换一个高级背景”，而是：

> **从当前食品本身推导出一个不可替换的商业摄影舞台，让同一份真实产品获得世界级 Hero 姿态。**

本文件只控制 Region C 环境、空间、材质、光影和负空间，不授权任何产品结构或表面状态改动。

---

## 0. P0 Principle

```text
PRODUCT_DERIVED_STAGE > GENERIC_PREMIUM_STYLE
BACKGROUND_ARCHITECTURE > PROP_STYLING
ONE_BIG_STAGE_IDEA > MANY_DECORATIVE_OBJECTS
```

高级感首先来自：
- 空间体块；
- 材质平面；
- 前后遮挡；
- 高低落差；
- 光影切面；
- 反射/吸光差异；
- 连续景深；
- 产品与环境的色彩关系。

不来自：
- 亚麻布；
- 黄铜夹子；
- 陶罐；
- 麦穗；
- 咖啡豆；
- 香料碟；
- 木板；
- 石块；
- bokeh；
- “暗一点、暖一点”。

这些只能是可选辅助元素，不能承担“高级感”的主体责任。

---

## 1. Product Derivation Matrix｜先从产品提取背景依据

每个任务必须至少从以下维度中提取 3 项可见证据：

```text
PRODUCT_DERIVATION_EVIDENCE >= 3
```

### A. Geometry
- 圆 / 环 / 长条 / 扭结 / 堆叠 / 扇形 / 球形 / 切片节奏；
- 重复单元的阵列节奏；
- 主体的横向/纵向趋势。

背景空间可以回应这种几何节奏，但不得复制或改变产品本身。

### B. Surface / Material
- 哑光 / 油润 / 透明 / 半透明 / 脆壳 / 湿润 / 奶油 / 金属包装 / 玻璃杯壁等。

背景应通过“对比或呼应材质”突出主体，例如：
- 亮壳主体 → 更克制的吸光石材/烟熏金属；
- 透明饮品 → 玻璃/冷金属的折射空间；
- 奶油甜品 → 柔和矿物石/细腻织物；
- 红油卤味 → 深哑光吸光材质，让真实油光成为唯一高光英雄。

### C. Color
提取：
- 食物主色；
- 第二主色；
- 高光色；
- 低饱和环境协调色。

环境必须保护真实食物颜色，不得把产品染进背景滤镜。

### D. Temperature / Process
- 冷、冰、清爽；
- 热、现烤、炭火、卤制、蒸煮；
- 手作、精致、粗犷、清鲜、浓郁。

背景通过光性、材质温感与空间密度表达，不靠假蒸汽/假火焰。

### E. Category / Brand Temperament
- 烘焙：烘焙工艺、壳/内瓤、烤盘记忆；
- 咖啡：液体、玻璃/陶瓷、反射与生活方式；
- 卤味：浓郁、油润、熟食陈列但非真实店面；
- 清鲜：轻、透、留白；
- 火锅/烧烤：热、重、金属/石材；
- 甜品：细腻、轻盈、曲面与柔材质。

---

## 2. BACKGROUND_BIG_IDEA｜每张图只能有一个主空间概念

生成前必须写一句：

```text
BACKGROUND_BIG_IDEA = <one clear spatial/material concept>
```

要求：
- 不是“高级烘焙背景”“电影感餐桌”这种空话；
- 必须包含当前食品推导出的**空间结构 + 主材质 + 光性**；
- 必须能解释为什么换成另一品类就要重做。

示例结构（不是固定模板）：

> “由当前圆环几何和焦糖/奶油双色关系推导出的暖灰矿物石 + 烟熏烘焙金属阶梯舞台，后侧以弧形暗部和切光形成纵深。”

> “由透明冷饮和冰感推导出的低饱和玻璃体块 + 拉丝冷金属层级，利用折射和冷白边缘光建立清凉纵深。”

---

## 3. Background Architecture Plan｜必须先搭空间，再考虑道具

每张 Stage A 必须建立：

```text
BACKGROUND_ARCHITECTURE_PLAN
- primary_material_planes: 2-3
- L1_near_camera_mass
- L3_mid_depth_mass
- L4_deep_recession_planes >= 2
- height_difference
- overlap / occlusion logic
- light_cut / shadow_geometry
- reflection_vs_absorption_relationship
- negative_space_zone
- props: OPTIONAL
```

### Primary Materials
主材质最多 2–3 种。

如果需要 5–8 种材质才能“显得高级”，通常说明没有明确 Art Direction。

### Spatial Masses
背景必须有体块，而不是一张墙纸：
- 高低台面；
- 前后石材/金属体块；
- 半遮挡边缘；
- 明暗切面；
- 前景框景；
- 深处继续后退的平面。

### Lighting Architecture
灯光不仅“照亮食物”，还要参与背景空间设计：
- 主体光池；
- 背景局部切光；
- 深处 light falloff；
- 某些材质反光、某些材质吸光；
- 明暗关系形成空间路径。

---

## 4. Prop Independence Test｜去掉道具背景仍必须成立

内部强制测试：

> 如果删除亚麻布、夹子、陶罐、麦穗、咖啡豆、香料、器具等所有辅助小物，背景是否仍然像一个世界级商业摄影舞台？

如果答案是“否”：

```text
PROP_DEPENDENCY_FOR_PREMIUM_LOOK = TRUE
→ FAIL
```

世界级舞台可以完全没有道具。

道具只在以下情况下加入：
- 能明确增强当前食品身份；
- 不会被误读为新增食材；
- 不抢 Hero；
- 不重复上一品类皮肤；
- 删除后画面仍然成立。

---

## 5. Category-Native Spatial Language｜不同食品必须长得不一样

背景不是“换色模板”。不同品类应改变：
- 空间密度；
- 材质硬/软；
- 反光/吸光；
- 前后景比例；
- 留白量；
- 灯光方向与硬度；
- 体块几何。

例如：

### Bread / Bakery
优先：矿物石、烘焙金属、纸张、原直接木托盘。
空间应更像**烘焙工艺的雕塑舞台**，而不是咖啡馆静物桌。

### Braised / Sauced Food
优先：深哑光石、深色金属、克制木/陶。
空间要让真实酱色/油光成为最亮材质，不用满屏香料道具。

### Dessert
优先：浅矿物石、细腻半哑光曲面、柔材质。
空间更轻、留白更多、阴影更柔。

### Cold Drink
优先：玻璃、冷金属、透明/半透明体块。
空间靠折射、冷边光和纵深表达，不靠水果堆满画面。

---

## 6. 9:16 Vertical Hero Architecture

Stage A 默认最终交付必须是严格 9:16 竖版。

背景设计必须从一开始服务竖版，而不是先做横图再裁。

推荐竖版空间逻辑：
- L1 在下方/侧下形成近相机入口；
- L2 Hero 占画面中下或中部主要视觉面积；
- L3 在主体后方斜向/纵向建立中景；
- L4 向画面上方继续退进并形成干净负空间；
- 上方负空间可供 Stage B 但不能变成空墙。

禁止：
- 横向舞台硬裁成竖图；
- 上半部只有一堵虚墙；
- 为凑 9:16 把主体缩成底部小块。

---

## 7. World-Class Background Failures

以下任一项存在，背景不得通过：

1. 画面首先读成“店里摆拍/柜台照片”；
2. 只加布、夹子、陶罐、麦穗等静物道具；
3. 一堵暖棕/灰色虚墙充当 L4；
4. 材质与当前食品没有至少 3 项推导关系；
5. 换成另一食品后背景几乎无需变化；
6. 背景比产品更花、更亮、更有戏；
7. 上半部大量无设计的模糊空区；
8. 材质太多、道具太多、没有 One Big Idea；
9. 非 9:16 最终画布；
10. 为了背景高级而改变食品表面状态、结构或摆盘。

---

## 8. Acceptance

必须同时满足：

```text
BACKGROUND_BIG_IDEA = PASS
PRODUCT_DERIVATION_EVIDENCE >= 3
BACKGROUND_ARCHITECTURE_PLAN = PASS
PRIMARY_STAGE_MATERIALS <= 3
PROP_DEPENDENCY_FOR_PREMIUM_LOOK = FALSE
ARCHITECTURAL_OR_SCULPTURAL_DEPTH = TRUE
FOUR_LAYER_DEPTH = PASS
OUTPUT_ASPECT_RATIO_EXACT = 9:16
PRODUCT_REMAINS_HERO = TRUE
```

目标：

> **即使完全不放任何小道具，单靠产品、空间、材质、光和景深，这张图也已经是一张世界级美食 Hero 商拍。**