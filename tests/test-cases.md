# PP-food-001 Regression Tests

这些测试只保留会影响稳定生产的关键失败模式，并避免把历史真实项目词反复注入冷启动上下文。

## Test 01｜Food DNA first
PASS：原图产品身份、主要食材、几何、器皿/包装、摆盘、酱汁/油/汤体状态和物理关系保持。
FAIL：为了高级感加减食材、换器皿、重摆盘或把产品重做成另一份。

## Test 02｜默认 9:16
输入：横图、方图、竖图各一张。
PASS：最终均为严格 9:16 竖版，关键产品完整，靠画布延展/背景重构/受控 Hero Reframe 适配。
FAIL：拉伸、压扁、裁掉关键产品区域、重做产品适配竖版，或最终交付任何非 9:16 成片。

## Test 03｜A 默认路由
输入：用户只上传美食图，未给 A/B，也无明显 KV 商业信息。
PASS：执行 Stage A 商拍。

## Test 04｜显式 A 优先
输入：用户说 A，同时附带产品名或店铺信息。
PASS：只执行 Stage A，不自动进入 KV。

## Test 05｜显式 B 必须先 A
输入：用户说 B。
PASS：原图 → Stage A → Fidelity QC → Stage A PASS 图 → Stage B。
FAIL：直接拿原始随手拍做 KV。

## Test 06｜商业信息自动 B
输入：用户未说 A/B，但给出产品名、店铺、主标题、副标题、地址、电话、价格、核心食材、卖点、新品/活动等明显商业信息。
PASS：判定为 B，但仍先完整执行 Stage A。

## Test 07｜当前任务隔离
输入：上一任务包含 `LEGACY_PRODUCT_X / LEGACY_BRAND_X / LEGACY_INGREDIENT_X`，下一任务是 `CURRENT_PRODUCT_Y`。
PASS：当前任务不继承上一任务品牌、产品名、食材、口味、地址、Slogan 或场景事实。
FAIL：任一 legacy entity 混入当前任务。

## Test 08｜Execution Contract 锁定当前任务
PASS：生成前合同至少包含：

```text
JOB_MODE
ASPECT_RATIO = 9:16
CURRENT_JOB_FACTS
SOURCE_PRODUCT
VISIBLE_FACTS
LOCK_TARGETS
SURFACE_STATE_LOCK
TOPOLOGY_COMPLETION_PLAN
CREATIVE_SCOPE
FORBIDDEN
HERO_REFRAME_PLAN
MULTI_PRODUCT_HERO_PLAN
BACKGROUND_ARCHITECTURE_PLAN
```

FAIL：未建立当前任务合同就直接调用 IMAGE_MODEL。

## Test 09｜IMAGE_MODEL 首段硬锁
PASS：明确锁定食物身份、主要食材几何、器皿/包装、摆盘拓扑、酱汁/油/汤体状态、表面状态和物理关系。
FAIL：只有“参考原图做高级商拍”“保持一致”之类弱约束。

## Test 10｜Container / Package Lock
PASS：当前容器/包装类型、材质、颜色、结构和比例保持。
FAIL：为了“高级”替换容器、重画包装或改变主要包装结构。

## Test 11｜Product Geometry Lock
PASS：当前食品自身的身份性几何、数量关系、排列和层级保持。
FAIL：为了更规整、更精致而标准化成另一份同类产品。

## Test 12｜温度语义
PASS：冷食无热蒸汽；热食仅有物理合理、克制的蒸汽。
FAIL：冷产品出现热气，或热产品被不合理浓烟遮挡。

## Test 13｜高级材质舞台而非经营场所
PASS：背景从当前食品属性推导材质、色彩、光影和身份锚点，形成四层 Hero Stage。
FAIL：默认生成真实经营场所结构并诱发人物/招牌/文字污染。

## Test 14｜反模板背景
输入：四个彼此差异显著的食品品类 A/B/C/D。
PASS：四者背景材质、色彩、光线和摄影情绪明显不同且符合各自属性。
FAIL：四者几乎共享同一舞台、同一道具和同一色调。

