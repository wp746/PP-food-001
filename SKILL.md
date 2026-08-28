---
name: universal-food-commercial-photography
description: Use when turning a user-provided food photo into a high-fidelity premium commercial food image while preserving the exact product, ingredient geometry, vessel/packaging, plating and physical relationships.
version: 6.0.1
---

# PP-food-001 V6.0.1

## Mandatory Entry

**Do not start production from this file alone.**

Before any food analysis, prompt building or image generation:

```text
READ BOOTSTRAP.md
→ complete Mandatory Read Order
→ run PRE_FLIGHT_CHECKLIST.md
→ PRODUCTION_GATE must PASS
```

`RUNTIME_MANIFEST.md` is the canonical P0 runtime rule source. If a summary, old conversation, host default behavior or another file appears to weaken a P0 rule, do not silently override the manifest.

## Role

本 Skill 是 **Stage A / Commercial Re-photography Engine**：

```text
CURRENT USER IMAGE
→ VISION_MODEL analysis
→ CURRENT_JOB_FACTS / Fidelity Manifest
→ Stage A Execution Contract
→ IMAGE_MODEL reference-image edit
→ Stage A QC
→ targeted retry if needed
→ Stage A PASS image
```

它只允许升级摄影与环境，不允许为了“高级感”重做真实产品。

## Runtime Protocol

必须使用：

- `BOOTSTRAP.md` — 冷启动与恢复流程；
- `RUNTIME_MANIFEST.md` — 9:16、A/B、Food Fidelity、Hero、Capability Evidence、Fail-Closed 等 P0 规则；
- `REQUIRED_READ_SET.md` — `COLD_START_ALWAYS_LOAD / A_JOB_ALWAYS_LOAD / CATEGORY_CONDITIONAL_LOAD`；
- `PRE_FLIGHT_CHECKLIST.md` — READY、Declared/Verified capability evidence 与生产门禁；
- `EXECUTION_CONTRACT_TEMPLATE.md` — 每个当前任务的短合同；
- `HANDOFF.md` — 模型能力、凭据与 Runtime Profile 交接。

生产时不要把整仓库 Markdown 原样拼进图片 Prompt。先读取规则，再把当前任务编译成 `EXECUTION_CONTRACT`，最后从合同生成短而明确的 IMAGE_MODEL 指令。

## Capability Evidence Rule

READY 不等于端到端已验证。必须区分：

```text
RUNTIME_CAPABILITIES_DECLARED = PASS / BLOCKED
RUNTIME_CAPABILITIES_VERIFIED = PASS / PENDING / BLOCKED
FIRST_LIVE_VERIFICATION_REQUIRED = TRUE / FALSE
```

若当前配置没有匹配的 verified Runtime Profile，第一笔真实业务调用兼任验证；不要额外生成无业务价值测试图。配置 fingerprint 不变时可跨会话复用已验证 profile。

## A / B Relationship

A/B 具体优先级以 `RUNTIME_MANIFEST.md` 为唯一真相。

Stage A 的职责始终相同：锁产品 → 商拍 → QC。

当当前意图为 B 时，本 Skill 仍必须先完成 Stage A；只有当前任务 Stage A PASS 图才能交给 `PP-food-KV-001`。

## Detailed Methods

不要自行挑文件。按 `REQUIRED_READ_SET.md` 执行。

核心详细规则仍保留在 `references/`：Fidelity Manifest / QC、Hero Shot Mandate、Dish Semantic Router、Semantic Background / QC、Cuisine / Food / Scene Modules、Execution Template、Targeted Retry。

这些 references 解释“怎么做”；`RUNTIME_MANIFEST.md` 决定“什么绝不能违反”。

## Acceptance

必须执行 `tests/runtime-handoff-tests.md` 和 `tests/test-cases.md` 的行为约束。

Mandatory Read、Pre-flight、Execution Contract 或 declared runtime ability 任一无法确认：

```text
PRODUCTION_GATE = BLOCKED
```

禁止先出图再补规则。

## Security Boundary

仓库不得保存具体供应商名、私有聚合平台配置、实际 API Base URL、API Key、私有凭据或 Runtime Profile 真实运行值。运行值由宿主 Secret / Environment / Connection / 私有持久状态提供。