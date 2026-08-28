# Bakery Bread Hero Route

本文件是 Stage A 面包类产品的**品类专属覆盖规则**。

当当前产品的主体身份是面包，而不是咖啡饮品、蛋糕甜品或包装零售商品时，必须优先使用本文件：

```text
SELECTED_STAGE_A_ROUTE = BAKERY_BREAD_HERO
```

本路由覆盖 `cuisine-style-map.md` 中旧的“咖啡 / 烘焙”混合语义。**不要因为产品来自面包店/咖啡店，就自动调用咖啡豆、手冲壶、咖啡馆 Lifestyle 或通用原木+亚麻+黄铜皮肤。**

## 1. Trigger

典型触发：
- 贝果 / 碱水贝果 / Pretzel-style bread；
- 恰巴塔 / Ciabatta；
- 欧包 / 酸种 / Sourdough；
- 法棍 / 硬欧；
- 普通餐包 / 手作面包；
- 以“面包本体”为第一视觉主体的现烤烘焙产品。

若产品主体是咖啡/茶饮 → 走咖啡饮品路线。

若主体是蛋糕、慕斯、奶油甜品 → 走甜品路线。

若主体是密封包装零售食品 → 走包装/零售路线。

## 2. Product Truth / DNA Lock

面包类高风险漂移点：
- 单体外轮廓；
- 圆环/长条/块状几何；
- 割包、爆口、裂纹、白色开口的位置与比例；
- 表皮深浅与烘烤色；
- 表面光泽/哑光属性；
- 内瓤可见范围与组织；
- 多产品数量、重叠、阵列关系；
- 托盘/木箱/烘焙纸等直接承载关系。

不得把不规则手作面包“标准化”成更完美、更对称的另一批产品。

## 3. Hero Material Language

面包的高级感来自：

```text
CRUST / CRACK / CRUMB / BAKING HEAT MEMORY
```

而不是咖啡馆道具。

### Primary material stage

根据面包本身选 2–3 种主材质，不要全堆：
- warm honed limestone / travertine；
- warm grey fine stone；
- dark or bronzed baking steel；
- smoked neutral metal；
- restrained parchment / baking paper；
- low-contrast linen only when compositionally useful；
- original wood tray when it is the true direct support.

### Material color logic

环境色由面包本身提取：
- caramel crust brown；
- cream crumb / pale split；
- warm neutral grey；
- muted bronze / baking-metal highlights；
- restrained off-white.

禁止整张图被统一橙棕滤镜吞掉。

## 4. Subtype Art Direction

### A. 碱水 / Pretzel / Bagel-like browned bread

视觉核心：
- 深焦糖/琥珀表皮；
- 高光沿圆弧滑动；
- 白色爆口/裂纹形成强明暗对比；
- 圆环或扭结几何形成节奏。

推荐舞台：
- warm grey honed stone；
- smoked / bronzed baking metal；
- 少量纸/布柔化硬材质；
- 深处多层中性暖灰与烘焙棕光影退进。

灯光：
- 45° large soft key；
- rear-side rim 精准勾白色裂口和圆弧；
- controlled specular line on the brown crust；
- product light pool 明显强于背景。

避免：
- 咖啡豆、手冲壶、咖啡杯默认入场；
- 木墙 + 亚麻布 + 黄铜夹子三件套；
- 平面暖棕墙；
- 过量面粉把碱水表皮做成欧包；
- 强行蒸汽。

### B. 恰巴塔 / 欧包 / 酸种 / 法棍

视觉核心：
- 脆壳纹理；
- 裂纹/割口；
- 手作不规则几何；
- 若源图可见切面，则强调真实气孔/内瓤，不得重新生成更“漂亮”的孔洞。

推荐舞台：
- limestone / travertine；
- dark baking steel；
- parchment；
- restrained flour memory only when semantically safe and kept outside product.

灯光：侧后方向光雕刻壳纹与裂口，背景更克制、更建筑化，不做咖啡馆 Lifestyle。

### C. 柔软餐包 / 奶香面包

视觉核心：
- 柔软体积；
- 烘烤顶部渐变；
- 轻薄光泽；
- 软与暖。

舞台可更明亮：浅暖石材 + 柔和织物 + 烘焙金属细节，但仍必须有四层空间，不得退化成浅色背景板。

## 5. Multi-Product Hero Plan

面包常以整盘/整箱出现。

必须建立：

```text
PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER
SUPPORTING_PRODUCT_FIELD
```

规则：
- 不移动产品；
- 不减少数量；
- 不重排；
- 不复制；
- 从原图已经存在的前景单体/小簇中选 Hero；
- 用 light pool、rim、局部锐度、对比、景深建立主次；
- 后方阵列逐级退入景深，但身份仍可读。

如果所有面包视觉权重一样，画面首先读成“库存陈列”，Hero FAIL。

## 6. Four-Layer Bakery Stage

### L1
近相机的托盘边缘、烘焙纸边、低对比工具边缘等，重虚化，形成空间入口。

### L2
面包 Hero。最锐、最亮、最具材质表现，处于 light pool。

### L3
明显后退的烘焙金属、石材、纸/布或兼容器物，中虚化；必须和 L2、L4 都能看出距离差。

### L4
至少两个可感知的后退材质/光影平面，进入更深的暖灰/烘焙棕中性空间并保留干净负空间。

**单一棕色虚墙、单块灰背景、一团 bokeh 不算 L4。**

## 7. Photography Mode

面包主体默认为：

```text
CINEMATIC_EDITORIAL
```

当原图为多产品阵列、需要更强广告英雄感时：

```text
PREMIUM_BAKERY_CAMPAIGN
```

`NATURAL_EDITORIAL` 只在产品本身轻盈、明亮、生活方式语义明显且仍能满足 Hero Spatial >=85 时使用。

“自然”不等于“普通店内自然光”。

## 8. Appetite Signals

只强化源图已有属性：
- caramelized crust sheen；
- crisp shell highlights；
- scoring / crack relief；
- cream crumb contrast；
- fresh-baked softness where visible；
- slight baking warmth in light, not fake steam.

面包食欲核心：

> **壳的脆、裂口的亮、内里的软。**

避免：
- 塑料亮膜；
- 油刷感过重；
- 表皮统一镜面；
- 凭空出现黄油、糖粉、芝麻、奶油、坚果等。

## 9. Anti-Template Check

生成前必须问：

1. 如果把当前面包换成咖啡，这套舞台是否几乎不用改？如果是 → FAIL。
2. 如果去掉面包，只剩“原木 + 亚麻 + 黄铜夹子”，是否仍像通用烘焙图库？如果是 → FAIL。
3. 舞台是否明确在服务当前面包的壳色、裂口、几何和烘焙质感？如果否 → 重路由。

## 10. Acceptance

除全局 Stage A 门槛外，面包 Hero 必须满足：

```text
BAKERY_BREAD_ROUTE = PASS
COFFEE_LIFESTYLE_CONTAMINATION = FALSE
MULTI_PRODUCT_HERO_HIERARCHY = PASS when applicable
FOUR_LAYER_BAKERY_STAGE = PASS
PRIMARY_CRUST_LIGHTING = PASS
GENERIC_DISPLAY_CASE_LOOK = FALSE
```

目标：

> **同一份真实面包被世界级商业摄影团队重新拍摄，而不是把普通展示柜照片加暖光、亚麻布和夹子。**