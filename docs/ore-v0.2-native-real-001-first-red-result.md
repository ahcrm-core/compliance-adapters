# ORE V0.2 Native Real 001 — First Red Preservation

- Case: ORE-V0.2-NATIVE-REAL-001
- Upstream issue: stellar-compliance-kit/compliance-adapters#565
- Frozen upstream base: dd1283809945e131afdd9edbba48746ea0fd0d53
- First-Red head: 588a99aeb6f067923e4eda478b28c12101549aee
- GitHub Actions run: 35927617807
- Job: 107406351121
- Environment: Node.js 22
- Command: npm test --workspace=sanctions-oracle -- --runInBand test/syncFailedReasons.test.ts
- Result: FIRST RED CONFIRMED
- Test suite: 1 failed, 1 total; 0 tests executed because TypeScript compilation failed.
- Primary failure: TS2339 — Property 'failedWithReasons' does not exist on type 'SyncResult' at test/syncFailedReasons.test.ts lines 31, 36, 55, and 69.
- Secondary TS7006 at line 36 follows from the missing typed property.
- Source and target test were unchanged before this First Red.
- Earlier environment/install and unrelated workspace-build failures are not classified as the issue First Red.

## Root-cause hypothesis before repair

The implementation already accumulates `failedWithReasons: FailedAddress[]`, and the SyncResult documentation references `SyncResult.failedWithReasons`, but the public `SyncResult` interface does not declare that field and the final returned object omits it.

## Frozen repair boundary

Only the smallest source repair needed to expose the already-computed field is authorized for the next step:
1. declare `failedWithReasons: FailedAddress[]` on `SyncResult`;
2. include `failedWithReasons` in the final result object.

Do not alter the existing target test. Do not repair unrelated repository build failures. Preserve this First Red permanently.
