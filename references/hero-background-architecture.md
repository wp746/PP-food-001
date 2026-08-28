# Hero Background Architecture Engine｜全品类世界级商拍背景空间引擎

本文件适用于 Stage A 所有食品品类。

目标：

> **背景首先是一套为当前食品专门设计的商业摄影空间建筑，其次才是道具布置。**

如果“高级感”主要来自几块布、夹子、杯子、陶罐、麦穗、香料碟或 bokeh，而背景本身没有空间结构，则不合格。

---

## 0. P0 Background Principle

```text
BACKGROUND_ARCHITECTURE > PROP_STYLING
CATEGORY_MATERIAL_LOGIC > GENERIC_PREMIUM_PROPS
SPATIAL_MASSES > DECORATION
FOOD_HERO > EVERYTHING_ELSE
```

必须保证：

- 删除所有辅助道具后，背景仍然是完整、昂贵、专业的 Hero Stage；
- 材质、色彩、明暗和空间体块从当前食品属性推导；
- 背景不能读成真实门店，也不能读成“搭了几个道具的桌面静物”；
- 背景存在明确近 / 中 / 深空间体块，而不是一面虚墙。

---

## 1. BACKGROUND_ARCHITECTURE_PLAN｜每任务必建

生成前必须建立：

```text
BACKGROUND_ARCHITECTURE_PLAN =
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

## 2. Material Plane Logic｜材质平面不是道具清单

每张图选择 2–3 种主材质即可。

材质承担的是：
- 台面；
- 竖向/斜向背景平面；
- 台阶/基座；
- 半遮挡体块；
- 反射面；
- 吸光面；
- 光影落点。

不要让材质只以“小道具”形式存在。

典型空间组合示例（只讲结构，不是固定模板）：

```text
L2 support plane
+ slightly raised L3 slab / panel
+ offset deeper L4 plane
+ a darker recessed L4 void
```

或者：

```text
foreground stage lip
+ hero platform
+ oblique mid-plane
+ layered deep planes with controlled light falloff
```

这些结构必须服务当前食品几何和材质，不得每类食物共用同一建筑结构。

---

## 3. Category-Derived Architecture｜食品属性决定空间

设计背景时先看食品本身：

### A. 强几何 / 硬壳 / 烘烤类
例如面包、贝果、法棍、烧烤焦壳。

空间可使用：
- 石材 / 烘焙金属 / 深浅体块；
- 更清晰的边缘和台阶关系；
- 侧后光切面；
- 暗部退进；
- 结构化负空间。

### B. 柔软 / 奶油 / 甜品类
空间可使用：
- 更柔和的曲面或低反差平面；
- 奶油白/浅石/半透材质；
- 柔光切面；
- 轻盈负空间。

### C. 冷饮 / 水果 / 清鲜类
空间可使用：
- 玻璃 / 半透 / 湿润石材 / 冷金属；
- 更明亮的纵深；
- 冷暖反射差；
- 通透层次。

### D. 红油 / 卤味 / 浓郁肉类
空间可使用：
- 深石 / 暗金属 / 吸光材质；
- 局部暖反射；
- 深暗部与高光锥；
- 避免整场红棕污染食物真实颜色。

### E. 包装零售
包装/货架身份优先，必要时使用 identity-critical retail exception，不强行转换成餐桌 Hero Stage。

---

## 4. Color Architecture｜环境色由产品反推

必须先锁产品真实颜色，再设计背景色。

建议结构：

```text
PRODUCT_PRIMARY_COLOR = locked
ENVIRONMENT_BASE = neutralized complement / tonal support
ACCENT = restrained echo of product color
DEEP_ZONE = darker or cooler/warmer separation as category requires
```

禁止：
- 全图统一橙棕滤镜；
- 用背景色把食物本身染成另一状态；
- “高级 = 黑金 / 深木 / 暖黄”通用公式。

---

## 5. Light Architecture｜光本身构成背景

背景高级感必须部分由光影结构建立：

- 主体光池只服务 Hero；
- L3 / L4 使用不同强度或方向的 falloff；
- 背景至少一个有意图的 light cut / shadow edge / grazing light；
- 反射材质与吸光材质形成对比；
- 深背景不允许全部均匀糊成一片。

正确：

> 空间即使没有道具，也能靠光线切出层次。

错误：

> 背景本身平，靠几盏 bokeh 灯和几件道具制造“氛围”。

---

## 6. Prop Budget｜道具预算

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
- 香料碟 + 蒜瓣；

这些元素只有在当前食品与构图确实需要时才能出现。

---

## 7. Four-Layer Spatial Evidence

背景必须与 Hero Shot Mandate 一起满足：

### L1
真正靠近镜头的空间入口，可由台缘、材质片、直接支撑边缘或抽象空间体块形成；不强制必须有道具。

### L2
Hero 产品层，最锐、最强 light pool。

### L3
明确后退的材质平面/体块，与 L2 有可见距离差。

### L4
至少两个更深的后退线索，例如：
- 第二个材质平面；
- 凹入暗区；
- 远处结构体块；
- 独立 light falloff；
- 不同焦外层级。

单一墙面、单一渐变、统一 bokeh 都不算。

---

## 8. Background Critical Failures

以下任一项直接背景 FAIL：

1. 删除道具后只剩普通店内/木柜/虚墙；
2. 背景主要由道具而不是空间结构构成；
3. 材质只作为小物件存在，没有形成平面/体块；
4. L3 / L4 缺少真正的前后距离；
5. 全背景同一暖棕/黑金模板；
6. 换成完全不同食品，背景几乎不需要改；
7. 背景强于产品；
8. 背景为了高级感改变产品真实颜色、表面或熟度；
9. 真实经营场所结构无身份必要却被保留；
10. 画面仍首先读成“店里拍的产品”，而不是“商业摄影棚 Hero”。

---

## 9. Targeted Retry

如果 Food Fidelity 已 PASS，但背景不够高级：

> Preserve the exact current food, surface state, count, arrangement, vessel/direct support and all physical relationships. Redesign ONLY Region C environment. Remove dependency on decorative props. Build a category-native premium material architecture using 2–3 primary material planes, explicit near/mid/deep spatial masses, height/depth variation, controlled occlusion, reflective-versus-absorptive material contrast, deliberate light cuts and at least two deep recession cues. Props are optional and subordinate. The background must remain world-class even if all props are removed.

---

## 10. Final Question

生成后必须问：

> **如果把所有布、夹子、杯子、陶器、麦穗、香料、灯泡等道具全部删掉，这张背景本身还像世界级商业摄影舞台吗？**

如果答案不是明确的“是” → Background Architecture FAIL，定向重试。
