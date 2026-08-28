# Semantic Background Quality Control

本文件用于生成后检查：背景、环境、色彩、道具、空间和摄影气质是否真正与当前食品匹配。

高保真主体通过并不代表整张图完成。

最终目标：

> **High Fidelity + High Photography Upgrade + High Semantic Relevance + True Hero Spatiality**

---

## 1. Semantic Score / 100

### Semantic Relevance / 30
背景是否明显服务当前食品，而不是通用模板？

### Cuisine / Category Alignment / 20
环境是否符合用户提供或高置信度推断出的食品品类/菜系？

### Flavor / Material Atmosphere Match / 20
视觉气质是否与当前食品的味觉和材质语言一致？

### Prop Relevance / 10
辅助道具是否少量、相关、弱化，不制造新增食材错觉？

### Color Direction Match / 10
环境色是否支持食品真实颜色与品类气质？

### Non-Template Diversity / 10
是否避免重复使用同一套深木、暖琥珀、陶器、亚麻、黄铜、bokeh 等“高级素材包”？

通过门槛：

```text
Semantic Score >=85
```

---

## 2. Hero Spatial Score / 100 — 独立硬门槛

```text
Hero Spatial Score >=85
AND NO HERO_SPATIAL_CRITICAL_FAILURE
```

不得凭“看起来有点景深”主观给高分。必须按可观察证据评分。

### A. L1 Spatial Entry / 15
- 是否存在真正位于相机近端的重虚化空间入口？
- 是否明显比 Hero 更靠近镜头？
- 是否形成前后遮挡/框景，而不是简单在产品旁边摆一个道具？

**没有可见 L1 → 本项最多 4/15。**

### B. L2 Hero Plane / 20
- Hero 是否为最锐、最重要的视觉层？
- 是否坐在明确 light pool 内？
- 产品周围是否存在自然光线衰减？
- 是否首先读成“英雄产品”，而不是“库存/陈列”？

多产品场景必须有 `PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER`。

### C. L3 Mid-Background Separation / 15
- L3 是否明显位于 Hero 后方？
- 是否有与当前食品相关的高级材质/器物？
- 是否与 L2、L4 都能看出距离差？

仅在 Hero 后面放一块布/夹子/石块，不自动构成有效 L3。

### D. L4 Deep Recession / 20
L4 必须有**至少两个可分辨的后退材质/光影线索**，例如：
- 两个不同距离的材质平面；
- 远处器物轮廓 + 更深暗部；
- 多层 light falloff；
- 可感知的前后 bokeh 级差；
- 深背景负空间与近背景不是同一平面。

以下不算 L4：
- 一堵均匀虚墙；
- 单一渐变背景；
- 一团无层次 bokeh；
- 单块模糊灰板/棕板。

**若 L4 只有单一平面 → 本项最多 5/20。**

### E. Hero Lighting Sculpting / 15
- 45° controlled key 是否雕刻主体材质？
- rim / back separation 是否在关键边缘有效？
- 接触阴影是否物理正确？
- 主体与背景是否有亮度/色温分离？

### F. Category-Native Material Stage / 10
- 材质、色彩、光性是否从当前食品本身推导？
- 换成完全不同食品后，这套舞台是否必须改变？

### G. Campaign Finish / 5
- 是否像顶级商业摄影团队有明确 art direction 的成片？
- 还是只像菜单照、店内展示照、普通 Lifestyle 照？

---

## 3. HERO_SPATIAL_CRITICAL_FAILURES

以下任一项存在，`Hero Spatial Score` **不得 >=85**：

1. **无 L1 空间入口**：画面从产品平面直接开始，没有近相机层。
2. **Fake L4**：远景只是一堵虚墙、一个渐变、一团 bokeh 或单块背景板。
3. **Two-Layer Flatness**：主体清晰 + 后面统一虚化，没有连续深度递进。
4. **No Light Pool**：主体和背景几乎同亮度/同色温，视线没有被单点锁住。
5. **No Hero Hierarchy in Multi-Product Scene**：多个产品视觉权重完全相同，首先读成库存/展示陈列。
6. **Generic Display-Case Look**：在普通展示柜/托盘场景中，柜体/墙面被机械保留，最终仍首先读成“店里拍的”，且不存在 identity-critical 原因。
7. **Prop-Kit False Premium**：仅靠亚麻布、夹子、石块、陶罐等几个通用道具冒充高级舞台，空间结构和品类语义并未真正升级。
8. **Wrong Material Language**：四层存在，但材质/颜色与当前食品属性没有不可替换关系。
9. **Product Pasted Into Stage**：接触平面、透视、阴影、环境反射不一致。
10. **Venue Dominance**：背景仍是可识别经营场所结构，并压过“材质舞台”读感。

