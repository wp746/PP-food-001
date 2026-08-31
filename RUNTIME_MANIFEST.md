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

无论源图横图、方图、竖图，Stage A 最终交付都必须是严格 9:16 竖版画布。

适配优先级：

```text
canvas extension
> background reconstruction
> Controlled Hero Reframe
> high-confidence Topology-Preserving Completion
```

禁止：拉伸、压缩、裁坏关键产品、重做产品适配画幅。

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

`VISION_MODEL`：识图、当前 Product/Fidelity facts、Surface State、Completion Confidence、品类/温度/语义路由、Background Architecture Plan、生成后 Fidelity/Semantic/Hero/Aspect QC。

`IMAGE_MODEL`：必须支持 reference-image editing / image-to-image；接收真实当前参考图并执行高保真商拍。

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
REVEAL_EXISTING_PROPERTY = YES
AMPLIFY_PROPERTY_BEYOND_SOURCE = NO
```

所有品类必须锁定原图已有的：基础颜色与梯度、烘烤深浅、焦化程度、熟度、油亮/哑光等级、湿润度、酱汁/油覆盖、脆壳/皮肤状态、裂纹/割口、奶油/糖霜、冷凝/冰霜、透明度等可见状态。

商拍允许让这些属性更清楚，不允许把属性本身推强。若看起来像“同类食品但火候/熟度/表皮/酱汁状态明显不同的一批产品”，直接 Fidelity FAIL。

## P7. Topology-Preserving Completion

当源图因裁切、取景或装盘边缘没拍全，只允许补全同一份产品/同一器皿/同一摆盘拓扑。

```text
HIGH → natural continuation allowed
MEDIUM → minimum conservative continuation only
LOW / UNKNOWN → environment extension only
```

必须延续食材身份、几何/切法、尺度、方向、层级、重叠、密度、数量关系、表面状态与承载关系。

```text
COMPLETE_THE_SAME_SERVING = TRUE
DESIGN_A_BETTER_SERVING = FALSE
```

## P8. Subject + Direct Support Lock

必须锁定：产品身份、主辅食材/材质、几何、数量关系、器皿/包装、摆盘/阵列拓扑、表面状态、手持/餐具/托盘/烘焙纸等直接承载与物理关系。

禁止：加减/替换主要食材、换器皿、重画包装、重摆盘、移动/删除/复制/重排产品、把产品标准化成“另一份更漂亮的同类食品”。

Stage A IMAGE_MODEL Prompt 第一段必须是强硬具体 Reference Lock，不接受仅写“参考原图”“保持一致”。

## P9. Hero Stage + Scene Context Precedence

```text
Food DNA / Source Surface State / Direct Support
> World-Class Hero Stage
> Category Semantic Translation
> Generic Source Venue Appearance
```

普通展示柜/墙面/店内空间不是默认 Food DNA；在保留产品和直接承载关系的前提下可以转译成品类原生高级材质舞台。

Hero 必须有清晰前中后景、明确 light pool、可感知后退空间；空间证据不足或普通店内感明显 → Hero FAIL。

## P10. Background Architecture — All Categories

```text
BACKGROUND_ARCHITECTURE > PROP_STYLING
CATEGORY_MATERIAL_LOGIC > GENERIC_PREMIUM_PROPS
```

每个 Stage A 必须有：

```text
PRODUCT_DERIVATION_EVIDENCE >=3
BACKGROUND_BIG_IDEA = one clear concept
PRIMARY_MATERIAL_PLANES = 2-3
NEAR / MID / DEEP spatial masses
height / depth variation
occlusion relationship
light-cut / shadow architecture
reflective-vs-absorptive relationship
negative-space zone
props = OPTIONAL / subordinate
```

删除辅助道具后，背景仍必须像世界级商业摄影舞台。

以下直接 FAIL：主要靠亚麻、夹子、杯子、陶罐、麦穗、香料碟、灯泡/bokeh 等道具包；去掉道具后只剩普通背景；不同品类换主体后背景几乎无需改变。

## P11. Controlled Hero Reframe

```text
CONTROLLED_HERO_REFRAME_ALLOWED = TRUE
SOURCE_CAMERA_COORDINATES_ARE_FOOD_DNA = FALSE
```

允许 9:16 扩图、裁切、构图重组、焦段感调整、轻到中度机位调整；必须锁定产品可见面比例、几何、数量、排列、重叠顺序、直接承载面和可信透视。

禁止极端新视角、极端广角、生成源图未支持的新侧面，或为构图改变产品数量/位置。

## P12. Multi-Product Hero Hierarchy

多产品场景从原图已存在的前景单体/小簇选择 `PRIMARY_HERO_UNIT / CLUSTER`；其余保持为 Supporting Product Field。

只能通过光、锐度、对比、景深、负空间和受控 reframe 建立层级；不得移动、删除、复制、缩放或重排产品。

## P13. Stage B Handoff

任何 B 请求：

```text
CURRENT_STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
```

不得让 Stage B 回退原始随手拍，也不得引用上一任务图片。

## P14. Targeted Retry

失败先诊断再修正，不随机整张重抽。

典型类型：Food/Ingredient Drift、Vessel/Package Drift、Surface State Drift、Unsupported Completion、Weak Photography、Generic Background、Background Architecture、Temperature/Physics、Hero Composition、Wrong Category Material Language、9:16 Composition。

最多 3 次逐级收紧。宁可降低危险的摄影戏剧性，也不降低 Fidelity；但不得退化为普通随手拍。

## P15. Capability Evidence + Runtime Profile

静态 schema、宿主能力说明、连接存在只能证明：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
```

