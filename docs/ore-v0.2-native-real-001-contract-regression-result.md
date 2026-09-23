# ORE V0.2 Native Real 001 — Narrow Contract Regression Result

- Case: ORE-V0.2-NATIVE-REAL-001
- Upstream issue: stellar-compliance-kit/compliance-adapters#565
- Repair commit: e25bc0db6f2d2e34f9e265ef3dc0705593322145
- Contract workflow head: fdb184c1c5cab6af6a233e31bf5bebe9f1eb366c
- GitHub Actions run: 35928290851
- Job: 107408548795
- Result: SUCCESS
- Scope: narrow source contract only.

Verified within this narrow scope:
1. SyncResult declares failedWithReasons: FailedAddress[].
2. syncSanctionsToDenylist creates the failedWithReasons accumulator.
3. the implementation populates the accumulator.
4. the returned SyncResult object includes failedWithReasons.

Claim boundary:
- This does not establish that the unchanged behavioral test passes.
- The unchanged behavioral test remains blocked by unrelated upstream TypeScript/dependency errors.
- This does not establish full repository build health, production readiness, or upstream acceptance.
- The preserved First Red remains authoritative evidence of the pre-repair defect.
