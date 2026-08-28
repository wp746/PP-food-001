# Bakery Bread Hero Route

面包主体强制使用：

```text
SELECTED_STAGE_A_ROUTE = BAKERY_BREAD_HERO
SOURCE_BREAD_SURFACE_STATE > BAKERY_APPETITE_STYLING
PRODUCT_DERIVED_STAGE > GENERIC_BAKERY_STYLE
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

## 2. Bread Product Derivation — mandatory

至少提取 3 项当前面包证据：

```text
PRODUCT_DERIVATION_EVIDENCE >=3
```

来源：
- geometry：圆环/扭结/长条/阵列节奏；
- surface：壳面哑/亮、白色裂口、内瓤与外壳对比；
- color：源图真实焦糖/琥珀/麦色与奶油白；
- process：碱水、现烤、酸种、硬壳、柔软餐包等工艺气质；
- direct support：真实木托盘/烘焙纸等承载关系。

背景不能先选“烘焙风”，再往里放面包；必须先看面包，再设计舞台。

---

## 3. Bread Background Big Idea

```text
BACKGROUND_BIG_IDEA = one product-derived sculptural bakery-stage concept
```

Big Idea 必须包含：
- 空间结构；
- 2–3 种主材质；
- 光性；
- 与当前面包至少 3 项可见关系。

面包高级感来自：

```text
SOURCE-TRUE CRUST / CRACK / CRUMB
+ BAKING MATERIAL MEMORY
+ ARCHITECTURAL DEPTH
```

不是咖啡馆道具。

默认不允许 Big Idea 只是：
- rustic bakery；
- warm lifestyle；
- dark wood bakery；
- linen / tongs / wheat still life；
- “高级面包店背景”。

---

## 4. Bakery Background Architecture — mandatory

根据产品选择 2–3 种主材质并让它们形成空间平面/体块：
- warm grey honed limestone / travertine；
- fine warm-grey mineral stone；
- smoked / bronzed baking steel；
- dark neutral baking metal；
- restrained parchment only when useful；
- original wood tray only when it is true direct support。

```text
BAKERY_BACKGROUND_ARCHITECTURE =
- hero support plane
- raised / offset mid-depth slab or panel
- deeper recessed plane / shadow void
- height variation
- perspective / occlusion relationship
- light-cut / grazing-light structure
- reflective-vs-absorptive material contrast
- designed vertical negative space
- props optional
```

### 对碱水 / Bagel-like browned bread
推荐：
- 保留原木箱/托盘作为 direct support；
- 外部环境转成暖灰矿物石 + 烟熏/烘焙金属的层叠空间；
- L3 使用明显后退的石材台阶、斜板或烘焙金属平面；
- L4 使用第二深度平面 + 凹入暗区/更深金属或石材体块；
- 用 grazing light / shadow edge 切出空间；
- 用少量浅中性色平面呼应白色裂口，但不染色产品；
- 9:16 上方继续有材质结构和光影退进，不做暖棕虚墙。

**默认不要出现：**
- 亚麻布；
- 黄铜夹子；
- 麦穗；
- 咖啡器具；
- 陶罐；
- “烘焙图库”道具组合。

除非当前构图确实需要且视觉权重极低。

### Anti-prop-kit test

> 如果删掉所有道具，背景是否仍像专门为这批面包设计的高预算商业摄影舞台？

如果不是 → FAIL。

---

## 5. Subtype Art Direction

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

## 6. Multi-Product Hero

```text
PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER
SUPPORTING_PRODUCT_FIELD
```

不移动、不减少、不复制、不重排；只用 light pool、rim、局部锐度、对比、DOF 建立主次。

所有单体等权、首先读成库存陈列 → FAIL。

---

## 7. Exact 9:16 Bakery Composition

```text
OUTPUT_ASPECT_RATIO_EXACT = 9:16
NON_9_16_DELIVERY = CRITICAL_FAILURE
```

必须原生竖版设计：
- L1 在下方/侧下形成近景入口；
- Hero 占中下/中部主要视觉面积；
- L3 向上方/斜后方继续展开；
- L4 在上半部继续有材质体块与光影退进；
- 上方留设计型负空间，但不能是一堵虚墙。

---

## 8. Appetite Signals

只提高摄影可读性：
- source-matched crust sheen；
- source-matched shell highlight；
- source-matched crack relief；
- real crumb contrast；
- visible softness only where source supports it。

> **让原本的壳、裂口、内里更好看见，而不是把壳重新烤一遍。**

---

## 9. Bakery Anti-Template Test

生成前后都问：

1. `BACKGROUND_BIG_IDEA` 是否能明确说出？
2. 是否至少有 3 项背景依据来自当前面包？
3. 去掉所有布、夹子、麦穗、杯子后，舞台是否仍然成立？
4. 如果把面包换成咖啡，这套空间是否仍几乎不用改？若是 → FAIL。
5. 输出面包是否比源图更深、更焦、更亮、更爆口？若是 → Surface State FAIL。
6. 9:16 上半部是否有真实空间结构，而不是虚墙？若否 → FAIL。

---

## 10. Acceptance

```text
OUTPUT_ASPECT_RATIO_EXACT = 9:16
BAKERY_BREAD_ROUTE = PASS
SOURCE_BREAD_SURFACE_STATE = PASS
PRODUCT_DERIVATION_EVIDENCE >=3
BACKGROUND_BIG_IDEA = PASS
BACKGROUND_ARCHITECTURE = PASS
PROP_DEPENDENCY_FOR_PREMIUM_LOOK = FALSE
COFFEE_LIFESTYLE_CONTAMINATION = FALSE
MULTI_PRODUCT_HERO_HIERARCHY = PASS when applicable
FOUR_LAYER_BAKERY_STAGE = PASS
GENERIC_DISPLAY_CASE_LOOK = FALSE
```

目标：

> **同一份、同一烘烤状态的真实面包，被世界级商业摄影团队放入由其几何、壳面、双色关系与烘焙工艺推导出的雕塑化材质舞台中重新拍摄。**