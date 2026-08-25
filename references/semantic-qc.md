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
- 货架商品被语义路由移到餐厅桌面；
- 街边小吃被改成不合理的西式豪华餐厅；
- 冷饮出现热气；
- 清鲜菜品被强行加入浓烟/暗红火锅氛围；
- 背景道具进入主菜并造成新增食材；
- 为呼应菜名而改变主菜配料、摆盘或器皿；
- 背景仍完全是与大量其他菜通用的无差别模板，且用户已给出明确菜品语义。

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
No Fidelity Critical Failure
No Semantic Critical Failure
```

语义背景做得再准确，只要食物身份、器皿、摆盘或主要食材发生明显漂移，仍然失败。

## 8. 定向重试

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
