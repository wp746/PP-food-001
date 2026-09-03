# Release Gate V1.0.0

Before treating this runtime as portable production-ready, verify:

```text
[ ] T01 Explicit A = A only
[ ] T02 Explicit B = current A → PASS → B
[ ] T03 Current-job isolation
[ ] T04 Runtime minimalism
[ ] T05 Fixed prompt compiler
[ ] T06 Vision/Image role separation
[ ] T07 B copy gate
[ ] T08 Default-copy authorization boundary
[ ] T09 Product Hero priority
[ ] T10 One current category profile
[ ] T11 Targeted retry only
[ ] T12 Fail closed
[ ] T13 Prompt payload boundary
[ ] T14 Setup/startup state machine
[ ] T15 Fidelity over design aggression
```

These checks are defined in `tests/runtime-contract-tests.md`.

The runtime may be installed for controlled pilot testing when all rules are represented in production files. Cross-agent equivalence must still be validated with the same Golden Set on each target host because model/runtime implementations differ.
