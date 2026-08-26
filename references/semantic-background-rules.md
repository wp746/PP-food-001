# Semantic Background Rules

本文件约束背景、环境、辅助道具、色彩和氛围，使它们与**具体菜品语义**相关，而不是套用统一的“高级美食广告背景”。

> **双重约束（V5.2 起）**：背景必须同时满足两份文件——本文件解决「环境语义是否属于这道菜」；`hero-shot-mandate.md` 解决「环境空间是否达到英雄定妆照标准」。语义正确但空间扁平，或空间华丽但语境错位，均不合格。

## 核心原则

> **The product is physically preserved; the environment is semantically designed.**

背景可以大幅升级，但必须解释得通：

- 为什么这个环境适合这道菜；
- 为什么这些颜色支持这道菜；
- 为什么这些辅助元素与菜品有关；
- 为什么新环境仍然像高级商拍材质舞台。

## 1. 禁止通用模板默认化

不得默认所有热食都是：

- 深色木桌
- 暖琥珀灯
- 陶罐
- 大量 bokeh
- 暗黑餐厅
- 大量蒸汽

不得默认所有高级食物都必须“更暗、更暖、更烟”。

**Cinematic 是摄影控制，不是固定滤镜。**

## 2. 用户菜名优先

如果用户明确提供菜名、菜系、风味或卖点：

这些信息必须直接参与背景设计。

例如用户明确说“青花椒酸菜鱼”：

背景必须围绕鲜麻、青花椒、酸菜、川味热汤等语义设计；不能继续使用与普通牛肉面、炖汤完全相同的背景。

## 3. 菜名缺失时

先调用 `dish-semantic-router.md` 推断。

- 高置信度：可以做更具体的菜品语义设计。
- 中置信度：采用品类级语义设计。
- 低置信度：采用保守、真实、与已识别食物类别相符的商业环境。

猜测不得影响主体内容。

## 4. 背景设计六要素

每次内部明确：

```text
background_semantic_theme
context_type
surface_material
supporting_props
color_direction
lighting_character
```

### background_semantic_theme

一句话概括这道菜的视觉世界，例如：

- 高级川味鲜麻热汤材质语境
- 明亮克制的粤式清鲜浅石舞台
- 暗调炭火烧烤材质舞台
- 极简桧木日料舞台
- 柔和大理石甜品舞台

### context_type

V5.3.0 起改为「材质语境」，新设计背景禁止使用真实场所：

- dark matte stone stage
- light stone / marble stage
- wood-texture stage
- metal / glass stage
- fabric / linen stage
- studio only when context is meaningless

### surface_material

表面材质按菜品选择，不固定为木桌：

- wood
- stone
- metal
- neutral counter
- original shelf
- display glass
- original handheld context

### supporting_props

只允许**语义支持道具**，并保持：

- 数量少
- 低对比
- 轻微失焦
- 不与主体重叠
- 不制造“菜里新增食材”的错觉

### color_direction

背景色必须支持菜品而不是压过菜品。

优先级：

1. 食物真实颜色
2. 用户明确品牌/菜品语义
3. 菜系与风味色彩
4. 环境协调色

### lighting_character

灯光根据食物材质和语义选择：

- 鲜麻热汤：方向柔光 + 克制热气背光 + 清晰青绿/暖金色区分
- 粤式清鲜：明亮柔和、干净阴影
- 烧烤：纹理侧光 + 合理炭火暖光
- 甜点：大面积柔光、细腻层次
- 冷饮：边缘光与冷凝材质，不用热气

## 5. 语义道具边界

道具用于“暗示环境”，不是给食物加料。

例如青花椒酸菜鱼可以在远处或边缘使用：

- 少量青花椒枝意象
- 腌菜陶罐
- 小料碟
- 中式餐饮器物

但禁止：

- 把大量新青花椒铺到主菜上
- 给鱼汤添加原图没有的酸菜块
- 把背景道具变成主体配料

## 6. 原场景是否保留

先判断原背景的语境价值。

### 有高语境价值

例如（指源图本身自带的语境）：

- 夜市
- 手持饮品
- 超市货架
- 蛋糕展示柜
- 烧烤摊

策略：**Enhance, don't replace**——但环境层一律向高级材质语言转译（V5.3.0）：保留语境可读性，剥离场所结构（门头/招牌/街道/人物）。

### 语境价值低

例如：

- 杂乱普通桌面
- 无意义墙面
- 截图边框
- 随手拍中的无关杂物

策略：可以重新设计环境，但必须语义匹配。

## 7. 真实合成要求

任何背景升级都必须与主体保持：

- 相同相机高度逻辑
- 相同透视逻辑
- 正确接触平面
- 正确阴影方向
- 正确环境反射
- 合理景深
- 合理尺度

禁止“主体像贴纸贴在新背景上”。

## 8. 青花椒酸菜鱼示例

### 已知信息

```text
dish_name: 青花椒酸菜鱼
cuisine_type: 川味
flavor_profile: 鲜麻、酸香、开胃、热汤
```

### 推荐设计

```text
background_semantic_theme: 高级川味鲜麻热汤材质舞台
context_type: dark matte stone / restrained deep-wood stage
surface_material: 深灰石材或克制深木中餐桌面
supporting_props: 少量失焦青花椒意象、酸菜陶罐、小料碟；全部远离主体
color_direction: 藤椒绿 + 酸菜黄绿 + 汤汁暖金 + 深灰/深木
lighting_character: 45°柔和方向主光，后侧轻微热汤背光，环境暖光克制
photography_mode: CINEMATIC_EDITORIAL，必要时轻度 DRAMATIC_FOOD_CAMPAIGN
```

### 明确避免

- 通用西式黑金模板
- 大量红辣椒背景
- 只有木桌+黄色灯泡
- 青绿色霓虹赛博风
- 过多蒸汽遮挡鱼片
- 新增主菜配料

## 9. 最终检查

生成前问：

1. 背景为什么属于这道菜？
2. 换成另一道完全不同的菜，这个背景是否仍然完全一样？
3. 如果答案是“是”，说明背景仍然过于模板化，应重新设计。

目标是：

> **The background should feel specific enough that it supports this dish, but restrained enough that the original food remains the hero.**
