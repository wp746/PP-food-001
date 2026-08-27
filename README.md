# PP-food-001

Stage A 高保真美食商业摄影 Skill。把用户随手拍升级成 9:16 电影级 / 商业广告级 Hero Shot，同时严格锁定 Food DNA。

当前版本：**5.5.0**

## 默认行为

```text
A = Stage A 商拍
B = 先完成 Stage A，再交给 PP-food-KV-001 做 Stage B
未说 A/B 且无明显商业信息 = 默认 A
未说 A/B 但提供产品名、店铺、标题、地址、价格、卖点等 KV 商业信息 = 自动 B
DEFAULT_ASPECT_RATIO = 9:16
```

显式 A 优先于自动 B。任何 B 都不得跳过 Stage A。

## 核心原则

> **Source truth first. Lock the product. Upgrade only the photography and environment.**

必须锁定：产品身份、主食材、食材几何、器皿/包装、摆盘拓扑、酱汁/红油/汤体状态、物理关系与主要数量关系。

目标：

```text
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container >=98
Plating >=95
Physical Relationship >=95
Photography >=85
Semantic Relevance >=85
Hero Spatial >=85
Appetite >=85
```

## 9:16 规则

无论原图横竖，默认输出 9:16。通过画布延展、背景重构和镜头重组适配；禁止拉伸、压扁、裁掉关键产品区或为了竖版重做产品。

## 商拍方法

Stage A 的创意主要发生在背景、灯光、景深、材质与调色。背景必须由当前食品属性和品类语义推导，避免所有食品套同一深木/暖灯模板。

高级商拍使用材质舞台和四层景深：前景弱虚化 → Hero Food → 中背景 → 深背景。产品始终是唯一视觉英雄。

## 双 Skill 链路

```text
原图
→ VISION_MODEL / Food DNA
→ PP-food-001 Stage A
→ Stage A QC
→ A: 交付商拍图
→ B: Stage A PASS 图作为唯一 Stage B 参考图
→ PP-food-KV-001
```

## 运行环境

首次安装读取 `HANDOFF.md`。仓库只保存通用能力约定；不要把具体供应商、模型服务 URL、API Key 或聚合平台配置写进 Skill。凭据由宿主 Secret / Environment / Connection 管理。

## 关键参考

- `references/fidelity-manifest.md`
- `references/fidelity-qc.md`
- `references/hero-shot-mandate.md`
- `references/dish-semantic-router.md`
- `references/cuisine-style-map.md`
- `references/semantic-background-rules.md`
- `references/retry-policy.md`

详细执行以 `SKILL.md` 为准。
