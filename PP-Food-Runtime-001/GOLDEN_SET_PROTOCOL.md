# Golden Set Cross-Agent Validation

The Runtime Pack reduces execution drift but cannot make different host models mathematically identical. Release stability must be measured with the same Golden Set.

## Minimum Golden Set
Use at least 6 fixed source images:
1. Chinese hot dish / noodles;
2. bakery bread;
3. dessert/cake;
4. cold beverage/fruit ice;
5. packaged retail product;
6. multi-product or difficult vessel/packaging scene.

For each image run:
```text
A once
B once with fixed copy
```
using the same runtime version and same configured VISION/IMAGE model route.

## Record
For every target host record:
- A fidelity pass/fail;
- A hero/background pass/fail;
- B product dominance;
- B copy accuracy;
- category match;
- previous-skin contamination;
- retry count;
- exact prompt compiler block compliance;
- whether current Stage A PASS was actually passed into B.

## Release Decision
A host is production-qualified only when:
```text
A hard-gate pass rate >= 90%
B hard-gate pass rate >= 90%
B current-A bridge success = 100%
previous-job contamination = 0
hard-fact hallucination = 0
```

If a host fails, fix the smallest runtime/connector cause. Do not add broad new prose rules unless the failure appears across multiple Golden Set cases.
