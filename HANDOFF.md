# PP-food-001｜安装交接与运行准备

这份文件用于把 `PP-food-001` 交给新的智能体/工作流运行环境。安装或首次加载本 Skill 后，智能体必须先完成运行环境检查，再进入生产。

## 1. 首次加载必须进入 SETUP_GATE

在运行状态未知时，不要直接生成图片。先向用户说明：

> 已加载 PP-food-001。为了稳定锁定参考图 Food DNA 并完成电影级商拍，请先配置运行环境。我只需要确认以下信息，配置完成后你回复“启动”即可进入生产模式。

然后只收集/确认缺失项：

1. **视觉理解模型（VISION_MODEL）**：用于识图、Food DNA Manifest、菜品/场景分析和生成后 QC。
2. **图片生成/编辑模型（IMAGE_MODEL）**：必须支持参考图 / image-to-image / image editing，用于真正锁定参考图并生成商拍。
3. **API Base URL（API_BASE_URL）**：聚合平台或模型服务地址。
4. **API Key / Credential**：应写入 Secret、Environment Variable 或平台凭据管理器；不要要求用户把完整 Key 明文贴进普通聊天。
5. **能力确认**：图片接口能接收参考图；生成结果能作为后续调用输入；视觉模型能读取用户上传图片。

推荐环境变量名：

```text
PP_FOOD_API_BASE_URL
PP_FOOD_API_KEY
PP_FOOD_VISION_MODEL
PP_FOOD_IMAGE_MODEL
```

如果宿主平台有自己的 Secret/Connection 系统，优先使用宿主机制，不强制使用上述变量名。

## 2. 模型职责必须分离

### VISION_MODEL
负责：
- 识别用户上传图片；
- 提取 Food DNA / Fidelity Manifest；
- 判断 food category、scene、dish semantics；
- 判断视觉路由置信度；
- 生成前分析；
- 生成后 Fidelity QC / Semantic QC。

如果宿主默认模型不支持视觉，**不得猜图**。必须显式调用已配置的 `VISION_MODEL`。

### IMAGE_MODEL
负责：
- 接收用户原始参考图；
- 按参考图执行高保真编辑；
- 锁定食物、主要食材、器皿、包装、摆盘和物理关系；
- 升级灯光、背景、景深、材质和商业摄影质感。

图片模型可以“参考图出图”，但不能替代前置识图、路由和后置 QC 的全部职责。

## 3. 最低能力检查

进入 READY 前至少确认：

```text
[ ] VISION_MODEL 能接收图片
[ ] IMAGE_MODEL 能接收参考图并编辑
[ ] API 凭据可用
[ ] 图片输入可从当前智能体传给 IMAGE_MODEL
[ ] IMAGE_MODEL 输出可被当前智能体保存/继续传递
[ ] 智能体能读取 SKILL.md 与 references/
```

若平台不支持其中一项，应明确告诉用户缺失能力，不要假装已经准备好。

## 4. READY 协议

所有必要项完成后，智能体必须回复类似：

> PP-food-001 运行环境已准备就绪。视觉模型负责识图与 QC，图片模型负责参考图高保真编辑。回复 **“启动”** 进入生产模式。

在收到“启动”之前，状态为：

```text
RUNTIME_STATE = READY_WAITING_FOR_START
```

用户回复“启动”后：

```text
RUNTIME_STATE = PRODUCTION
```

然后用户可以完全使用自然语言，例如：

> 这是一道青花椒酸菜鱼，帮我优化成电影级商拍，9:16。

智能体应自动执行，不再反复询问模型配置，除非连接失效或配置缺失。

## 5. 生产模式默认链路

```text
用户上传原图
→ VISION_MODEL 读取原图
→ 建立 Fidelity Manifest / 菜品语义 / 场景路由
→ PP-food-001 组装编辑指令
→ IMAGE_MODEL 接收原始参考图 + 编辑指令
→ 输出电影级商拍图
→ VISION_MODEL 做 Fidelity QC + Semantic QC
→ 若失败，按失败类型定向重试
```

## 6. 图像提示词首段硬锁

调用 IMAGE_MODEL 时，最终编辑提示词前部必须明确表达：

> 以用户上传的参考图为唯一产品真相。严格锁定原始食物主体、主要食材身份与几何、器皿/包装、摆盘拓扑和物理关系。不得为了“更高级”重做、替换、增减或重新摆放主体食材。主要创意只发生在灯光、环境、背景、景深、调色和摄影品质层。

不能只写“参考原图”四个字就结束。

## 7. 与 PP-food-KV-001 联动

当同时安装 `PP-food-KV-001` 时：

- 本 Skill 是 **Stage A / Commercial Re-photography Engine**；
- KV Skill 必须把本 Skill 的 Stage A 输出作为 Stage B 输入；
- 不得绕过 Stage A 直接用原始随手拍做激进 KV，除非用户明确要求跳过且接受更低保真稳定性。

一次完成上述双模型配置后，可以供两个 Skill 共用，不必重复询问。

## 8. 用户不需要知道内部术语

生产模式下，用户只需要上传照片并用大白话说明需求。不要强迫用户提供 JSON、Prompt、路由名或模型参数。内部自动结构化执行。
