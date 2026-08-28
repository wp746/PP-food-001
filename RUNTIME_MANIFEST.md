# PP-food-001 Runtime Manifest

本文件是 Stage A 的 **P0 唯一运行真相源**。其他文件可以解释、举例、扩展，但不得重新定义或削弱以下规则。

## P0. Source Truth

```text
SOURCE_TRUTH = CURRENT_USER_IMAGE
```

原图可见像素是真实产品真相。用户明确提供的菜名/品类信息可以帮助语义路由，但不能覆盖原图食材、器皿、摆盘、排列、表面状态和物理关系。

未知区域只允许 Minimum Plausible Continuation，不得借扩图重做主体。

## P1. Stage A Output Contract — Exact 9:16

```text
DEFAULT_ASPECT_RATIO = 9:16
OUTPUT_ASPECT_RATIO_EXACT = 9:16
NON_9_16_DELIVERY = CRITICAL_FAILURE
```

无论源图横图、方图、竖图，Stage A 最终交付都必须是**严格 9:16 竖版画布**。

适配优先级：

```text
canvas extension
> background reconstruction
> Controlled Hero Reframe
> high-confidence Topology-Preserving Completion
```

禁止：拉伸、压缩、裁坏关键产品、重做产品适配画幅。

如果 IMAGE_MODEL 第一次返回非 9:16：**不得交付**。必须通过 canvas correction / outpaint / targeted retry 修正到严格 9:16，并继续锁住产品。

## P2. A / B Intent Router

```text
1. Explicit A → Stage A only
2. Explicit B → Stage A → Stage A QC → Stage A PASS → Stage B
3. No A/B + obvious KV business info → B, but still Stage A first
4. Otherwise → A
```

```text
EXPLICIT_A_OVERRIDES_AUTO_B = TRUE
B_CAN_SKIP_STAGE_A = FALSE
```

## P3. Current Job Isolation

每张新上传图创建新的 `CURRENT_JOB_FACTS`。当前任务只允许使用：当前图可见事实、当前用户明确提供的信息、当前任务已验证的中间产物。

上一任务的品牌、产品名、食材、口味、地址、电话、Slogan、文案、场景事实和视觉皮肤默认全部失效，除非用户明确要求沿用。

## P4. Runtime Roles

`VISION_MODEL`：识图、Fidelity Manifest、Surface State Manifest、Completion Confidence、品类/温度/语义路由、Background Architecture Plan、生成后 Fidelity/Semantic/Hero/Aspect QC。

`IMAGE_MODEL`：必须支持 reference-image editing / image-to-image；接收真实参考图并执行高保真商拍。

默认宿主模型无视觉时禁止猜图。

## P5. Fidelity Hard Gate

```text
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container Identity >=98
Plating / Arrangement >=95
Physical Relationship Fidelity >=95
Source Surface / Material State = LOCKED
Photography >=85
Semantic Relevance >=85
Hero Spatial Score >=85
Appetite Score >=85
Output Aspect Ratio = EXACT 9:16
NO CRITICAL FAILURE
NO HERO_SPATIAL_CRITICAL_FAILURE
```

不可牺牲顺序：