## Test 15｜Hero Food
PASS：产品是第一视觉锚点；四层空间、光池、轮廓光和身份锚点服务产品。
FAIL：背景道具或舞台元素比产品更抢眼。

## Test 16｜Fidelity hard gate
通过条件：

```text
Food Fidelity >=95
Vessel Fidelity >=98
Photography >=85
Semantic >=85
Hero Spatial >=85
Appetite >=85
OUTPUT_ASPECT_RATIO = 9:16
NO CRITICAL FAILURE
```

## Test 17｜保真与视觉张力冲突
PASS：降低背景、构图或摄影激进度，保留产品真相。
FAIL：为了“真正高级”牺牲 Food DNA。

## Test 18｜定向重试
PASS：按 Ingredient / Vessel / Plating / Physical Relationship / Surface State / Photography / Background / Temperature / Integration / Hero Reframe / Multi-Product Hierarchy / Background Architecture / 9:16 Composition 分类修正；最多逐级收紧到 Ultra-Conservative Subject Mode。
FAIL：每次随机整张重抽，导致已正确区域再次漂移。

## Test 19｜Fail Closed
任何 Mandatory Read、Pre-flight 能力或当前任务 Contract 无法确认时，不得调用 IMAGE_MODEL。

## Test 20｜Display Case 不得绑死 Hero Stage
输入：开放式面包/甜点陈列在普通展示柜或木托盘中，展示柜本身没有品牌、包装、手持或物理身份价值。
PASS：锁定产品、原托盘/直接承载关系和产品排列；允许把柜体、墙面、门店环境转译成品类专属高级材质 Hero Stage。
FAIL：因为命中 `DISPLAY_CASE` 就机械保留普通柜体/墙面，最后只是“更干净的店内展示照”。

## Test 21｜Controlled Hero Reframe
PASS：允许改变画布、裁切、焦段、机位高度/俯仰的轻到中度调整，只要产品可见面比例、几何、排列、接触平面和透视关系仍可信；目标是让主体进入英雄机位。
FAIL A：把“锁产品”误读成“必须锁死源图相机坐标”，导致只能原角度修图。
FAIL B：为了 Hero 感使用极端低机位/广角，生成源图未支持的新侧面、变形或数量漂移。

## Test 22｜多产品 Hero Hierarchy
输入：一盘/一箱多个同类食品。
PASS：数量、位置、排列不变；从原图已存在的前景单体或小簇中选 `PRIMARY_HERO_UNIT / PRIMARY_HERO_CLUSTER`，只通过光池、局部锐度、对比、rim light 和景深建立主次，其余成为 `SUPPORTING_PRODUCT_FIELD`。
FAIL：所有单体视觉权重完全相同而继续像库存陈列；或为了主次关系移动、删除、复制、重排产品。

## Test 23｜Bakery Bread 独立路由
输入：贝果、碱水面包、恰巴塔、欧包等“面包为主体”的烘焙产品。
PASS：进入 `BAKERY_BREAD_HERO` 路由，以原图已有脆壳/裂口/内瓤/烘焙色为视觉核心；背景由品类原生材质建筑舞台与真正四层纵深构成；摄影可到 CINEMATIC_EDITORIAL / PREMIUM_BAKERY_CAMPAIGN。
FAIL：因为“烘焙”与咖啡同组而默认加入咖啡豆、手冲壶、咖啡馆 Lifestyle 皮肤，或只形成原木+亚麻+黄铜夹子的通用烘焙模板。

## Test 24｜Hero Spatial Anti-False-Pass
以下任一项存在，`Hero Spatial Score` 不得 >=85：
- 没有可见 L1 近景空间入口；
- L4 只是单一虚墙/渐变/一团 bokeh，没有至少两个可分辨的后退材质/光影层；
- 产品没有明确 light pool 或 rim separation；
- 多产品场景没有主 Hero 层级，整体仍读成库存/展示陈列；
- 普通门店/展示柜语境在无身份必要时被机械保留，画面仍首先读成“店里拍的”；
- 加几个亚麻布/夹子/石块就被误判为世界级材质舞台。

PASS：L1/L2/L3/L4 都有可观察证据，虚实连续递进，产品具有纪念碑式视觉权重，背景材料与当前食品属性有不可替换的语义关系。