---

## 4. Appetite Score — 独立硬门槛

```text
Appetite Score >=85
```

检查：
1. 真实光泽/湿润/脆壳/切面等食欲信号是否可读？
2. 微距质感是否足够？
3. 温度逻辑是否正确？
4. 食物主色是否鲜活但不失真？
5. 是否有“刚做好/刚烤好”的即时状态？
6. 是否避免塑料亮膜、假湿、过饱和、过度蒸汽？

终审：3 秒内是否产生“想吃”的生理反应？

---

## 5. Semantic Critical Failures

以下任一项直接失败：
- 明确菜名/品类却路由到另一食品语境；
- Food DNA 漂移；
- 包装零售身份被错误移出必要货架；
- 冷食出现热蒸汽；
- 背景道具进入主菜造成新增食材；
- 为呼应语义而改食物、器皿、摆盘；
- 背景完全通用于大量不同食品；
- 真实场所污染且无 identity-critical 理由；
- 食欲感干涩、发死、塑料化；
- 任一 `HERO_SPATIAL_CRITICAL_FAILURE`。

---

## 6. Category / User Information Consistency

如果用户提供：

```text
dish_name
product_category
cuisine_type
flavor_profile
main_highlights
```

则逐项检查环境是否一致。

用户信息是语义设计最高优先级事实，但不能覆盖源图产品真相。

若品类由系统推断：
- 高置信度 → 可具体设计；
- 中置信度 → 品类级设计；
- 低置信度 → 保守商业材质舞台。

低置信度猜测不得变成强势配料/地域事实。

---

## 7. Anti-Template Test

生成后问：

1. 为什么这个背景属于当前食品？
2. 哪些材质、颜色、光线和空间决定是由当前食品驱动的？
3. 如果换成完全不同食品，这套舞台是否仍几乎无需变化？
4. 如果去掉新增的几个小道具，画面是否立刻退回普通店内/展示柜照片？

第 3 题 = 是，或第 4 题 = 是 → 必须重试。

---

## 8. Final Acceptance

```text
Fidelity Score >=95
Photography Score >=85
Semantic Score >=85
Hero Spatial Score >=85
Appetite Score >=85
No Fidelity Critical Failure
No Semantic Critical Failure
No Hero Spatial Critical Failure
```

高保真但空间普通，不能交付。

空间高级但产品漂移，也不能交付。

---

## 9. Targeted Retry Directions

### A. Generic Display Case / Venue Conservatism

> The product is faithful, but the result still reads as an ordinary shop/display-case photograph. Preserve the exact food, count, arrangement, original direct tray/support and contact relationships. Remove the generic cabinet/wall/venue as the dominant environment and translate only that outer context into a category-native premium material Hero Stage with visible L1/L2/L3/L4 depth. Do not move or redesign the product.

### B. Camera Too Conservative

> The product is faithful, but the framing still inherits the accidental snapshot camera. Use a controlled Hero Reframe: improve crop, focal-length feel, camera height/pitch and 9:16 spatial composition while preserving visible-face proportions, product geometry, count, overlap, support plane and believable perspective. Do not invent unseen sides or use extreme wide-angle/low-angle distortion.

### C. Multi-Product Inventory Look

> Preserve every visible unit and its position. Select one existing foreground unit or cluster as the optical Hero using light pool, rim light, local sharpness, contrast and depth-of-field only. Let the remaining unchanged product field recede progressively. Do not move, remove, duplicate or re-stack products.

### D. Fake Four-Layer Depth

> Rebuild the environment with observable depth evidence: a true near-camera L1 entry, Hero L2 in a light pool, clearly separated L3 material objects, and L4 with at least two perceptible receding material/light planes plus clean negative space. A single blurred wall/gradient/bokeh field is not L4. Keep the product unchanged.

### E. Generic Prop Kit

> Remove generic premium props that do not specifically serve the current food. Rebuild the stage from the product's own material character, color, temperature and category. Do not use recurring linen/tongs/stone/ceramic combinations by default.

### F. Food Looks Dry / Dull

> Re-render only the source-supported appetite properties with stronger material-specific specular control, micro-texture and edge light. Keep the product geometry and ingredients unchanged.

### G. Wrong Category Material Language

> Re-route the environment to the current food category. Preserve all product geometry and the four-layer spatial structure, but replace unrelated stage materials/colors/props with category-native ones.

Retry by diagnosed failure type. Do not random-regenerate already correct regions.