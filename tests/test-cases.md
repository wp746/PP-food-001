# PP-food-001 Regression Tests

这些测试只保留会影响稳定生产的关键失败模式。

## Test 01｜Food DNA first
PASS：原图产品身份、主要食材、几何、器皿/包装、摆盘、酱汁/红油/汤体状态和物理关系保持。
FAIL：为了高级感加减食材、换器皿、重摆盘或把产品重做成另一份。

## Test 02｜默认 9:16
输入：横图、方图、竖图各一张。
PASS：最终均为 9:16，关键产品完整，靠画布延展/背景重构/镜头重组适配。
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
输入：上一任务为“泡菜米线”，下一任务是其他食品。
PASS：新任务不继承上一任务品牌、产品名、食材、口味、地址、Slogan 或场景事实。
FAIL：旧实体混入当前任务。

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
```

FAIL：未建立当前任务合同就直接调用 IMAGE_MODEL。

## Test 09｜IMAGE_MODEL 首段硬锁
PASS：明确锁定食物身份、主要食材几何、器皿/包装、摆盘拓扑、酱汁/红油/汤体状态和物理关系。
FAIL：只有“参考原图做高级商拍”“保持一致”之类弱约束。

## Test 10｜饮品容器锁定
PASS：塑料杯仍是塑料杯，吸管、液体颜色、冰块/配料和握持关系保持。
FAIL：塑料杯变玻璃杯、加新水果/奶盖或错误蒸汽。

## Test 11｜烘焙产品锁定
PASS：面包/贝果/糕点形状、开口、表皮颜色、阵列关系和托盘身份保持。
FAIL：为了更精致改变烘焙造型或新增装饰。

## Test 12｜包装食品锁定
PASS：包装 Logo、文字、形状、材质和比例保持。
FAIL：重画包装或改成堂食摆盘。

## Test 13｜温度语义
PASS：冷食无热蒸汽；热食仅有物理合理、克制的蒸汽。
FAIL：冷饮冒热气，或热菜被浓烟遮挡。

## Test 14｜高级材质舞台而非经营场所
PASS：背景从食品属性推导材质、色彩、光影和身份锚点，形成四层 Hero Stage。
FAIL：默认生成真实餐厅、档口、门店、街道等容易诱发人物/文字污染的经营场所。

## Test 15｜反模板背景
输入：宽面、蛋糕、咖啡、烧烤。
PASS：背景材质、色彩、光线和摄影情绪明显不同且符合各自属性。
FAIL：全部变成深木 + 暖灯 + 陶罐 + 重散景。

## Test 16｜Hero Food
PASS：产品是第一视觉锚点；四层空间、光池、轮廓光和身份锚点服务产品。
FAIL：背景道具或作料比产品更抢眼。

## Test 17｜Fidelity hard gate
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

## Test 18｜保真与视觉张力冲突
PASS：降低背景、构图或摄影激进度，保留产品真相。
FAIL：为了“真正高级”牺牲 Food DNA。

## Test 19｜定向重试
PASS：按 Ingredient / Vessel / Plating / Physical Relationship / Photography / Background / Temperature / Integration / 9:16 Composition 分类修正；最多逐级收紧到 Ultra-Conservative Subject Mode。
FAIL：每次随机整张重抽，导致已正确区域再次漂移。

## Test 20｜Fail Closed
任何 Mandatory Read、Pre-flight 能力或当前任务 Contract 无法确认时，不得调用 IMAGE_MODEL。