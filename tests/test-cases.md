# PP-food-001 Regression Tests

这些测试只保留会影响稳定生产的关键失败模式，并避免把历史真实项目词反复注入冷启动上下文。

## Test 01｜Food DNA first
PASS：原图产品身份、主要食材、几何、器皿/包装、摆盘、酱汁/油/汤体状态和物理关系保持。
FAIL：为了高级感加减食材、换器皿、重摆盘或把产品重做成另一份。

## Test 02｜默认 9:16
输入：横图、方图、竖图各一张。
PASS：最终均为 9:16，关键产品完整，靠画布延展/背景重构/受控 Hero Reframe 适配。
FAIL：拉伸、压扁、裁掉关键产品区域或重做产品来适配竖版。

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
CREATIVE_SCOPE
FORBIDDEN
HERO_REFRAME_PLAN
MULTI_PRODUCT_HERO_PLAN
```

FAIL：未建立当前任务合同就直接调用 IMAGE_MODEL。

## Test 09｜IMAGE_MODEL 首段硬锁
PASS：明确锁定食物身份、主要食材几何、器皿/包装、摆盘拓扑、酱汁/油/汤体状态和物理关系。
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
NO CRITICAL FAILURE
```

## Test 17｜保真与视觉张力冲突
PASS：降低背景、构图或摄影激进度，保留产品真相。
FAIL：为了“真正高级”牺牲 Food DNA。

## Test 18｜定向重试
PASS：按 Ingredient / Vessel / Plating / Physical Relationship / Photography / Background / Temperature / Integration / Hero Reframe / Multi-Product Hierarchy / 9:16 Composition 分类修正；最多逐级收紧到 Ultra-Conservative Subject Mode。
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
PASS：进入 `BAKERY_BREAD_HERO` 路由，以脆壳/裂口/内瓤/烘焙色为视觉核心；背景由石材、烘焙金属、纸/布等克制材质和真正四层纵深构成；摄影可到 CINEMATIC_EDITORIAL / PREMIUM_BAKERY_CAMPAIGN。
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