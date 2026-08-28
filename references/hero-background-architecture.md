# Hero Background Architecture Engine｜全品类世界级商拍背景空间引擎

本文件适用于 Stage A 所有食品品类。

目标：

> **背景首先是一套从当前食品本身推导出来的商业摄影空间建筑，其次才是道具布置。**

如果“高级感”主要来自几块布、夹子、杯子、陶罐、麦穗、香料碟或 bokeh，而背景本身没有空间结构，则不合格。

---

## 0. P0 Background Principle

```text
PRODUCT_DERIVED_STAGE > GENERIC_PREMIUM_STYLE
BACKGROUND_ARCHITECTURE > PROP_STYLING
ONE_BIG_STAGE_IDEA > MANY_DECORATIVE_OBJECTS
CATEGORY_MATERIAL_LOGIC > GENERIC_PREMIUM_PROPS
SPATIAL_MASSES > DECORATION
FOOD_HERO > EVERYTHING_ELSE
```

必须保证：
- 删除所有辅助道具后，背景仍然是完整、昂贵、专业的 Hero Stage；
- 材质、色彩、明暗和空间体块从当前食品属性推导；
- 背景不能读成真实门店，也不能读成“搭了几个道具的桌面静物”；
- 背景存在明确近 / 中 / 深空间体块，而不是一面虚墙；
- Stage A 从一开始就按严格 9:16 竖版设计，而不是先做横图再裁。

---

## 1. Product Derivation Matrix｜先从产品提取背景依据

每个任务必须至少从以下维度中提取 3 项真实可见证据：

```text
PRODUCT_DERIVATION_EVIDENCE >= 3
```

### A. Geometry
- 圆 / 环 / 长条 / 扭结 / 堆叠 / 扇形 / 球形 / 切片节奏；
- 重复单元的阵列节奏；
- 主体的横向/纵向趋势。

背景空间可回应这种几何节奏，但不得复制、移动或改变产品本身。

### B. Surface / Material
- 哑光 / 油润 / 透明 / 半透明 / 脆壳 / 湿润 / 奶油 / 玻璃 / 金属包装等。

背景应通过材质对比或呼应突出主体：
- 亮壳主体 → 更克制的吸光石材/烟熏金属；
- 透明饮品 → 玻璃/冷金属折射空间；
- 奶油甜品 → 柔和矿物石/细腻半哑光材质；
- 红油/卤味 → 深哑光吸光材质，让真实油光成为唯一高光英雄。

### C. Color
先锁食品真实主色，再提取：
- product primary color；
- secondary color；
- highlight color；
- low-saturation environmental support color。

环境必须保护产品真实颜色，不得把食物染进背景滤镜。

### D. Temperature / Process
- 冷、冰、清爽；
- 热、现烤、炭火、卤制、蒸煮；
- 手作、精致、粗犷、清鲜、浓郁。

通过光性、材质温感和空间密度表达，不靠假蒸汽、假火焰、假焦化。

### E. Category Temperament
不同品类必须改变空间密度、材质硬/软、反光/吸光、留白量、灯光方向和体块几何。

---

## 2. BACKGROUND_BIG_IDEA｜每张图只能有一个主空间概念

生成前必须写一句：

```text
BACKGROUND_BIG_IDEA = <one clear spatial/material/light concept>
```

要求：
- 不能只是“高级烘焙背景”“电影感餐桌”这种空话；
- 必须包含当前食品推导出的**空间结构 + 主材质 + 光性**；
- 必须能解释为什么换成另一品类后要重做；
- 必须服务当前 Hero，不允许背景自己成为第一主角。

例：

> 由圆环几何、焦糖/奶油双色关系和亮壳材质推导出的暖灰矿物石 + 烟熏烘焙金属阶梯舞台，后侧用弧形暗部与切光形成纵深。

这只是结构示例，不是固定模板。

---

## 3. BACKGROUND_ARCHITECTURE_PLAN｜每任务必建

```text
BACKGROUND_ARCHITECTURE_PLAN =
- background_big_idea:
- product_derivation_evidence: >=3
- category_material_logic:
- food-derived_color_logic:
- primary_material_planes: 2-3
- L1_near_spatial_mass:
- L3_mid_spatial_mass:
- L4_deep_spatial_masses: >=2 depth cues
- height_variation:
- depth_variation:
- occlusion_relationship:
- light_cut_and_shadow_architecture:
- reflective_vs_absorptive_material_relationship:
- negative_space_zone:
- props_required?: YES / NO
- if props: role = subordinate only
```

如果这个计划只有“放亚麻布 / 放夹子 / 放陶器 / 做虚化”，则 `BACKGROUND_ARCHITECTURE_PLAN = FAIL`。

---

## 4. Material Plane Logic｜材质平面不是道具清单

每张图选择 2–3 种主材质即可。

材质承担：
- 台面；
- 竖向/斜向背景平面；
- 台阶/基座；
- 半遮挡体块；
- 反射面；
- 吸光面；
- 光影落点。

不要让材质只以“小道具”形式存在。

如果需要 5–8 种材质才能显得高级，通常说明没有明确 Art Direction。

典型空间组合示例（只讲结构）：

```text
foreground stage lip
+ hero support plane
+ slightly raised / oblique L3 slab
+ offset deeper L4 plane
+ darker recessed L4 void
```

这些结构必须服务当前食品几何和材质，不得每类食品共用同一建筑结构。

---

## 5. Light Architecture｜光本身构成背景

背景高级感必须部分由光影结构建立：
- 主体光池只服务 Hero；
- L3 / L4 使用不同强度或方向的 falloff；
- 背景至少一个有意图的 light cut / shadow edge / grazing light；
- 反射材质与吸光材质形成对比；
- 深背景不允许全部均匀糊成一片。

