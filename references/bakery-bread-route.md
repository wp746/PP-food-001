# Bakery Bread Hero Route

面包主体强制使用：

```text
SELECTED_STAGE_A_ROUTE = BAKERY_BREAD_HERO
SOURCE_BREAD_SURFACE_STATE > BAKERY_APPETITE_STYLING
BACKGROUND_ARCHITECTURE > BAKERY_PROPS
```

本路由覆盖旧“咖啡 / 烘焙”混合语义。不要因为产品来自面包店/咖啡店，就自动调用咖啡豆、手冲壶、亚麻布、黄铜夹子、麦穗或咖啡馆 Lifestyle。

---

## 1. Product Truth / Surface Lock

必须锁定：
- 单体外轮廓；
- 圆环/长条/块状几何；
- 割包/爆口/裂纹/白色开口位置、宽度、比例；
- 源图真实表皮深浅与烘烤色；
- 源图真实焦化程度；
- 源图真实光泽/哑光等级；
- 内瓤可见范围；
- 多产品数量、重叠、阵列关系；
- 木箱/托盘/烘焙纸等直接承载关系。

不得把手作面包标准化成更完美的另一批产品，也不得为了“更香、更脆、更高级”加深烘烤色、焦化、油亮或裂纹。

---

## 2. Bread Hero Material Language

面包高级感来自：

```text
SOURCE-TRUE CRUST
+ CRACK / SCORING
+ CRUMB
+ BAKING MATERIAL MEMORY
+ ARCHITECTURAL DEPTH
```

不是咖啡馆道具。

### Primary materials
根据产品选择 2–3 种主材质并让它们形成**空间平面/体块**：
- warm grey honed limestone / travertine；
- fine warm-grey stone；
- smoked / bronzed baking steel；
- dark neutral baking metal；
- restrained parchment only when useful；
- original wood tray only when it is true direct support.

### Color logic
环境围绕源图真实面包颜色设计：
- source crust brown / amber；
- source pale split / crumb；
- warm-neutral grey；
- restrained bronze / smoked-metal highlight；
- off-white only as controlled relief.

禁止统一橙棕滤镜。

---

## 3. Bakery Background Architecture — mandatory

面包 Hero 背景必须先设计建筑关系，再考虑道具。

```text
BAKERY_BACKGROUND_ARCHITECTURE =
- primary material planes: 2-3
- hero support plane
- raised / offset mid-depth slab or panel
- deeper recessed plane / shadow void
- height variation
- perspective/occlusion relationship
- light-cut / grazing-light structure
- reflective-vs-absorptive material contrast
- clean vertical negative space for KV
- props optional
```

### 对碱水 / Bagel-like browned bread
推荐结构方向：
- 保留原木箱/托盘作为 direct support；
- 外部环境转成 warm-grey honed stone + smoked/bronzed baking-metal 的层叠空间；
- L3 可使用明显后退的暖灰石材台阶/斜板或烘焙金属平面；
- L4 使用第二深度平面 + 凹入暗区/更深金属或石材体块，形成至少两个后退线索；
- 通过狭长 grazing light / shadow edge 切出空间；
- 上方留干净负空间，不做一堵暖棕虚墙。

**默认不要出现：**
- 亚麻布；
- 黄铜夹子；
- 麦穗；
- 咖啡器具；
- 陶罐；
- “烘焙图库”小道具组合。

除非当前构图确实需要且视觉权重极低。

### Anti-prop-kit test

> 如果删掉所有道具，背景是否仍然像专门为这批面包设计的高预算商业摄影舞台？

如果不是 → FAIL。

---

## 4. Subtype Art Direction

### A. 碱水 / Pretzel / Bagel-like
视觉核心：源图真实焦糖/琥珀深浅、白色裂口、圆环几何和现有表皮光泽。

灯光：
- 45° large soft key；
- rear-side rim 勾白色裂口与圆弧；
- controlled specular line 只揭示已有壳面；
- Hero light pool 明显强于背景。

禁止：深烤化、黑亮壳、裂纹夸大、假蒸汽。

### B. 恰巴塔 / 欧包 / 酸种 / 法棍
突出源图已有脆壳、裂纹/割口、手作不规则几何；若有切面，只揭示真实气孔，不重做更漂亮的孔洞。

背景偏 limestone / travertine + baking steel 的建筑化关系，非咖啡馆 Lifestyle。

### C. 柔软餐包 / 奶香面包
可用更明亮浅暖石材与柔和低反差平面，但仍要有 L1/L2/L3/L4，不得退化成浅色背景板。

---

## 5. Multi-Product Hero

```text
PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER
SUPPORTING_PRODUCT_FIELD
```

不移动、不减少、不复制、不重排；只用 light pool、rim、局部锐度、对比、DOF 建立主次。

所有单体等权、首先读成库存陈列 → FAIL。

---

## 6. Four-Layer Bakery Stage

### L1
近相机的托盘边缘/舞台边缘/抽象材质片，重虚化；不强制放道具。

### L2
面包 Hero，最锐、最亮、源图真实材质可读。

### L3
明显后退的石材/烘焙金属材质平面或体块，中虚化。

### L4
至少两个更深的材质/光影线索 + 负空间。

单一棕色虚墙、单块灰板、一团 bokeh 都不算 L4。

---

## 7. Photography Mode

默认：

```text
CINEMATIC_EDITORIAL
```

多产品广告英雄阵列：

```text
PREMIUM_BAKERY_CAMPAIGN
```

“更电影”只允许来自光、空间、镜头和材质，不允许来自更深烤色。

---

## 8. Acceptance

```text
OUTPUT_ASPECT_RATIO_EXACT = 9:16
BAKERY_BREAD_ROUTE = PASS
SOURCE_BREAD_SURFACE_STATE = PASS
BACKGROUND_ARCHITECTURE = PASS
PROP_KIT_DEPENDENCY = FALSE
COFFEE_LIFESTYLE_CONTAMINATION = FALSE
MULTI_PRODUCT_HERO_HIERARCHY = PASS when applicable
FOUR_LAYER_BAKERY_STAGE = PASS
GENERIC_DISPLAY_CASE_LOOK = FALSE
```

目标：

> **同一份、同一烘烤状态的真实面包，被世界级商业摄影团队放入为其专门设计的材质建筑舞台中重新拍摄。**