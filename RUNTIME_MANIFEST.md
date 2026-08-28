# PP-food-001 Runtime Manifest

本文件是 Stage A 的 **P0 唯一运行真相源**。其他文件可以解释、举例、扩展，但不得重新定义或削弱以下规则。

## P0. Source Truth

```text
SOURCE_TRUTH = CURRENT_USER_IMAGE
```

原图可见像素是真实产品真相。用户明确提供的菜名/品类信息可以帮助语义路由，但不能覆盖原图食材、器皿、摆盘、排列和物理关系。

未知区域只允许 Minimum Plausible Continuation，不得借扩图重做主体。

## P1. Default Output

```text
DEFAULT_ASPECT_RATIO = 9:16
```

横图、方图、竖图都默认输出 9:16。适配优先级：画布延展 > 背景重构 > Controlled Hero Reframe。禁止拉伸、压缩、裁坏关键产品或重做产品适配画幅。

## P2. A / B Intent Router

```text
1. Explicit A → Stage A only
2. Explicit B → Stage A → Stage A QC → Stage A PASS → Stage B
3. No A/B + obvious KV business info → B, but still Stage A first
4. Otherwise → A
```

明显商业信息：产品/菜名、品牌/店铺、主副标题、地址、电话、价格、核心食材、卖点、新品/活动等。

```text
EXPLICIT_A_OVERRIDES_AUTO_B = TRUE
B_CAN_SKIP_STAGE_A = FALSE
```

## P3. Current Job Isolation

每张新上传图创建新的 `CURRENT_JOB_FACTS`。

当前任务只允许使用：当前图可见事实、当前用户明确提供的信息、当前任务已验证的中间产物。

除非用户明确要求沿用，上一任务的品牌、产品名、食材、口味、地址、电话、Slogan、文案、场景事实和视觉皮肤全部失效。

## P4. Runtime Roles

`VISION_MODEL`：识图、Fidelity Manifest、品类/温度/语义路由、生成后 Fidelity/Semantic/Hero QC。

`IMAGE_MODEL`：必须支持 reference-image editing / image-to-image；接收真实参考图并执行高保真商拍。

默认宿主模型无视觉时禁止猜图。

## P5. Fidelity Hard Gate

```text
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container Identity >=98
Plating / Arrangement >=95
Physical Relationship Fidelity >=95
Photography >=85
Semantic Relevance >=85
Hero Spatial Score >=85
Appetite Score >=85
NO CRITICAL FAILURE
NO HERO_SPATIAL_CRITICAL_FAILURE
```

不可牺牲顺序：

```text
Food Identity
> Major Ingredient Identity
> Ingredient / Product Geometry
> Vessel / Packaging / Direct Support
> Physical Relationships
> Plating / Arrangement Topology
> Sauce / Oil / Broth / Cream / Ice / Crust State
> Visible Count / Overlap
> Material Realism
> Color
> Composition
> Lighting
> Background
> Props
> Atmosphere
```

冲突时：

```text
REDUCE_DESIGN_AGGRESSION = TRUE
REDUCE_FIDELITY = NEVER
```

## P6. Subject + Direct Support Lock

必须锁定：产品身份、主辅食材/材质、几何、数量关系、器皿/包装、摆盘/阵列拓扑、表面状态、手持/餐具/托盘/烘焙纸等**直接承载与物理关系**。

禁止：加减/替换主要食材、换器皿、重画包装、重摆盘、移动/删除/复制/重排产品、把产品标准化成“另一份更漂亮的同类食品”。

Stage A Prompt 前部必须是强硬具体锁定，不接受仅写“参考原图”“保持一致”。

## P7. Hero Stage + Scene Context Precedence

Stage A 是高级材质舞台上的 Food Hero，不是默认真实经营场所，也不是普通门店照片的清洁升级。

优先级：

```text
Food DNA / Direct Support
> World-Class Hero Stage
> Category Semantic Translation
> Generic Source Venue Appearance
```

```text
HERO_STAGE_OVERRIDES_GENERIC_VENUE_CONTEXT = TRUE
DIRECT_SUPPORT_RELATION_LOCKED = TRUE
GENERIC_VENUE_CONTEXT_LOCKED = FALSE_BY_DEFAULT
```

例外：包装零售货架、品牌/标签展示结构、手持关系或用户明确要求保留的场所，才可视为 identity-critical context。

普通开放式面包/甜点展示柜中的柜体、墙面、店内空间不是默认 Food DNA；可以在保留产品与原托盘/直接承载关系的前提下转译成品类原生高级材质舞台。

