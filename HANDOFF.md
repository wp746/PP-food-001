# PP-food-001 Runtime Handoff

本文件只负责**运行环境能力与凭据交接**。设计与保真规则由 `RUNTIME_MANIFEST.md` / `references/` 管理，避免重复定义。

## 1. Start Here

新的智能体必须先读：

```text
BOOTSTRAP.md
```

Bootstrap 完成后才进入本文件的能力检查。

## 2. Required Runtime Capabilities

只确认缺失项：

1. `VISION_MODEL`
   - 能读取用户上传图；
   - 能读取 IMAGE_MODEL 生成结果；
   - 用于 Food DNA / 路由 / QC。

2. `IMAGE_MODEL`
   - 必须支持 reference image / image editing / image-to-image；
   - 能实际接收用户原始图片，不是只接文字描述。

3. Credential / Connection
   - 凭据已经在宿主 Secret / Environment / Connection 中可用；
   - 普通对话只确认“已配置/未配置”，不要回显完整 Key。

4. Image Pass-through
   - 用户图能传给 IMAGE_MODEL；
   - IMAGE_MODEL 输出能被 Agent / VISION_MODEL 读取；
   - 若当前任务为 B，Stage A PASS 图能继续传给 Stage B。

## 3. Generic Runtime Variables

宿主可自行映射名称，例如：

```text
VISION_MODEL
IMAGE_MODEL
API_BASE_URL
API_KEY
REFERENCE_IMAGE_EDIT
STAGE_A_TO_STAGE_B_PASS_THROUGH
```

这里只定义接口，不保存任何真实值。

## 4. Security Boundary

禁止提交到仓库：
- 具体供应商/聚合平台私有名称；
- 实际 API Base URL；
- API Key / Token；
- 用户账户或私有凭据。

这些只存在运行环境。

## 5. State Machine

能力未知或缺失：

```text
RUNTIME_STATE = SETUP_GATE
```

Bootstrap Proof + Pre-flight + Runtime Capabilities 全部通过后：

```text
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

等待用户说“启动”。之后：

```text
RUNTIME_STATE = PRODUCTION
```

PRODUCTION 中不再反复询问配置，除非能力或连接失效。

## 6. Failure Recovery

出现以下任一情况，立即退回 SETUP_GATE：
- VISION_MODEL 无法读图；
- IMAGE_MODEL 参考图编辑不可用；
- Credential 失效；
- 图片输入/输出传递失败；
- Stage A 输出无法继续传给 Stage B；
- 上下文压缩后无法证明 P0 规则仍在活跃上下文。

只修复具体缺失项，不假装 READY。

## 7. Production UX

用户不需要知道 JSON、Prompt、模型参数或内部路由。进入 PRODUCTION 后，用户只需：
- 上传图片；
- 说 A / B；
- 或用自然语言描述需求。

每个任务的内部编译由 `EXECUTION_CONTRACT_TEMPLATE.md` 完成。