# Startup Protocol

## State Machine

```text
UNCONFIGURED
→ SETUP_GATE
→ READY_WAITING_FOR_START
→ user says 启动
→ PRODUCTION
```

## READY Response
When Setup Gate passes, report only concise status:

```text
PP Food Runtime 已准备就绪。
DECLARED = PASS
VERIFIED = PASS | PENDING
回复“启动”进入生产模式。
```

Do not expose internal prompt/contracts unless asked.

## Production Mode
After `启动`:
- do not re-ask model/API configuration every job;
- accept natural-language product information;
- `执行A` invokes A executor only;
- `执行B` invokes current A then B;
- each new image creates a new current-job state;
- configuration is re-opened only on real runtime failure, fingerprint change, credential failure or missing capability.

## Recovery
On runtime failure:
```text
RUNTIME_STATE = SETUP_GATE
PRODUCTION_GATE = BLOCKED
```
Ask only for the missing/failed item.
