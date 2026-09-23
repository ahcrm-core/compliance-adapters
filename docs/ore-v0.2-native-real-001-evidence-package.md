# ORE V0.2 Native Real 001 — Evidence Package

## Identity
- Case: ORE-V0.2-NATIVE-REAL-001
- Upstream: stellar-compliance-kit/compliance-adapters
- Issue: #565 — SyncResult.failedWithReasons is computed but never returned or added to the SyncResult type
- Frozen upstream base: dd1283809945e131afdd9edbba48746ea0fd0d53
- Repair branch: ore-v0.2-native-real-001
- Minimal repair commit: e25bc0db6f2d2e34f9e265ef3dc0705593322145

## Preserved First Red
- Run: 35927617807
- Job: 107406351121
- Head: 588a99aeb6f067923e4eda478b28c12101549aee
- Command: npm test --workspace=sanctions-oracle -- --runInBand test/syncFailedReasons.test.ts
- Result: FAIL before test execution because TypeScript reported TS2339: Property 'failedWithReasons' does not exist on type 'SyncResult' at the unchanged target test.
- Source and target test were unchanged for this First Red.

Earlier setup failures are preserved separately and are not classified as the issue First Red:
- Node 20 dependency-engine incompatibility.
- stale package-lock/package.json preventing npm ci.
- unrelated workspace TypeScript build failures.

## Root Cause
The implementation already accumulated failedWithReasons: FailedAddress[] and documentation referenced SyncResult.failedWithReasons, but the public SyncResult interface omitted the field and the final SyncResult return omitted it.

## Minimal Repair
Only sanctions-oracle/src/sync.ts was changed for the defect:
1. declare failedWithReasons: FailedAddress[] on SyncResult;
2. return failedWithReasons in the final SyncResult object.

The existing target test was not changed. Unrelated upstream failures were not repaired.

## Post-repair evidence
### Unchanged behavioral test
Run 35928011926 reached the unchanged target test. The original TS2339 failedWithReasons defect no longer appeared, but compilation remained blocked by unrelated existing TypeScript/dependency errors. Therefore full behavioral PASS is NOT established.

### Narrow contract regression
- Run: 35928290851
- Job: 107408548795
- Result: SUCCESS
Verified only that the typed field, accumulator, population, and returned field are present.

### Adversarial narrow contract
- Run: 35928601476
- Job: 107409559422
- Result: SUCCESS
Attacked field type/uniqueness, accumulator, address/error preservation, and return inclusion.

## Live upstream / competition check
Observed after adversarial validation:
- upstream main remained dd1283809945e131afdd9edbba48746ea0fd0d53; no drift from frozen base;
- issue #565 remained open and unassigned;
- a contributor, wisdom2030-dotcom, had applied to work on #565 through the Stellar Wave Program;
- no upstream submission is authorized by this package.

Operational disposition: WAIT_FOR_MAINTAINER / MONITOR_COMPETITOR until assignment/maintainer policy is clear. Do not create a duplicate upstream PR merely because a local repair exists.

## Claim boundary
Established:
- a valid First Red for the reported missing public field;
- a minimal source repair;
- disappearance of that specific TS2339 failure on the post-repair attempt;
- narrow contract regression PASS;
- adversarial narrow contract PASS;
- no upstream drift at the recorded check.

Not established:
- full unchanged behavioral test PASS;
- full repository build health;
- upstream acceptance or merge;
- production readiness;
- independent validation or general superiority of ORQELON.

Human/upstream maintainer authority remains final.
