# PP-food-001

高保真美食商业摄影 Skill。把用户随手拍升级成电影级 / 商业广告级美食摄影，同时锁定原始食物、主要食材、几何、摆盘、器皿、包装和真实物理关系。

当前版本：**V5.1.0**

## 首次安装：先完成运行环境交接

本 Skill 现在内置 `HANDOFF.md`。新的智能体安装后，不应该马上出图，而应该先检查运行环境。

首次加载时必须确认：

- **VISION_MODEL**：能读取图片，用于识图、Food DNA/Fidelity Manifest、路由与生成后 QC；
- **IMAGE_MODEL**：支持参考图编辑 / image-to-image，用于真正锁定原图并生成商拍；
- **API_BASE_URL**：聚合平台或模型服务地址；
- **API Key/Credential**：建议放在 Secret / Environment / Connection 中，不要长期明文写在普通对话；
- 图片能够从智能体传给 IMAGE_MODEL；
- IMAGE_MODEL 输出能够继续被智能体读取/保存。

配置完成后，智能体应告诉用户：

> **PP-food-001 已准备就绪。回复“启动”进入生产模式。**

用户说“启动”以后进入自然语言生产，不再要求用户理解 Prompt、路由、Food DNA 或模型参数。

详细交接规则见：`HANDOFF.md`。

## 双模型分工

### VISION_MODEL
负责：
- 看懂上传图片；
- 提取 Food DNA；
- 判断菜品、场景、语义路由；
- Fidelity QC / Semantic QC。

如果宿主默认模型不识图，禁止瞎猜，必须调用配置好的 VISION_MODEL。

### IMAGE_MODEL
负责：
- 接收原始参考图；
- 参考图高保真编辑；
- 锁食材、器皿、包装、摆盘和物理关系；
- 升级灯光、背景、环境、景深和商业摄影质感。

“图片模型能参考图出图”并不等于可以完全省掉视觉理解与 QC 层。

## V5.1 核心原则

> **保留产品本身，升级摄影品质；根据具体菜品语义设计环境。**

最终必须同时满足：

1. **HIGH FIDELITY** — 一眼仍然是原来那一份食物；
2. **HIGH PHOTOGRAPHY UPGRADE** — 摄影品质达到商业广告级；
3. **HIGH SEMANTIC RELEVANCE** — 背景、色彩、道具和氛围与具体菜品有关。

## 高保真目标

- 食物身份：**≥95%**
- 食材几何：**≥95%**
- 器皿 / 包装：**≥98%**
- 摆盘：**≥95%**
- 物理关系：**≥95%**
- 商业摄影质量：**≥85/100**
- 菜品语义背景：**≥85/100**

## 图像模型调用的首段硬锁

每次调用 IMAGE_MODEL 时，最终编辑提示词必须在前部明确表达：

> **以用户上传的参考图为唯一产品真相。严格锁定原始食物主体、主要食材身份与几何、器皿/包装、摆盘拓扑和物理关系。不得为了“更高级”重做、替换、增减或重新摆放主体食材。主要创意只发生在灯光、环境、背景、景深、调色和摄影品质层。**

这是跨智能体运行时保持稳定的关键规则之一。

## 生产链路

```text
用户上传原图
→ VISION_MODEL 识图
→ Fidelity Manifest / 菜品语义 / 场景路由
→ PP-food-001 组装编辑指令
→ IMAGE_MODEL 接收原始参考图 + 指令
→ 电影级商拍图
→ VISION_MODEL 做 Fidelity QC + Semantic QC
→ 定向重试（如有需要）
```

## 与 PP-food-KV-001 联动

当两个 Skill 同时安装：

```text
原始随手拍
→ PP-food-001（Stage A：高保真商拍）
→ Stage A 输出图
→ PP-food-KV-001（Stage B：KV）
```

Stage A 输出必须作为 Stage B 的输入参考图。一次完成视觉模型、图片模型和 API 配置后，两个 Skill 可以共用，不必重复配置。

## 仓库结构

```text
PP-food-001/
├── README.md
├── SKILL.md
├── HANDOFF.md
├── VERSION
├── references/
│   ├── cuisine-style-map.md
│   ├── dish-semantic-router.md
│   ├── execution-template.md
│   ├── fidelity-manifest.md
│   ├── fidelity-qc.md
│   ├── food-modules.md
│   ├── retry-policy.md
│   ├── scene-modules.md
│   ├── semantic-background-rules.md
│   └── semantic-qc.md
└── tests/
    └── test-cases.md
```

## 一句话定义

> **让同一份真实食物，在一个真正属于这道菜的环境中，被世界级商业摄影团队重新布光、重新布景、重新拍摄。**