## Test 25｜Surface / Material State Lock
输入：任意食品原图，其表面已经存在明确的烘烤深浅、焦化程度、湿润度、油亮度、酱汁覆盖、糖霜/奶油状态、冰霜/冷凝、脆壳/皮肤、炭化、熟度或颜色梯度。
PASS：商拍只通过更好的曝光、显色、局部对比、镜面高光控制、微纹理解析和真实光线，把**原图已经存在的表面状态看得更清楚、更诱人**；基础颜色、烘烤/焦化程度、熟度、湿润度等级和表皮结构不发生身份性变化。
FAIL：为了食欲感把表皮烤得更黑、更焦、更红、更油、更湿、更脆、更有糖壳，或把原来哑光食品做成镜面亮膜；输出看起来像另一批火候/熟度不同的产品。

## Test 26｜Appetite Enhancement ≠ Material Mutation
PASS：`Appetite Score` 提升来自摄影读取能力：light placement、specular control、micro-contrast、texture legibility、color accuracy、freshness cues；不是重新烹饪或重画产品。
FAIL：把“增强食欲”解释成“增强属性本身”，例如把轻微焦糖色变成深焦、少量油光变成油刷感、自然裂纹变成夸张爆口、普通汁水变成大量滴汁。

## Test 27｜Topology-Preserving Completion
输入：用户原图因裁切、取景或装盘边缘没有拍全，能从可见部分高置信度判断同一份食品/器皿/摆盘的自然延续。
PASS：允许为 9:16 扩图或完整呈现而补全被画面边缘截断的**同一份产品/同一器皿/同一摆盘拓扑**；只做 Minimum Plausible Continuation，延续已知食材身份、切法、尺度、方向、层级、酱汁状态、数量密度和承载关系。
FAIL：借“补全”新增原图没有证据的食材种类、改变主料结构、重新摆盘、把不规则堆叠改成规则造型、增加豪华配料，或把补全部分做成比原图更高级的另一份产品。

## Test 28｜Completion Confidence Gate
PASS：只有在可见证据足以支持自然延续时才补全主体；低置信度区域优先用环境延展、裁切策略或保守遮挡解决。
FAIL：看不见也无法推断的产品区域被模型自由创造。

## Test 29｜9:16 Final Delivery Hard Gate
输入：任意 Stage A 请求，源图比例任意。
PASS：IMAGE_MODEL 最终输出画布必须为严格竖版 `width:height = 9:16`；若第一次模型输出不是 9:16，系统不得交付，必须通过 outpaint / canvas correction / targeted retry 修正到 9:16，同时继续锁住产品。
FAIL：输出 16:9、4:3、1:1、接近 9:16 但不准确，或因为源图横向就沿用横构图。

```text
OUTPUT_ASPECT_RATIO_EXACT = 9:16
NON_9_16_DELIVERY = CRITICAL_FAILURE
```

## Test 30｜Background Architecture > Prop Styling
输入：任意需要高级 Hero Stage 的食品，尤其是开放展示柜、桌面、普通门店环境来源图。
PASS：即使删除全部辅助道具，背景仍能依靠**材质平面、空间体块、前后遮挡、台面高差、光影切面、反射/吸光差异和深度递进**成立；道具只占辅助角色，且可为零。
FAIL：高级感主要依赖亚麻布、夹子、咖啡杯、陶罐、麦穗、香料碟等“道具包”；去掉道具后只剩普通木柜、虚墙或空背景。

必须建立：

```text
BACKGROUND_ARCHITECTURE_PLAN
- primary_material_planes: 2-3
- near/mid/deep spatial masses
- height/depth variation
- light-cut / shadow architecture
- reflection vs absorption relationship
- category-derived color/material logic
- props: OPTIONAL, subordinate
```

如果背景第一读感是“布置了几个高级道具”，而不是“为该食品专门设计的商业摄影舞台”，则 FAIL。

以上 Test 25–30 **适用于所有食品品类**，包括面食、米食、肉类、卤味、烧烤、海鲜、烘焙、甜品、水果、饮品、火锅、包装食品等。