# PP FOOD｜执行A：高保真商业美食摄影 Canonical SOP

> 快捷指令：`执行A` / `A`
>
> 角色：Stage A / Commercial Re-photography Engine
>
> 目标：把用户上传的真实美食、饮品、烘焙、包装食品随手拍，升级成严格 9:16、世界级商业摄影 Hero 图，同时最大限度锁定当前产品 DNA。

## 0. Authority

本文件是 **A 任务的操作 SOP**，用于跨智能体复现当前稳定工作方式。

执行时必须同时遵守：

```text
RUNTIME_MANIFEST.md                 # P0 单一事实源
SKILL.md                            # Stage A 角色与硬门槛
REQUIRED_READ_SET.md                # 必读/条件加载
PRE_FLIGHT_CHECKLIST.md             # 生产门禁
EXECUTION_CONTRACT_TEMPLATE.md      # 当前任务合同
references/*                        # 详细方法
```

如本 SOP 与 `RUNTIME_MANIFEST.md` 冲突，以 `RUNTIME_MANIFEST.md` 为准并 Fail Closed，不自行挑规则。

---

# 1. 用户触发协议

用户上传图片并说：

```text
执行A
```

默认含义：

- 只做 Stage A 商拍；
- 不做 KV；
- 不要求主标题、副标题；
- 不追问营销文案；
- 默认最终成片严格 9:16；
- 直接执行当前产品的高保真商业重拍。

如果用户额外给出菜名、产品名、品牌、风味、品类、想要的氛围，这些用于 **语义路由与背景设计**，不得用于擅自重做产品。

无 A/B 且没有明显商业海报信息时，默认按 A 处理。

---

# 2. 双模型职责

## VISION_MODEL

负责：

- 读取当前用户上传图片；
- 建立 `CURRENT_JOB_FACTS`；
- Food DNA / Fidelity Manifest；
- Surface State Manifest；
- 食品品类、场景、语义路由；
- Topology Completion 判断；
- 生成后 Fidelity / Semantic / Hero / Appetite / Aspect QC。

如果宿主默认模型不识图：

> **禁止猜图，必须显式调用 VISION_MODEL。**

## IMAGE_MODEL

负责：

- 真正接收当前用户图片作为 reference；
- 执行 image editing / image-to-image；
- 锁定产品并完成商业摄影升级；
- 输出当前任务 Stage A 图。

“IMAGE_MODEL 能参考图出图”不能替代前置视觉分析与后置 QC。

---

# 3. Source Truth｜源图事实优先

优先级：

```text
1. 当前用户图可见事实
2. 用户明确说明
3. VISION_MODEL 当前图推断
4. 品类常识
5. 审美偏好
```

核心原则：

> **Source pixels override assumptions.**

未知/裁切区域只允许 `Minimum Plausible Continuation`。

不得因为“这类食物通常应该有”而添加原图不存在的肉、虾、芝士、香草、果粒、装饰、器皿或包装元素。

---

# 4. 出图前必须建立 Manifest

至少形成：

```text
MAIN_SUBJECT
FOOD_CATEGORY
DISH_OR_PRODUCT_NAME
SCENE_TYPE
VESSEL_OR_PACKAGE
SHAPE / GEOMETRY
SOURCE_SURFACE_STATE
MAIN_INGREDIENTS
SECONDARY_INGREDIENTS
GARNISH
COLOR_DISTRIBUTION
PLATING_TOPOLOGY
PHYSICAL_RELATIONSHIPS
CRITICAL_IDENTITY_FEATURES
SEMANTIC_ROUTE
ROUTING_CONFIDENCE
```

同时按当前版本建立：

```text
SURFACE_STATE_MANIFEST
TOPOLOGY_COMPLETION_PLAN
PRODUCT_DERIVATION_EVIDENCE >= 3
BACKGROUND_BIG_IDEA
BACKGROUND_ARCHITECTURE_PLAN
HERO_REFRAME_PLAN
MULTI_PRODUCT_HERO_PLAN (if applicable)
```

Manifest 只在后台使用，不要求用户填写 JSON。

