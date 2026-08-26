# PP-food-001 Runtime / Handoff Regression Tests

## Test R01｜首次安装不得直接生产

条件：新智能体首次加载 Skill，运行环境状态未知。

PASS：先读取 `HANDOFF.md`，进入 `SETUP_GATE`，询问缺失的视觉模型、图片模型、API URL、Credential 和参考图能力。

FAIL：用户刚安装 Skill，智能体立即声称可以生产或直接调用图片模型。

## Test R02｜默认模型不识图时禁止猜图

条件：宿主默认 LLM 为纯文本模型，但已配置 VISION_MODEL。

PASS：遇到上传图片时显式调用 VISION_MODEL。

FAIL：默认模型根据文件名/用户一句话自行猜测 Food DNA。

## Test R03｜IMAGE_MODEL 必须支持 reference image

PASS：确认图片接口能接收用户原图并进行 image editing / image-to-image。

FAIL：只有 text-to-image 端点却宣称能稳定锁 Food DNA。

## Test R04｜Key 不要求长期明文放聊天

PASS：引导用户把 Key 放入 Secret / Environment / Connection，并只确认是否已配置。

FAIL：要求用户把完整长期 API Key 明文写入普通聊天作为唯一配置方式。

## Test R05｜READY 后必须等待“启动”

PASS：配置完成后回复“已准备就绪，回复‘启动’进入生产模式”，状态为 `READY_WAITING_FOR_START`。

FAIL：配置一完成就自动开始生成用户未要求的图片。

## Test R06｜启动后自然语言生产

条件：用户回复“启动”。

PASS：状态切换到 `PRODUCTION`，后续用户只需自然语言，不再反复问模型配置。

FAIL：每张图都重新追问 Base URL / 模型名 / Key。

## Test R07｜商拍生产链路

PASS：原图 → VISION_MODEL 分析 → Fidelity Manifest → IMAGE_MODEL 原图编辑 → VISION_MODEL QC → 定向重试。

FAIL：VISION_MODEL 只生成文字描述，IMAGE_MODEL 没有收到原始参考图。

## Test R08｜图片 Prompt 首段硬锁

PASS：IMAGE_MODEL 的编辑指令前部明确锁定食物、食材几何、器皿/包装、摆盘和物理关系。

FAIL：仅写“参考原图做高级商拍”这种弱约束。

## Test R09｜与 PP-food-KV-001 联动

PASS：Stage A 输出可继续作为 Stage B 输入，两 Skill 共用同一套 VISION_MODEL / IMAGE_MODEL / API 配置。

FAIL：KV Stage B 又回到原始随手拍，丢弃 Stage A 高保真商拍结果。
