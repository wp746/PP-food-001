# PP-food-001 Runtime Manifest

本文件是 Stage A 的 **P0 唯一运行真相源**。其他文件可以解释、举例、扩展，但不得重新定义或削弱以下规则。

## P0. Source Truth

```text
SOURCE_TRUTH = CURRENT_USER_IMAGE
```

原图可见像素是真实产品真相。用户明确提供的菜名/品类信息可以帮助语义路由，但不能覆盖原图食材、器皿、摆盘和物理关系。

未知区域只允许 Minimum Plausible Continuation，不得借扩图重做主体。

## P1. Default Output

```text
DEFAULT_ASPECT_RATIO = 9:16
```

横图、方图、竖图都默认输出 9:16。适配方式优先级：画布延展 > 背景重构 > 镜头/空间重组。禁止拉伸、压缩、裁坏关键产品或重做产品适配画幅。

## P2. A / B Intent Router

优先级：

```text
1. Explicit A → Stage A only
2. Explicit B → Stage A → Stage A QC → Stage A PASS → Stage B
3. No A/B + obvious KV business info → B, but still Stage A first
4. Otherwise → A
```

商业信息包括：产品/菜名、品牌/店铺、主标题、副标题、地址、电话、价格、核心食材、卖点、新品/活动等。

```text
EXPLICIT_A_OVERRIDES_AUTO_B = TRUE
B_CAN_SKIP_STAGE_A = FALSE
```

## P3. Current Job Isolation

每张新上传图创建新的 `CURRENT_JOB_FACTS`。

当前任务只允许使用：
- 当前图可见事实；
- 当前用户明确提供的信息；
- 当前任务已验证的中间产物。

除非用户明确要求沿用，上一任务的品牌、产品名、食材、口味、地址、电话、Slogan、文案和场景事实全部失效。

## P4. Runtime Roles

`VISION_MODEL`：识图、Fidelity Manifest、品类/温度/语义路由、生成后 Fidelity/Semantic/Hero QC。

`IMAGE_MODEL`：必须支持 reference-image editing / image-to-image；接收真实参考图并执行高保真商拍。

默认宿主模型无视觉时禁止猜图。

## P5. Fidelity Hard Gate

```text
Food Identity >=95
Ingredient Geometry >=95
Vessel / Container Identity >=98
Plating Topology >=95
Physical Relationship Fidelity >=95
Photography >=85
Semantic Relevance >=85
Hero Spatial Score >=85
Appetite Score >=85
NO CRITICAL FAILURE
```

不可牺牲顺序：

```text
Food Identity
> Major Ingredient Identity
> Ingredient Geometry
> Vessel / Packaging
> Physical Relationships
> Plating Topology
> Sauce / Oil / Broth / Cream / Ice State
> Visible Count / Arrangement
> Material Realism
> Color
> Composition
> Lighting
> Background
> Props
> Atmosphere
```

视觉张力与保真冲突时：

```text
REDUCE_DESIGN_AGGRESSION = TRUE
REDUCE_FIDELITY = NEVER
```

## P6. Subject Lock

必须锁定：产品身份、主辅食材、几何、数量关系、器皿/包装、摆盘拓扑、酱汁/红油/汤体/奶油/冰块状态、手持/餐具/托盘等物理关系。

禁止：加减/替换主要食材、换器皿、重画包装、重摆盘、把产品标准化成“另一份更漂亮的同类食品”。

Stage A Prompt 前部必须是强硬具体锁定，不接受仅写“参考原图”“保持一致”。

## P7. Hero Stage

Stage A 是高级材质舞台上的 Food Hero，不是默认真实经营场所。

必须：
- 从当前食品属性推导材质、色彩、温度、光线和身份锚点；
- 建立 L1 前景 / L2 Hero / L3 中后景 / L4 深背景四层空间；
- 产品为唯一锐利主角并处于光池；
- 语义道具只在主体外部、低对比、虚化且不得暗示主体新增食材；
- 冷食零热蒸汽，热食仅克制且物理合理的蒸汽；
- 食欲感来自真实材质，不来自塑料高光、过饱和或浓烟。

## P8. Stage B Handoff

任何 B 请求：

```text
CURRENT_STAGE_B_REFERENCE = CURRENT_JOB_STAGE_A_PASS_IMAGE
```

不得让 Stage B 回退原始随手拍，也不得引用上一任务图片。

## P9. Targeted Retry

失败先诊断再修正，不随机整张重抽。

典型类型：Ingredient / Vessel / Plating / Physical Relationship / Weak Photography / Generic Background / Temperature / Excessive Effect / Scene Integration / 9:16 Composition。

最多逐级收紧到 Attempt 3 Ultra-Conservative Subject Mode。宁可降低摄影戏剧性，也不允许产品漂移。

## P10. Fail Closed

以下任一项无法确认时：

```text
PRODUCTION_GATE = BLOCKED
```

- Mandatory Read 未完成；
- Pre-flight 未通过；
- VISION_MODEL 不能读图；
- IMAGE_MODEL 不支持参考图编辑；
- Credential 未就绪；
- 图片输入/输出不能被正确传递；
- 当前 Execution Contract 未建立；
- 规则文件存在未解决冲突。

禁止“先出一张试试看”。

## P11. Repository Security Boundary

仓库只保存通用能力约定和变量名，不保存：
- 具体供应商名；
- 私有聚合平台名；
- 实际 API Base URL；
- API Key；
- 私有凭据或账户信息。

运行值只存在宿主 Secret / Environment / Connection。

## P12. Runtime State

```text
SETUP_GATE
→ READY_WAITING_FOR_START
→ user says 启动
→ PRODUCTION
```

连接失效或能力变为 UNKNOWN 时，退回 SETUP_GATE，只修复缺失项。