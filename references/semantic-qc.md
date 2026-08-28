# Semantic Background Quality Control

用于生成后检查：背景、空间、材质、色彩、道具、摄影气质和最终画幅是否真正达到 Stage A 世界级 Hero 标准。

目标：

> **High Fidelity + Exact 9:16 + Product-Derived Art Direction + True Hero Spatiality**

---

## 0. Exact Aspect Gate

```text
OUTPUT_ASPECT_RATIO_EXACT = 9:16
NON_9_16_DELIVERY = CRITICAL_FAILURE
```

任何 Stage A 最终图只要不是严格 9:16 竖版，无论其他分数多高都不得交付。

若第一次生成非 9:16：执行 canvas correction / outpaint / targeted retry，再重新 QC。

---

## 1. Semantic / Art Direction Score / 100

- Semantic Relevance / 20
- Product Derivation / 20
- Background Big Idea / 15
- Category Alignment / 15
- Material / Color Match / 15
- Prop Independence / 10
- Non-Template Diversity / 5

```text
Semantic / Art Direction Score >=85
PRODUCT_DERIVATION_EVIDENCE >=3
BACKGROUND_BIG_IDEA = PASS
PROP_DEPENDENCY_FOR_PREMIUM_LOOK = FALSE
```

### Product Derivation / 20
至少有 3 项可观察设计依据来自当前食品的：几何、表面材质、颜色、温度/工艺、品类气质。

### Background Big Idea / 15
必须存在一个明确、统一、可描述的空间/材质/光主概念，而不是零碎道具组合。

### Prop Independence / 10
删除所有辅助道具后，背景是否仍然成立为世界级商业摄影舞台？若否，本项 0 分并触发 Critical Failure。

---

## 2. Hero Spatial Score / 100

```text
Hero Spatial Score >=85
AND NO HERO_SPATIAL_CRITICAL_FAILURE
```

### A. L1 Spatial Entry / 15
必须有真正近相机的空间入口，而不是产品旁边摆一个道具。

### B. L2 Hero Plane / 20
Hero 最锐、处于明确 light pool；多产品必须有 `PRIMARY_HERO_UNIT / CLUSTER`。

### C. L3 Mid-Background Separation / 15
L3 必须是明显后退的材质平面/体块；只放一块布/夹子/石头不算。

### D. L4 Deep Recession / 20
必须至少有两个可分辨的更深材质/光影线索。

不算 L4：一堵虚墙、单一渐变、一团 bokeh、单块模糊灰板/棕板。

### E. Hero Lighting Sculpting / 15
45° controlled key、rim/back separation、接触阴影、主体与背景亮度/色温分离。

### F. Category-Native Material Architecture / 10
背景材质/颜色/光性/空间体块必须从当前食品推导；换食品必须重新设计。

### G. Campaign Finish / 5
是否真正像顶级商业摄影 Art Direction，而不是菜单照/店内陈列照/Lifestyle 图。

---

## 3. HERO_SPATIAL_CRITICAL_FAILURES

任一项存在，`Hero Spatial Score` 不得 >=85：

1. 无 L1 空间入口；
2. Fake L4；
3. Two-Layer Flatness；
4. No Light Pool；
5. 多产品无 Hero hierarchy；
6. Generic Display-Case Look；
7. Prop-Kit False Premium；
8. No Background Architecture；
9. Props Carry The Scene；
10. Wrong Material Language；
11. Product Pasted Into Stage；
12. Venue Dominance；
13. **No Background Big Idea**；
14. **Product Derivation Evidence <3**；
15. **Vertical Dead Zone**：9:16 上半部只是大片无设计模糊墙/空区。

---

## 4. Appetite Score

```text
Appetite Score >=85
```

食欲感必须来自源图已有表面状态在更好的摄影下被读清楚。

禁止为了 Appetite 提高烘烤、焦化、油亮、湿润、酱汁、裂纹、熟度等属性强度。

---

## 5. Semantic Critical Failures

任一项直接失败：
- 输出非严格 9:16；
- Food DNA / Surface State 漂移；
- 明确品类却路由错语境；
- 包装零售身份被错误移出必要货架；
- 冷食出现热蒸汽；
- 背景道具造成新增食材误读；
- 为语义改食物、器皿、摆盘；
- 背景通用于大量不同食品；
- 真实场所污染且无 identity-critical 理由；
- 背景高级感依赖通用道具包；
- `BACKGROUND_BIG_IDEA` 缺失；
- `PRODUCT_DERIVATION_EVIDENCE <3`；
- 任一 `HERO_SPATIAL_CRITICAL_FAILURE`。

---

## 6. Anti-Template / Architecture Test

生成后问：

1. 为什么这个背景属于当前食品？
2. 至少哪 3 项材质、颜色、几何、温度/工艺或光线决定来自当前食品？
3. `BACKGROUND_BIG_IDEA` 是什么？
4. 换成完全不同食品，背景是否必须明显变化？
5. 去掉所有新增小道具，背景是否仍像世界级商业摄影舞台？
6. 背景本身是否有近/中/深体块、高差、遮挡、反射差和光影切面？
7. 9:16 上方空间是否有真实纵深，而不是一堵虚墙？

第 4=否、第 5/6/7=否，或第 3 无法明确回答 → Background Architecture Retry。

---

## 7. Final Acceptance

```text
Output Aspect Ratio = EXACT 9:16
Fidelity Score >=95
Photography Score >=85
Semantic / Art Direction Score >=85
Hero Spatial Score >=85
Appetite Score >=85
PRODUCT_DERIVATION_EVIDENCE >=3
BACKGROUND_BIG_IDEA = PASS
BACKGROUND_ARCHITECTURE_PLAN = PASS
PROP_DEPENDENCY_FOR_PREMIUM_LOOK = FALSE
No Fidelity Critical Failure
No Semantic Critical Failure
No Hero Spatial Critical Failure
```

高保真但背景普通，不能交付。
背景高级但产品漂移，也不能交付。
非 9:16，不能交付。

---

## 8. Targeted Retry

### A. Non-9:16
> Preserve the exact product and current accepted photography. Correct only canvas/aspect to exact 9:16 portrait using environment extension and safe recomposition. Do not distort, crop away or rebuild the product.

### B. Background Big Idea / Product Derivation Failure
> Preserve the exact food, surface state, count, arrangement, direct support and all physical relationships. Redesign ONLY Region C. Derive at least three visual facts from the current product and define one clear BACKGROUND_BIG_IDEA. Build the stage from only 2–3 primary material planes, explicit near/mid/deep spatial masses, height/depth variation, controlled occlusion, reflective-versus-absorptive contrast, deliberate light cuts and at least two deep recession cues. Props are optional and subordinate.

### C. Generic Display Case
> Preserve product/direct support. Remove generic cabinet/wall/venue dominance and translate outer context into a category-native Hero Stage.

### D. Camera Too Conservative
> Use controlled Hero Reframe while preserving visible-face proportions, geometry, count, overlap, support plane and believable perspective.

### E. Multi-Product Inventory Look
> Preserve every unit and position; establish one optical Hero only through light/sharpness/rim/contrast/DOF.

### F. Fake Four-Layer Depth / Vertical Dead Zone
> Rebuild observable L1/L2/L3/L4 depth. In exact 9:16, continue designed material/light recession upward; do not leave a large blurred wall or empty upper field.

### G. Surface State Drift
> Restore source browning/char/doneness/gloss/moisture/sauce/crust intensity. Improve only photography.

Retry diagnosed failure only; do not random-regenerate correct regions.