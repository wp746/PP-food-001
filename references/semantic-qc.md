# Semantic Background Quality Control

本文件用于生成后检查：背景、环境、色彩、道具和摄影气质是否真正与菜品语义匹配。

高保真主体通过并不代表整张图完成。V5 要求同时满足：

> **High Fidelity + High Photography Upgrade + High Semantic Relevance**

## 1. 评分维度

总分 100。

### Semantic Relevance / 30

背景是否明显服务于当前这道菜，而不是通用模板？

### Cuisine Alignment / 20

环境是否符合用户提供或高置信度推断出的菜系/地域餐饮气质？

### Flavor Atmosphere Match / 20

视觉气质是否与风味一致，例如鲜麻、清鲜、红油麻辣、炭火、清凉、甜感等？

### Prop Relevance / 10

辅助道具是否少量、相关、弱化，且没有让人误以为菜品新增配料？

### Color Direction Match / 10

环境色是否支持菜品语义，同时保护真实食物颜色？

### Non-Template Diversity / 10

是否避免了无论什么菜都使用相同的深木桌、暖琥珀灯、陶罐和烟雾？

## 1.5 Hero Spatial Score（独立必检项，V5.2 新增）

按 `hero-shot-mandate.md` 单独评分，**不并入上述 100 分制**，独立门槛：

```text
Hero Spatial Score >= 85 才通过
```

检查项：

1. 四层景深是否齐全（前景 / 中景光池 / 中后景材质器物 / 远景纵深）？
2. 虚化是否连续递进，而非「主体清晰 + 背后一刀切虚」？
3. 主体是否坐在光池内、被轮廓光雕刻、与背景有亮度或色温分离？
4. 环境是否为高级材质舞台——材质、色彩、作料围铺指向这道菜的身份（而非某个场所）？
5. 背景是否**完全没有**真实场所结构（门头/招牌/街道/店内/就餐区/门窗）？
6. 温度逻辑是否正确（冷食零热气冷调 / 热食暖调克制蒸汽）？
7. 工业级商拍质量——主体锐度、材质可信度、光影物理是否达到投放标准？

低于 85 时按 `hero-shot-mandate.md` §7 的定向方向重试，不要随机重抽。

## 1.6 Appetite Score（独立必检项，V5.3 新增）

按 `hero-shot-mandate.md` §8 单独评分，**不并入上述 100 分制**，独立门槛：

```text
Appetite Score >= 85 才通过
```

检查项：

1. 油脂光泽——红油/酱汁是否有镜面高光，而不是哑光发死？
2. 湿润度——汤汁浸润、水珠、酱料包裹感是否可读？
3. 微距质感——芝麻、辣椒碎、蒜末等细节是否在景深内清晰？
4. 温度可视化——热食蒸汽 / 冷食冷凝是否正确且克制？
5. 色彩饱和管理——食物主色是否透亮鲜活（红油红得发光，绿叶不发灰）？
6. 「刚做好」状态——是否像刚从厨房端出来的下一秒，而不是摆了半小时？

终审判据：**这张图能否让观者在 3 秒内产生「想吃」的生理反应？**

低于 85 时按 `hero-shot-mandate.md` §8 重写食欲渲染指令后定向重试，不要随机重抽。

## 2. 通过门槛

```text
95–100  Excellent / 菜品专属感非常强
90–94   Strong
85–89   Pass
<85     Retry
```

若存在 Semantic Critical Failure，则无论总分多少都必须重试。

## 3. Semantic Critical Failures

以下任意一项直接失败：

- 用户明确提供菜名，但背景明显按另一种菜系设计；
- 用户明确说青花椒/鲜麻类，但画面被处理成红油麻辣模板；
- **食材 DNA 漂移（最高级失败，V5.3 升格）**：主体身份/几何/器皿/摆盘/物理关系发生任何改变——整图判废，无论其他分数多高；
- 货架商品被语义路由移到餐厅桌面；
- 冷饮出现热气；
- 清鲜菜品被强行加入浓烟/暗红火锅氛围；
- 背景道具进入主菜并造成新增食材；
- 为呼应菜名而改变主菜配料、摆盘或器皿；
- 背景仍完全是与大量其他菜通用的无差别模板，且用户已给出明确菜品语义；
- **平背景 / 背景板**：主体贴墙、无景深分层、无纵深递进，空间层次缺失（Hero Shot Mandate 硬规则）；
- **真实场所污染（V5.3 新增）**：画面出现可识别经营场所结构——门头、招牌、街道、店内就餐区、门窗、柜台服务场景；
- **空间结构在但材质与食物无关**：四层景深齐全但舞台材质不属于这道菜的调性；
- **作料围铺喧宾夺主**：围铺元素虚化不足、抢主体、或可被误读为菜里加料；
- **食欲感缺失（V5.3 新增）**：食物干涩、发暗、无光泽、无湿润度——看起来「不好吃」即为 Critical Failure。