```text
Food Identity
> Major Ingredient Identity
> Ingredient / Product Geometry
> Source Surface / Material / Cooking State
> Vessel / Packaging / Direct Support
> Physical Relationships
> Plating / Arrangement Topology
> Sauce / Oil / Broth / Cream / Ice State
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

## P6. Surface / Material State Lock — All Categories

```text
SOURCE_SURFACE_STATE > APPETITE_ENHANCEMENT
```

所有品类必须锁定原图已有的：基础颜色与梯度、烘烤深浅、焦化程度、熟度、油亮/哑光等级、湿润度、酱汁/油覆盖、脆壳/皮肤状态、裂纹/割口、奶油/糖霜、冷凝/冰霜、透明度等可见状态。

商拍允许通过曝光、显色、光位、镜面高光控制、微对比、纹理解析和色彩分级让这些属性**更清楚**；不允许把属性本身**变得更强**。

```text
REVEAL_EXISTING_PROPERTY = YES
AMPLIFY_PROPERTY_BEYOND_SOURCE = NO
```

任何输出若看起来像“同类食品，但火候/熟度/表皮/酱汁状态明显不同的一批产品”，直接 Fidelity FAIL。

## P7. Topology-Preserving Completion

当源图因裁切、取景或装盘边缘没有拍全时，允许补全，但只允许补全**同一份产品/同一器皿/同一摆盘拓扑**。

```text
HIGH → natural continuation allowed
MEDIUM → minimum conservative continuation only
LOW / UNKNOWN → do not invent product content
```

补全必须延续：食材身份、几何/切法、尺度、方向、层级、重叠、密度、数量关系、表面状态、酱汁/油/汤体状态、容器/承载关系。

```text
COMPLETE_THE_SAME_SERVING = TRUE
DESIGN_A_BETTER_SERVING = FALSE
```

低置信度时优先环境延展、裁切调整或自然遮挡，不强行补产品。

## P8. Subject + Direct Support Lock

必须锁定：产品身份、主辅食材/材质、几何、数量关系、器皿/包装、摆盘/阵列拓扑、表面状态、手持/餐具/托盘/烘焙纸等直接承载与物理关系。

禁止：加减/替换主要食材、换器皿、重画包装、重摆盘、移动/删除/复制/重排产品、把产品标准化成“另一份更漂亮的同类食品”。

Stage A Prompt 前部必须是强硬具体锁定，不接受仅写“参考原图”“保持一致”。

## P9. Hero Stage + Scene Context Precedence

```text
Food DNA / Source Surface State / Direct Support
> World-Class Hero Stage
> Category Semantic Translation
> Generic Source Venue Appearance
```

普通开放式展示柜中的柜体、墙面、店内空间不是默认 Food DNA；可以在保留产品与原托盘/直接承载关系的前提下转译成品类原生高级材质舞台。

必须建立可观察的 L1 / L2 / L3 / L4 四层空间；L4 至少有两个可感知的后退材质/光影线索；Hero 处于明确 light pool。

Hero / Appetite 只能提升摄影表现，不能覆盖 P6 Surface State Lock。

## P10. Background Architecture — All Categories

```text
BACKGROUND_ARCHITECTURE > PROP_STYLING
CATEGORY_MATERIAL_LOGIC > GENERIC_PREMIUM_PROPS
```

每个 Stage A 任务必须建立 `BACKGROUND_ARCHITECTURE_PLAN`，至少包含：

```text
category_material_logic
food-derived_color_logic
primary_material_planes = 2-3
near / mid / deep spatial masses
height / depth variation
occlusion relationship
light-cut / shadow architecture
reflective-vs-absorptive material relationship
negative-space zone
props = OPTIONAL / subordinate
```

**删除所有辅助道具后，背景仍必须像世界级商业摄影舞台。**

以下情况直接 Background / Hero FAIL：
- 主要依赖亚麻布、夹子、杯子、陶罐、麦穗、香料碟、灯泡等道具制造高级感；
- 去掉道具后只剩普通木柜、虚墙或空背景；
- 材质只作为小物件出现，没有形成空间平面/体块；
- 背景没有台面高差、前后遮挡、材质反射差和光影切面；
- 换成完全不同食品，背景仍几乎无需改变。

道具可为 0；背景高级感必须首先来自**空间建筑 + 材质 + 光影**。

## P11. Controlled Hero Reframe

```text
CONTROLLED_HERO_REFRAME_ALLOWED = TRUE
SOURCE_CAMERA_COORDINATES_ARE_FOOD_DNA = FALSE
```

允许 9:16 扩图、裁切、构图重组、焦段感调整、轻到中度机位高度/俯仰调整、光学主次重建。

必须锁定：产品可见面比例、几何、数量、排列、重叠顺序、直接承载面、可信透视和器皿/托盘形态。

禁止极端低机位、极端广角、生成源图未支持的新侧面、旋转成全新视角、为构图改变产品数量或位置。

## P12. Multi-Product Hero Hierarchy

多产品场景从原图已存在的前景单体或小簇选 `PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER`；其余保持不变成为 `SUPPORTING_PRODUCT_FIELD`。

只能通过 light pool、局部锐度、rim、对比、景深、负空间和受控 reframe 建立层级；不得移动、删除、复制、缩放或重排产品。

## P13. Stage B Handoff

任何 B 请求：

```text
CURRENT_STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
```

不得让 Stage B 回退原始随手拍，也不得引用上一任务图片。

## P14. Targeted Retry

失败先诊断再修正，不随机整张重抽。

典型类型：Ingredient / Vessel / Plating / Physical Relationship / Surface State Drift / Unsupported Completion / Weak Photography / Generic Background / Background Architecture / Temperature / Excessive Effect / Scene Integration / Generic Display Case / Camera Too Conservative / Multi-Product Inventory Look / Fake Four-Layer Depth / Wrong Category Material Language / 9:16 Composition。

最多逐级收紧到 Attempt 3 Ultra-Conservative Subject Mode。宁可降低危险的摄影戏剧性，也不允许产品漂移；但不得因为保真退化成普通随手拍。

## P15. Capability Evidence + Runtime Profile

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

允许进入 READY，但不得声称已端到端验证。第一次真实业务调用兼任验证，不额外生成无业务价值测试图。

## P16. Fail Closed

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
- `SURFACE_STATE_MANIFEST` 未建立；
- `TOPOLOGY_COMPLETION_PLAN` 未建立或明确 N/A；
- `BACKGROUND_ARCHITECTURE_PLAN` 未建立；
- Hero Reframe / Multi-Product Plan 未建立或明确 N/A；
- 规则文件存在未解决冲突。

## P17. Repository Security Boundary

仓库只保存通用能力约定和变量名，不保存具体供应商名、私有聚合平台名、实际 API Base URL、API Key、私有凭据或 Runtime Profile 真实运行值。

## P18. Runtime State

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