真实调用链成功，或存在与当前非秘密配置 fingerprint 匹配的已验证 Runtime Profile，才可：

```text
RUNTIME_CAPABILITIES_VERIFIED = PASS
```

否则：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

允许 READY，但不得声称已端到端验证。第一次真实业务调用兼任验证，不额外生成无业务价值测试图。

## P16. Runtime Context Discipline｜防过载

正常生产采用 Minimal Core：

```text
FULL_REPO_DUMP = FORBIDDEN
TESTS_IN_NORMAL_RUNTIME = FORBIDDEN
LOAD_ALL_REFERENCES = FORBIDDEN
PREVIOUS_JOB_SKIN_IMPORT = OFF
```

每个 A 任务只激活当前任务需要的 reference；品类、场景、示例与上一任务不自动延续。

IMAGE_MODEL 只接收：

```text
CURRENT_USER_IMAGE
+ compact current A Execution Contract
+ compact current A Prompt
```

不得把 SOP、tests、全部 references、历史案例或旧任务总结原样拼进 IMAGE_MODEL Prompt。

## P17. Fail Closed

以下任一无法确认：

```text
PRODUCTION_GATE = BLOCKED
```

- Runtime Minimal Core 未完成；
- Pre-flight 未通过；
- `RUNTIME_CAPABILITIES_DECLARED != PASS`；
- VISION_MODEL 不能读当前图；
- IMAGE_MODEL 不支持 reference edit；
- Credential / 图片传递未就绪；
- 当前 compact Execution Contract 未建立；
- Product Lock / Surface State / Completion / Background Big Idea / Hero Plan 无法解析；
- 当前合同出现未授权 previous-job contamination；
- 规则文件存在未解决冲突。

## P18. Repository Security Boundary

仓库只保存通用能力约定和变量名，不保存具体供应商名、私有聚合平台名、实际 API Base URL、API Key、私有凭据或 Runtime Profile 真实运行值。

## P19. Runtime State

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

连接失效、profile fingerprint 不匹配、版本变化或上下文压缩后无法证明 P0 时，退回 SETUP_GATE，只修复缺失项。
