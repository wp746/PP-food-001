# Semantic Background Rules

本文件只解决一个问题：

> **为什么这个环境属于当前这道食品？**

空间怎么搭、层次怎么做、材质平面怎么组织，由 `hero-background-architecture.md` 负责；本文件不得把 Agent 拉回“道具布置型高级感”。

---

## 0. Core Principle

```text
THE_PRODUCT_IS_PHYSICALLY_PRESERVED
THE_ENVIRONMENT_IS_SEMANTICALLY_DESIGNED
BACKGROUND_ARCHITECTURE > PROP_STYLING
```

背景可以大幅升级，但必须能解释：
- 为什么这个空间适合当前食品；
- 为什么这些材质来自当前食品的几何/表面/颜色/温度/工艺；
- 为什么换成另一食品后需要重新设计；
- 为什么环境仍让食品成为唯一 Hero。

---

## 1. Semantic Inputs

优先级：

```text
1. 用户明确提供的产品/菜名/品类/风味
2. 当前图片可见食品事实
3. 高置信度品类推断
4. 保守品类级 fallback
```

猜测不得改变主体内容，也不得生成不存在的配料事实。

---

## 2. Semantic Design Fields

每张图内部只需要明确：

```text
semantic_theme
category_temperament
food_material_character
food_color_logic
temperature_process_logic
background_big_idea
```

其中：

### semantic_theme
一句话说明视觉世界属于谁，例如：
- 清鲜通透的浅矿物舞台；
- 浓郁卤味的深吸光材质舞台；
- 现烤面包的烘焙工艺雕塑舞台；
- 冷饮的玻璃/冷金属折射舞台。

### background_big_idea
必须从 `hero-background-architecture.md` 编译，不能只写“高级、电影感、暖色、生活方式”。

---

## 3. Product-Derived Semantics

至少使用 3 项当前食品证据来决定环境：

```text
geometry
surface/material
color
temperature/process
category temperament
```

例如：
- 亮壳焦糖色面包 → 吸光暖灰石材 + 烘焙金属，突出原壳色，不用咖啡馆道具；
- 红油卤味 → 深哑光材质压住环境反光，让真实酱油/油光成为最高亮点；
- 透明冷饮 → 玻璃/冷金属/折射体块，靠冷边光和透明层次表达；
- 奶油甜品 → 浅矿物石/柔曲面/低反差材质，增加轻盈负空间。

---

## 4. Props Are Optional

```text
PROPS_REQUIRED = FALSE
```

辅助道具只有在明确增强当前食品身份、空间尺度或遮挡关系时才出现。

必须：
- 0–3 个以内；
- 低对比；
- 轻虚化；
- 不与主体重叠；
- 不制造新增食材错觉；
- 删除后背景仍然成立。

禁止把以下组合默认当成“高级感”：
- 亚麻布 + 黄铜夹子；
- 咖啡豆 + 手冲壶；
- 麦穗 + 面粉；
- 陶罐 + 木勺；
- 香料碟 + 蒜瓣；
- 灯泡/bokeh + 深木。

---

## 5. Color Direction

优先级：

```text
1. 食品真实颜色
2. 用户明确品牌/产品语义
3. 品类与工艺色彩
4. 环境协调色
```

环境色应形成支持或对比，不得把产品染成另一火候、熟度或材质状态。

禁止：
- 通用橙棕滤镜；
- 黑金通用高级感；
- 食物与背景同色导致主体消失；
- 用更深背景顺便把食物也加深。

---

## 6. Lighting Character

灯光只根据当前食品材质和温度决定：
- 清鲜：明亮柔光、干净阴影；
- 红油/卤味：控制环境反射，让源图已有油光被准确看见；
- 烧烤：纹理侧光、真实焦边读取，不增加焦化；
- 烘焙：侧/后光雕刻源图已有壳纹、裂口与内瓤，不加深烘烤色；
- 甜点：大面积柔光、细腻层次；
- 冷饮：冷白边光、透明/冷凝读取，不出现热气。

---

## 7. Original Scene Value

原场景必须拆成：

```text
DIRECT_SUPPORT / IDENTITY_CRITICAL_CONTEXT / GENERIC_VENUE_CONTEXT
```

- Direct support：锁定；
- identity-critical context：按需保留；
- generic venue：可转译或移除。

普通展示柜、店内墙面、柜体、无品牌货架不能因为“原图里有”就压过 Hero Stage。

---

## 8. Realistic Integration

任何环境升级必须保持：
- 可信相机高度/透视；
- 正确接触平面；
- 正确阴影方向；
- 正确环境反射；
- 合理景深；
- 合理尺度。

禁止产品像贴纸贴在新背景上。

---

## 9. Anti-Template / Anti-Prop Test

生成前后都问：

1. 这个背景为什么属于当前食品？
2. 至少哪 3 项设计决定来自当前食品？
3. 如果换成完全不同食品，这个背景是否仍几乎不用变化？
4. 删除所有小道具后，背景是否仍然是世界级商业摄影舞台？
5. 背景是否有一个明确 One Big Idea，而不是很多“看起来高级”的零碎物件？

若 3=是、4=否或5=否 → FAIL。

---

## 10. Acceptance

必须同时满足：

```text
SEMANTIC_RELEVANCE = PASS
PRODUCT_DERIVATION_EVIDENCE >= 3
BACKGROUND_BIG_IDEA = PASS
BACKGROUND_ARCHITECTURE_PLAN = PASS
PROP_DEPENDENCY_FOR_PREMIUM_LOOK = FALSE
PRODUCT_REMAINS_HERO = TRUE
```

最终目标：

> **环境一眼属于这道食品，但绝不靠复制食品配料、真实门店或通用道具包来证明身份。**