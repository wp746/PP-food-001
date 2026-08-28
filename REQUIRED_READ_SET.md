# PP-food-001 Required Read Set

本文件把“必须读”和“按任务读”分开，避免智能体自己判断后漏读，也避免每次把整个仓库塞进上下文造成噪声。

## ALWAYS_LOAD｜冷启动必须完整读取

```text
references/fidelity-manifest.md
references/fidelity-qc.md
references/hero-shot-mandate.md
references/retry-policy.md
references/semantic-background-rules.md
references/semantic-qc.md
references/dish-semantic-router.md
references/execution-template.md
tests/runtime-handoff-tests.md
tests/test-cases.md
```

不得用“已摘要”“大概知道”代替正文读取。

## READ-PROOF CHECKPOINTS

读完 ALWAYS_LOAD 后必须能回答：

1. `fidelity-manifest.md`：Region A/B/C 的自由度分别是什么？
2. `fidelity-qc.md`：Critical Failure 是否覆盖数字评分？最终 Fidelity/Photography 门槛是什么？
3. `hero-shot-mandate.md`：Priority 0 是什么？为什么默认高级材质舞台而非真实经营场所？四层空间是什么？Hero/Appetite 阈值是多少？
4. `retry-policy.md`：Attempt 1/2/3 如何逐级收紧？为什么禁止随机整张重抽？
5. `semantic-background-rules.md`：如何避免通用背景与温度错配？
6. `semantic-qc.md`：语义相关性如何判 FAIL？
7. `dish-semantic-router.md`：低/中/高置信度如何影响路由激进度？
8. `execution-template.md`：最终 IMAGE_MODEL 指令必须先锁什么、后开放什么？
9. 两份 tests：默认 9:16、A/B、Fail Closed、Execution Contract 的回归要求是什么？

无法回答任何一项 → 重新读取对应文件。

## CONDITIONAL_LOAD｜每个任务按需读取

### 品类/菜系舞台映射

识别当前食品后，必须读取 `references/cuisine-style-map.md` 中对应品类/菜系条目；不要无差别加载整份长文档到每个任务上下文。

### Food material module

需要具体材质表现时读取：

```text
references/food-modules.md
```

只加载与当前主体直接相关的 1 个主模块 + 必要的少量辅模块。

### Scene / support module

需要场景支撑模块时读取：

```text
references/scene-modules.md
```

其内容不得覆盖 `RUNTIME_MANIFEST.md` 的“高级材质舞台、非默认真实经营场所”P0 规则。

## Production Rule

冷启动读完 ALWAYS_LOAD 后，后续每个新任务至少刷新：

```text
RUNTIME_MANIFEST.md
当前品类对应的 CONDITIONAL section
EXECUTION_CONTRACT_TEMPLATE.md
```

如果上下文压缩导致 ALWAYS_LOAD 的关键规则无法证明仍在活跃上下文，重新执行 BOOTSTRAP。