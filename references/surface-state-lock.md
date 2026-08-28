# Surface / Material State Lock｜全品类表面状态锁与拓扑延续

本文件适用于 Stage A 的**所有食品品类**。它解决一个核心风险：图像模型为了“更有食欲 / 更高级 / 更电影感”，把原产品重新烹饪、重新上色、重新上光或重新塑形。

## 0. P0 Principle

```text
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
SOURCE_STRUCTURE > BEAUTIFICATION
TOPOLOGY_PRESERVING_COMPLETION > INVENTION
```

商拍升级的目标是：

> **让原图已有的食物状态被更好的摄影看见，而不是把食物本身变成一个更夸张的新状态。**

食欲感主要来自：灯光位置、曝光、显色、镜面高光控制、微对比、纹理解析、景深、色彩分级和真实的新鲜度读取。

食欲感**不来自重新烹饪产品**。

---

## 1. Surface State Manifest｜生成前必须记录

每个当前任务必须从原图记录可见的表面/材质状态。只记录源图有证据的项目：

```text
base_color_and_gradient
browning_level
char_level
cooking_doneness
surface_gloss_level
surface_matte_level
moisture_level
sauce_oil_coverage
crust_skin_state
crack_scoring_state
cream_frosting_state
sugar_powder_state
condensation_frost_state
translucency
freshness_cues
visible_damage_or_irregularity
```

对于不同品类，可对应为：
- 面包：烘烤深浅、焦糖色、爆口/割口、壳面光泽、内瓤暴露范围；
- 肉类/牛排：熟度、焦化程度、肉汁、酱汁覆盖；
- 卤味：卤色深浅、皮肤纹理、油亮程度、辣椒/香料附着；
- 红油/汤汁：油层厚度、透明度、颜色、覆盖范围；
- 烧烤：炭化范围、焦边、油滴状态；
- 甜品：奶油/糖霜形态、缎面/哑光程度、切面湿润度；
- 水果/轻食：天然水分、切面、表皮光泽、水珠有无；
- 饮品：分层、冰块、泡沫、冷凝、透明度；
- 海鲜/日料：湿润度、半透明程度、表面反光；
- 包装食品：包装本身的哑光/亮膜、印刷与表面状态。

---

## 2. What May Improve｜允许优化

只允许把**源图已经存在**的材质特征更准确、更清晰地呈现：

- 修正曝光与白平衡；
- 恢复真实颜色层次；
- 通过主光/rim light 让原有轮廓和纹理更可读；
- 通过 specular control 让原有油光/水光更自然；
- 提升微纹理解析；
- 提升局部对比，但不改变材料本身；
- 恢复被手机拍摄压扁的动态范围；
- 让原本已有的新鲜、脆、润、透、软、酥等视觉信号更容易读到。

核心：

```text
REVEAL EXISTING PROPERTY
DO NOT AMPLIFY PROPERTY BEYOND SOURCE IDENTITY
```

---

## 3. What Must Stay Locked｜禁止改变

以下变化若超过普通摄影造成的视觉差异，属于 Surface State Drift：

- 原本浅烘烤 → 深焦/焦黑；
- 原本中度焦糖色 → 变成深红褐/黑亮壳；
- 原本轻微油光 → 变成厚重油刷感；
- 原本哑光/半哑光 → 变成镜面塑料亮膜；
- 原本自然裂纹 → 变成夸张爆口；
- 原本少量汁水 → 变成大量滴汁/流汁；
- 原本清汤/浅油 → 变成浓油/深红；
- 原本熟度 → 改成另一熟度；
- 原本轻焦 → 改成重炭化；
- 原本自然奶油/糖霜 → 变成更厚、更整齐、更豪华的重新裱花；
- 原本无冷凝/水珠 → 凭空大量喷水；
- 原本无糖粉/芝麻/坚果/黄油等 → 为“高级”凭空添加。

如果输出让人判断为“同类食品，但火候/熟度/表皮/酱汁状态明显不同的一批产品”，直接 FAIL。

---

## 4. Appetite Rendering Rule

任何品类的 `Appetite Rendering` 指令都必须先经过本文件过滤。

正确逻辑：

```text
SOURCE PROPERTY = mild
→ render mild property clearly

SOURCE PROPERTY = medium
→ render medium property clearly

SOURCE PROPERTY = strong
→ render strong property clearly
```

错误逻辑：

```text
mild → stronger because appetizing
medium → dramatic because premium
strong → extreme because cinematic
```

**Appetite Score 不能通过改变食物状态来换取。**

---

## 5. Topology-Preserving Completion｜装盘未拍全时的补全规则

当源图因裁切、竖版扩图或取景没有拍全，但能从可见区域高置信度判断同一份食品/器皿/摆盘的自然延续时，允许补全。

### 可补全的对象

- 被画面边缘截断的同一器皿边缘；
- 被裁切的同一托盘/木箱/盘子；
- 被裁切但可从邻近结构明确延续的同一食材；
- 同一堆叠/阵列在画外的最小自然延续；
- 同一酱汁/汤体/油层在器皿内的连续区域；
- 同一装盘拓扑因镜头裁切而缺失的边缘部分。

### 必须继承

```text
ingredient_identity
geometry_and_cut
scale
orientation
layer_order
overlap_logic
density
surface_state
sauce/oil/broth state
container/support relationship
```

### 最高原则

> **Complete the same serving; do not design a better serving.**

补全不是重摆盘权限。

---

## 6. Completion Confidence Gate

```text
HIGH_CONFIDENCE_VISIBLE_CONTINUATION → MAY COMPLETE
MEDIUM_CONFIDENCE → MINIMUM CONSERVATIVE CONTINUATION
LOW_CONFIDENCE / UNKNOWN → DO NOT INVENT PRODUCT CONTENT
```

低置信度时优先：
- 用环境扩图；
- 调整裁切；
- 用景深/遮挡自然收边；
- 保留未知，不强行补产品。

`Unknown ≠ permission to invent` 仍然生效。

---

## 7. Forbidden Completion

禁止借补全：
- 新增新的食材种类；
- 增加更贵/更豪华的配料；
- 把随机堆叠改成规则阵列；
- 把不完整手作结构标准化；
- 改变原食材切法、厚度、颜色或熟度；
- 把补全部分做得比已拍到的部分更焦、更亮、更整齐；
- 增加没有证据的装饰、酱汁、芝麻、香草、糖粉、黄油等；
- 通过复制重复纹理制造明显 AI 克隆感。

---

## 8. QC

生成后必须问：

1. 这是原图同一份产品的表面状态，还是像重新烹饪过？
2. 光泽/湿润/焦化/颜色是“更清楚”，还是“更强了”？
3. 补全区域能否从原图可见信息自然推出？
4. 补全部分是否严格延续原有拓扑，而没有变成重新摆盘？
5. 如果关闭背景和灯光升级，产品本身是否仍与源图是同一状态？

任一问题失败 → Surface State / Completion Retry。

---

## 9. Scope

本规则适用于所有 Stage A 食品：

```text
noodles / rice / meat / braised food / BBQ / seafood / hotpot /
bakery / bread / dessert / fruit / salad / drinks / packaged food / others
```

品类规则可以决定“如何照亮它”，不能决定“把它变成什么状态”。