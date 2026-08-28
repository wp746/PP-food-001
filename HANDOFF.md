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

## 3. Capability Evidence Levels

**宿主声明支持 ≠ 端到端已经验证。**

静态工具 schema、宿主能力描述、连接存在，只能得到：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
```

只有真实调用链成功，或存在与当前配置指纹匹配的已验证 Runtime Profile，才能得到：

```text
RUNTIME_CAPABILITIES_VERIFIED = PASS
```

若静态能力完整但没有匹配 profile：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

这时可以 READY；但不得声称“已 smoke tested / 已端到端验证”。

## 4. Runtime Profile Reuse

为了避免每个新会话重复 smoke test，允许宿主保存一个**私有持久 Runtime Profile**。该 profile 不属于 Git 仓库。

建议状态：

```text
RUNTIME_PROFILE_SCHEMA = 1
RUNTIME_PROFILE_VERIFIED = TRUE / FALSE
RUNTIME_PROFILE_FINGERPRINT = <opaque non-secret digest>
RUNTIME_PROFILE_SCOPE = STAGE_A / FULL_A_TO_B
```

Fingerprint 只使用非秘密运行身份，例如：
- VISION_MODEL 标识；
- IMAGE_MODEL 标识；
- reference-edit 路由/连接槽标识；
- Stage A→B pass-through 路由版本；
- 必要时 API origin 的不可逆摘要。

**不得包含 API Key、Token、完整私有 URL 或用户凭据。**

如果：

```text
RUNTIME_PROFILE_VERIFIED = TRUE
AND RUNTIME_PROFILE_FINGERPRINT_MATCH = TRUE
```

则：

```text
RUNTIME_CAPABILITIES_VERIFIED = PASS
FIRST_LIVE_VERIFICATION_REQUIRED = FALSE
```

无需重复 smoke test。

Fingerprint 不匹配、profile 不存在或 profile 已失效：

```text
RUNTIME_CAPABILITIES_VERIFIED = PENDING
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE
```

## 5. First Live Verification

不要额外生成无业务价值的测试图。

如果 `FIRST_LIVE_VERIFICATION_REQUIRED = TRUE`，用户“启动”后的**第一笔真实任务**兼任一次性验证。

在最终交付前必须实际证明：
- VISION_MODEL 真实读到当前用户图；
- IMAGE_MODEL 真实收到 current user image 作为 reference 并返回结果；
- Agent / VISION_MODEL 真实读取生成结果；
- 若为 B，当前 Stage A PASS 图真实传入 Stage B。

成功后更新私有 profile；失败则不交付假结果，立即回 SETUP_GATE。

## 6. Generic Runtime Variables

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

## 7. Security Boundary

禁止提交到仓库：
- 具体供应商/聚合平台私有名称；
- 实际 API Base URL；
- API Key / Token；
- 用户账户或私有凭据；
- Runtime Profile 的真实运行值或 fingerprint 原始组成信息。

这些只存在运行环境/宿主私有状态。

## 8. State Machine

Mandatory Read 或静态能力缺失：

```text
RUNTIME_STATE = SETUP_GATE
PRODUCTION_GATE = BLOCKED
```

Bootstrap Proof + Pre-flight + `RUNTIME_CAPABILITIES_DECLARED = PASS` 后，可以：

```text
READY
RUNTIME_STATE = READY_WAITING_FOR_START
```

同时必须准确报告 `VERIFIED = PASS` 或 `PENDING`。

等待用户说“启动”。之后进入 `PRODUCTION`。

## 9. Failure Recovery

出现以下任一情况，立即使当前 profile 失效并退回 SETUP_GATE：
- VISION_MODEL 无法读图；
- IMAGE_MODEL 参考图编辑不可用；
- Credential 失效；
- 图片输入/输出传递失败；
- Stage A 输出无法继续传给 Stage B；
- 当前 runtime fingerprint 与已验证 profile 不匹配；
- 上下文压缩后无法证明 P0 规则仍在活跃上下文。

```text
RUNTIME_PROFILE_VERIFIED = FALSE
RUNTIME_STATE = SETUP_GATE
PRODUCTION_GATE = BLOCKED
```

只修复具体缺失项，不假装 READY。

## 10. Production UX

用户不需要知道 JSON、Prompt、模型参数或内部路由。进入 PRODUCTION 后，用户只需上传图片、说 A / B 或用自然语言描述需求。

每个任务的内部编译由 `EXECUTION_CONTRACT_TEMPLATE.md` 完成。