正确：空间即使没有道具，也能靠光线切出层次。

错误：背景本身平，靠几盏 bokeh 灯和几件道具制造“氛围”。

---

## 6. Category-Derived Architecture｜食品属性决定空间

### A. 强几何 / 硬壳 / 烘烤类
例如面包、贝果、法棍、烧烤焦壳。
- 石材 / 烘焙金属 / 结构清晰体块；
- 更清晰边缘和台阶关系；
- 侧后光切面；
- 暗部退进；
- 结构化负空间。

### B. 柔软 / 奶油 / 甜品类
- 更柔和曲面或低反差平面；
- 奶油白/浅石/半透材质；
- 柔光切面；
- 轻盈负空间。

### C. 冷饮 / 水果 / 清鲜类
- 玻璃 / 半透 / 湿润石材 / 冷金属；
- 更明亮纵深；
- 冷暖反射差；
- 通透层次。

### D. 红油 / 卤味 / 浓郁肉类
- 深石 / 暗金属 / 吸光材质；
- 局部暖反射；
- 深暗部与高光锥；
- 避免整场红棕污染食物真实颜色。

### E. 包装零售
包装/货架身份优先，必要时使用 identity-critical retail exception，不强行转换成餐桌 Hero Stage。

---

## 7. 9:16 Vertical Hero Architecture｜竖版从一开始就是设计条件

```text
OUTPUT_ASPECT_RATIO_EXACT = 9:16
```

Stage A 背景必须从第一步就服务竖版，不允许先做横图再硬裁。

推荐空间逻辑：
- L1 在下方/侧下形成近相机入口；
- L2 Hero 占画面中下或中部主要视觉面积；
- L3 在主体后方斜向/纵向建立中景；
- L4 向画面上方继续退进并形成有设计的负空间；
- 上方负空间可服务 Stage B，但不能变成一堵无内容虚墙。

禁止：
- 横向舞台硬裁成竖图；
- 上半部只有模糊墙面；
- 为凑 9:16 把主体缩成底部小块；
- 输出“接近 9:16”但不是严格 9:16。

---

## 8. Prop Budget｜道具预算

```text
PROPS_OPTIONAL = TRUE
PROP_COUNT_TARGET = 0-3 subtle cues
PROP_VISUAL_PRIORITY < BACKGROUND_ARCHITECTURE
PROP_VISUAL_PRIORITY << FOOD_HERO
```

道具必须满足至少一个条件：
- 强品类身份；
- 强材料逻辑；
- 明确空间遮挡功能；
- 帮助建立尺度。

否则不放。

禁止默认组合：
- 亚麻布 + 黄铜夹子；
- 咖啡豆 + 手冲壶；
- 陶罐 + 木勺；
- 麦穗 + 面粉；
- 香料碟 + 蒜瓣。

这些只有当前食品与构图确实需要时才能出现。

---

## 9. Prop Independence Test｜去掉道具背景仍必须成立

内部强制测试：

> 如果删除所有布、夹子、杯子、陶器、麦穗、香料、器具等辅助小物，背景是否仍然像一个世界级商业摄影舞台？

如果否：

```text
PROP_DEPENDENCY_FOR_PREMIUM_LOOK = TRUE
→ FAIL
```

---

## 10. Four-Layer Spatial Evidence

### L1
真正靠近镜头的空间入口，可由台缘、材质片、直接支撑边缘或抽象空间体块形成；不强制必须有道具。

### L2
Hero 产品层，最锐、最强 light pool。

### L3
明确后退的材质平面/体块，与 L2 有可见距离差。

### L4
至少两个更深的后退线索，例如：第二材质平面、凹入暗区、远处结构体块、独立 light falloff、不同焦外层级。

单一墙面、单一渐变、统一 bokeh 都不算。

---

## 11. Background Critical Failures

以下任一项直接背景 FAIL：
1. 删除道具后只剩普通店内/木柜/虚墙；
2. 背景主要由道具而不是空间结构构成；
3. 材质只作为小物件存在，没有形成平面/体块；
4. L3 / L4 缺少真正前后距离；
5. 全背景同一暖棕/黑金模板；
6. 换成完全不同食品，背景几乎不需要改；
7. 背景强于产品；
8. 背景为了高级感改变产品真实颜色、表面或熟度；
9. 真实经营场所结构无身份必要却被保留；
10. 画面仍首先读成“店里拍的产品”，而不是“商业摄影棚 Hero”；
11. `PRODUCT_DERIVATION_EVIDENCE < 3`；
12. 没有明确 `BACKGROUND_BIG_IDEA`；
13. 非严格 9:16 最终画布；
14. 上半部大量无设计的模糊空区。

---

## 12. Targeted Retry

如果 Food Fidelity 已 PASS，但背景不够高级：

> Preserve the exact current food, source surface state, count, arrangement, vessel/direct support and all physical relationships. Redesign ONLY Region C environment. First derive at least three visual facts from the current food (geometry, color, material, temperature/process, category temperament) and define one clear BACKGROUND_BIG_IDEA. Build a category-native premium material architecture using only 2–3 primary material planes, explicit near/mid/deep spatial masses, height/depth variation, controlled occlusion, reflective-versus-absorptive material contrast, deliberate light cuts and at least two deep recession cues. Props are optional and subordinate. The background must remain world-class even if all props are removed. Compose natively for exact vertical 9:16; do not create a horizontal set and crop it.

---

## 13. Acceptance

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

最终问题：

> **即使完全不放任何小道具，单靠产品、空间、材质、光和景深，这张图是否已经是一张世界级美食 Hero 商拍？**

如果不是明确“是” → Background Architecture FAIL。