## 4. 用户信息一致性检查

如果用户提供：

```text
dish_name
cuisine_type
flavor_profile
main_highlights
```

则逐项检查最终视觉是否与这些信息一致。

用户信息是语义设计的最高优先级事实。

## 5. 自动推断一致性检查

如果菜名由系统推断：

- 高置信度可以使用具体语义；
- 中置信度应使用品类级语义；
- 低置信度不应出现过度具体的地域符号或配料暗示。

不要让低置信度猜测变成强势背景事实。

## 6. 反模板检查

问三个问题：

1. 这个背景为什么适合当前菜品？
2. 背景中至少有哪些色彩、材质、环境或光线决定是由当前菜品语义驱动的？
3. 如果换成草莓蛋糕、寿司或奶茶，这套背景是否仍然几乎无需变化？

如果第 3 问答案是“是”，则 Non-Template Diversity 不应通过。

## 7. 与 Fidelity QC 的关系

Semantic QC 不能覆盖主体保真要求。

最终通过条件：

```text
Fidelity Score >= 95
Photography Score >= 85
Semantic Score >= 85
Hero Spatial Score >= 85
Appetite Score >= 85
No Fidelity Critical Failure
No Semantic Critical Failure
```

语义背景做得再准确，只要食物身份、器皿、摆盘或主要食材发生明显漂移，仍然失败。

## 8. 定向重试

### 平背景 / 空间层次缺失（V5.2 新增）

追加：

> The current background reads as a flat backdrop. Rebuild the environment as a real three-dimensional place with four depth layers: defocused foreground dressing, the hero dish inside a light pool, softly blurred premium material objects (stoneware, dark wood, matte metal) half a meter behind, and layered premium darkness with clean negative space above. Keep the food subject completely unchanged.

### 真实场所污染（V5.3 新增）

追加：

> The background contains real-venue structures (storefront / signage / street / restaurant interior / doors / windows). Remove all venue semantics from the scene: rebuild the environment purely from premium materials — stone, ceramic, wood, metal, fabric — with no identifiable place. Keep the food subject completely unchanged.

### 食欲感缺失（V5.3 新增）

追加：

> The food renders dry, dull and unappetizing. Re-render the existing appetizing properties (glossy oil sheen, sauce cling, moisture droplets, macro texture legibility, translucent color glow) with stronger rim light and specular control. Do not invent properties that do not exist in the source. Keep the food subject completely unchanged.

### 空间在但语境错位（V5.2 新增，V5.3 修订）

追加：

> The space has depth but does not belong to this dish. Re-route the stage materials to match the food's own category, cuisine and temperament (e.g. cold noodle dish on dark basalt with cool key light and chili-oil dressing). Keep the four-layer spatial structure and keep the food subject completely unchanged.

### 背景过于通用

追加：

> The current environment is too generic. Redesign only the background and lighting so they are specifically informed by the known dish identity, cuisine, flavor profile and material character. Keep the food subject completely unchanged.

### 菜系不匹配

追加：

> Restore semantic alignment with the explicitly provided cuisine/dish information. Change only environment, supporting props, color direction and lighting atmosphere. Do not modify the food.

### 风味气质不匹配

追加：

> Adjust the environmental mood to reflect the actual flavor profile without adding ingredients or changing the dish. The flavor character should be communicated through light, color, setting and restrained contextual cues only.

### 道具过多

追加：

> Remove unnecessary semantic props. Keep at most a few subtle, softly defocused, contextually relevant supporting elements. The food must remain the sole hero subject.

### 颜色抢主体

追加：

> Reduce environmental color dominance. Preserve accurate food color and use semantic colors only as restrained supporting accents in the environment.