---

# 5. 五大硬锁

感知验收目标：

```text
Food Identity >= 95
Ingredient Geometry >= 95
Vessel / Container >= 98
Plating Topology >= 95
Physical Relationship >= 95
```

必须锁住：

- 食品/商品身份；
- 主食材与清晰可见辅料；
- 形状、厚薄、切法、卷曲、朝向、堆叠、数量关系；
- 器皿、瓶、罐、袋、盒、标签与包装结构；
- 上下/前后/中心边缘摆盘拓扑；
- 手持、筷子、刀叉、托盘、货架、展示柜等直接物理关系。

## Source Surface State Lock

必须锁住源图实际：

- 基础颜色；
- 火候/熟度；
- 焦化/烘烤程度；
- 油亮/湿润等级；
- 酱汁覆盖；
- 裂纹/割口；
- 奶油/糖霜状态；
- 冷凝/透明度。

> **食欲升级来自摄影读取能力，不来自重新烹饪产品。**

---

# 6. Region Edit Budget

## Region A｜Subject Core

修改预算：**极低**。

允许：曝光、白平衡、已有材质显现、受控高光、真实阴影、轻微清理。

禁止：重做主体、换食材、增减份量、改火候、重新摆盘、换器皿、重设计包装。

## Region B｜Direct Support

修改预算：**低到中**。

包括：手、餐具、托盘、与主体直接接触的支撑区域。

## Region C｜Environment

修改预算：**高**。

主要创意发生在：背景、远桌面、空间材质、光影切面、前中后景、设计型负空间。

---

# 7. World-Class Background Architecture

执行A不是“食物 + 普通高级背景”。

必须满足：

```text
PRODUCT_DERIVED_STAGE > GENERIC_PREMIUM_STYLE
BACKGROUND_ARCHITECTURE > PROP_STYLING
ONE_BIG_STAGE_IDEA > MANY_DECORATIVE_OBJECTS
```

背景必须从当前产品本身推导，建立：

- 至少 3 条 `PRODUCT_DERIVATION_EVIDENCE`；
- 一个明确 `BACKGROUND_BIG_IDEA`；
- 2–3 个主材质平面/体块；
- 近 / 中 / 深空间质量；
- 台面高差与遮挡；
- light cut / shadow architecture；
- reflective vs absorptive material relationship；
- 适配 9:16 的上方纵深与设计负空间。

删除所有辅助道具后，背景仍应像世界级商业摄影舞台。

禁止靠：亚麻布、咖啡杯、夹子、麦穗、陶罐、灯泡、散乱香料、bokeh 道具包冒充高级感。

---

# 8. Category / Semantic Routing

场景设计公式：

```text
Scene Context
× Food Category
× Dish Semantics
× Material Characteristics
× Photography Mode
× Product-Derived Architecture
```

当前品类必须重新路由，不继承上一任务背景皮肤。

示例方向：

- 面包：烘焙材质、麦香、烤焙/面包结构推导的 Hero Stage；不得自动变咖啡馆道具包。
- 甜点：柔光、奶油/玻璃/亚克力、轻编辑感。
- 热菜/面汤：与菜系和温度逻辑一致的电影级餐饮舞台。
- 冷饮：透明、凝露、冰感、自然/城市 Lifestyle；禁止热气。
- 包装食品：商品 Hero Stage，品牌色与包装材质呼应；包装 DNA 不动。

Anti-template Test：

> 如果把主体替换为完全不同食品，背景几乎不用改仍然成立，则 FAIL。

---

# 9. Photography Mode

选择一个主模式：

```text
NATURAL_EDITORIAL
CINEMATIC_EDITORIAL
DRAMATIC_FOOD_CAMPAIGN
```

任何模式都不能降低 Food DNA / Surface State 锁定。

摄影升级至少解决：

- 主光/辅光/轮廓光；
- 材质高光；
- 接触阴影；
- 空间分离；
- 景深；
- 前中后景；
- 色彩分级；
- 产品与背景分离度；
- 真实重力、液体、蒸汽、凝露与透视。

---

