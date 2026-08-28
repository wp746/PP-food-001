# PP-food-001 Required Read Set

目标：**不漏读关键规则，也不把所有菜品语义一次性灌进冷启动上下文。**

## COLD_START_ALWAYS_LOAD｜冷启动核心必读

```text
references/fidelity-manifest.md
references/fidelity-qc.md
references/hero-shot-mandate.md
references/retry-policy.md
tests/runtime-handoff-tests.md
tests/test-cases.md
```

这些文件与任何具体菜品无关，负责产品保真、Hero 标准、重试和运行门禁。

不得用摘要或“大概知道”代替正文。

## COLD-START READ-PROOF

必须能回答：

1. `fidelity-manifest.md`：Region A/B/C 自由度分别是什么？
2. `fidelity-qc.md`：Critical Failure 是否覆盖数字评分？最终 Fidelity/Photography 门槛是什么？
3. `hero-shot-mandate.md`：Priority 0 是什么？高级材质舞台、四层空间、Hero/Appetite 阈值分别是什么？
4. `retry-policy.md`：Attempt 1/2/3 如何逐级收紧？为什么禁止随机整张重抽？
5. 两份 tests：9:16、A/B、Execution Contract、Fail Closed、Current Job Isolation 的回归要求是什么？

答不准任何一项 → 重读对应文件。

## A_JOB_ALWAYS_LOAD｜每个 Stage A 任务必读

拿到当前用户图片并完成初步视觉识别后，每个 A 任务必须读取：

```text
references/execution-template.md
references/semantic-qc.md
references/dish-semantic-router.md
references/semantic-background-rules.md
```

但只把**当前任务需要的规则**编译进 Execution Contract，不把文档中的其他菜品示例写入 Prompt。

### A-Job Proof

进入 IMAGE_MODEL 前必须确认：

```text
CURRENT_SEMANTIC_ROUTE = RESOLVED_OR_CONSERVATIVE_FALLBACK
TEMPERATURE_LOGIC = RESOLVED
MATERIAL_STAGE_DIRECTION = RESOLVED
SEMANTIC_QC_RULE = LOADED
EXECUTION_TEMPLATE = LOADED
```

## CATEGORY_CONDITIONAL_LOAD｜按当前食品加载

### Cuisine / Category Material Stage

识别当前品类后，读取：

```text
references/cuisine-style-map.md
```

只使用当前品类/菜系对应条目，不把整份长文档的所有菜品语义注入当前 Contract。

### Food material module

需要更细的材质表现时读取：

```text
references/food-modules.md
```

只选 1 个主模块 + 必要的少量辅模块。

### Scene / Support module

确有物理呈现/原场景关系需要时读取：

```text
references/scene-modules.md
```

其内容不得覆盖 `RUNTIME_MANIFEST.md` 的 P0 Hero Stage 规则。

## Production Refresh

每个新任务至少刷新：

```text
RUNTIME_MANIFEST.md
A_JOB_ALWAYS_LOAD
当前 CATEGORY_CONDITIONAL_LOAD
EXECUTION_CONTRACT_TEMPLATE.md
```

上下文压缩后如果无法证明 Cold-Start Core 仍在活跃上下文，重新执行 BOOTSTRAP。