必须：
- 从当前食品属性推导材质、色彩、温度、光线和身份锚点；
- 建立可观察的 L1 / L2 / L3 / L4 四层空间；
- L4 至少有两个可感知的后退材质/光影线索；单一虚墙/渐变/bokeh 不算；
- Hero 处于明确 light pool；
- rim / brightness / temperature separation 雕刻主体；
- 环境道具低对比、虚化、品类相关，不靠通用道具包冒充高级；
- 冷食零热蒸汽，热食仅克制且物理合理；
- 食欲感来自真实材质，不来自塑料高光、过饱和或浓烟。

## P8. Controlled Hero Reframe

```text
CONTROLLED_HERO_REFRAME_ALLOWED = TRUE
SOURCE_CAMERA_COORDINATES_ARE_FOOD_DNA = FALSE
```

允许：9:16 扩图、裁切、构图重组、焦段感调整、轻到中度机位高度/俯仰调整、光学主次重建。

必须锁定：产品可见面比例、几何、数量、排列、重叠顺序、直接承载面、可信透视和器皿/托盘形态。

禁止：极端低机位、极端广角、生成源图未支持的新侧面、旋转成全新视角、为构图改变产品数量或位置。

目标：

> **锁产品视图几何，不锁偶然的随手拍相机坐标。**

## P9. Multi-Product Hero Hierarchy

多产品场景必须：

```text
MULTI_PRODUCT_HERO_HIERARCHY_REQUIRED = TRUE
```

从原图已存在的前景单体或小簇选：

```text
PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER
```

其余保持不变，作为：

```text
SUPPORTING_PRODUCT_FIELD
```

只能通过 light pool、局部锐度、rim、对比、景深、负空间和受控 reframe 建立层级；不得移动、删除、复制、缩放或重排产品。

如果画面首先读成库存/展示陈列而非 Hero，Hero Spatial FAIL。

## P10. Stage B Handoff

任何 B 请求：

```text
CURRENT_STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
```

不得让 Stage B 回退原始随手拍，也不得引用上一任务图片。

## P11. Targeted Retry

失败先诊断再修正，不随机整张重抽。

典型类型：Ingredient / Vessel / Plating / Physical Relationship / Weak Photography / Generic Background / Temperature / Excessive Effect / Scene Integration / Generic Display Case / Camera Too Conservative / Multi-Product Inventory Look / Fake Four-Layer Depth / Wrong Category Material Language / 9:16 Composition。

最多逐级收紧到 Attempt 3 Ultra-Conservative Subject Mode。宁可降低危险的摄影戏剧性，也不允许产品漂移；但不得因为保真就退化成普通随手拍/门店展示照。

## P12. Capability Evidence + Runtime Profile

静态 schema、宿主能力说明、连接存在只能证明：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
```

只有真实调用链成功，或存在与当前非秘密配置 fingerprint 匹配的已验证 Runtime Profile，才能证明：

```text
RUNTIME_CAPABILITIES_VERIFIED = PASS
```

若静态配置完整但没有匹配 profile：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

允许进入 READY，但不得声称已端到端验证。

第一次真实业务调用兼任验证，不额外生成无业务价值测试图。验证成功后可把 profile 保存在宿主私有持久状态；fingerprint 不变时跨会话复用。

## P13. Fail Closed

以下任一项无法确认：

```text
PRODUCTION_GATE = BLOCKED
```

- Mandatory Read 未完成；
- Pre-flight 未通过；
- `RUNTIME_CAPABILITIES_DECLARED != PASS`；
- VISION_MODEL 不能读图；
- IMAGE_MODEL 不支持参考图编辑；
- Credential 未就绪；
- 图片输入/输出不能被正确传递；
- 当前 Execution Contract 未建立；
- Hero Reframe / Multi-Product Plan 未建立或明确 N/A；
- 规则文件存在未解决冲突。

`RUNTIME_CAPABILITIES_VERIFIED = PENDING` 本身不是配置缺失；它表示首次真实任务需要在交付前完成 live verification。

## P14. Repository Security Boundary

仓库只保存通用能力约定和变量名，不保存具体供应商名、私有聚合平台名、实际 API Base URL、API Key、私有凭据或 Runtime Profile 真实运行值。

## P15. Runtime State

```text
SETUP_GATE
→ READY_WAITING_FOR_START
→ user says 启动
→ PRODUCTION
```

READY 时必须准确报告：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
RUNTIME_CAPABILITIES_VERIFIED = PASS / PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE / FALSE
```

连接失效、profile fingerprint 不匹配或能力变为 UNKNOWN/MISSING 时，退回 SETUP_GATE，只修复缺失项。