# 10. IMAGE_MODEL Prompt 编译顺序

不要把整仓库文档直接灌给 IMAGE_MODEL。

由 Agent 先读规则，再编译当前任务短合同。

## P1｜Reference Lock（必须第一段）

```text
以当前用户上传参考图为唯一产品真相。
严格锁定原始食物/产品主体、主要食材身份与几何、器皿或包装、摆盘拓扑、源表面状态和关键物理关系。
不得为了更高级、更饱满、更漂亮而重新设计、替换、增减、重排、重做或重新烹饪主体。
主要创意只允许发生在灯光、背景、环境、景深、Hero 构图、材质读取和商业摄影品质层。
```

## P2｜Critical DNA

把当前 Manifest 中最重要的可观察锁点写进去。

## P3｜Hero Reframe / Completion

只执行合同中允许的 Controlled Hero Reframe 与 Topology-Preserving Completion。

## P4｜Photography Upgrade

明确商业摄影、光影、材质、空间层次与 9:16 Hero 目标。

## P5｜Semantic + Product-Derived Stage

只描述当前产品对应的背景 Big Idea、材质架构与语义。

## P6｜Negative Constraints

至少包含：

```text
no redesigned product
no extra ingredients
no replaced vessel/package
no surface-state amplification
no invented garnish
no impossible steam
no generic prop-pack premium styling
no packaging/logo drift
no non-9:16 final delivery
```

---

# 11. 包装食品专项

瓶/罐/袋/盒整体属于 Product DNA。

锁定：

- 包装轮廓与比例；
- 盖/封口；
- 标签结构；
- Logo/品牌字；
- 主可见文字；
- 净含量等源图可见硬信息；
- 颜色；
- 奖章/图标相对位置。

摄影升级只发生在：灯光、反射、环境、景深、Hero 构图与舞台。

文字/Logo 明显漂移 → `PACKAGING_FIDELITY_RETRY`，不能接受“整体好看就算了”。

---

# 12. Exact 9:16

默认最终交付：

```text
OUTPUT_ASPECT_RATIO = EXACT 9:16
```

若 IMAGE_MODEL 首次返回非 9:16：

- 不交付；
- 做 canvas correction / outpaint / targeted retry；
- 不得拉伸产品；
- 不得裁坏产品；
- 不得为了适配比例重做主体。

---

# 13. QC

生成后 VISION_MODEL 必须检查：

```text
Aspect Ratio = EXACT 9:16
Food Fidelity >=95
Vessel Fidelity >=98
Source Surface State = PASS
Product Derivation Evidence >=3
Background Big Idea = PASS
Background Architecture = PASS
Photography >=85
Semantic >=85
Hero Spatial >=85
Appetite >=85
No Critical Failure
```

## Critical Fail Examples

- 食物变成“类似但不是同一份”；
- 主要食材/包装/器皿漂移；
- 源表面状态被重新烹饪；
- 背景只是普通店内/通用高级图库；
- 道具包替代背景架构；
- 非 9:16；
- 冷品冒热气；
- 包装文字/Logo 严重重绘。

---

# 14. Targeted Retry｜禁止随机重抽

失败后只修当前失败项：

```text
Food drift               → REFERENCE_LOCK_RETRY
Surface-state drift      → SURFACE_STATE_RETRY
Vessel/package drift     → VESSEL_OR_PACKAGING_RETRY
Weak hero composition    → HERO_REFRAME_RETRY
Generic background       → BACKGROUND_ARCHITECTURE_RETRY
Semantic mismatch        → SEMANTIC_ROUTE_RETRY
Physical realism         → PHYSICS_RETRY
Wrong aspect ratio       → ASPECT_CORRECTION_RETRY
```

不得因为某一处失败就随机把整张换成另一套产品和背景。

---

# 15. 执行A结束条件

只有 Stage A QC PASS，才允许交付为 A 成片，或作为 B 的 Stage A Bridge 输入。

最终心法：

> **The current user image is the real product, not creative raw material.**
>
> **Preserve the product physically. Reveal appetite through photography. Build a product-derived world-class stage. Change the photography, not the product.**