# ORE V0.2 Native Real 001 — First Red Precommit

Upstream issue: stellar-compliance-kit/compliance-adapters#565

Frozen upstream/base commit: `dd1283809945e131afdd9edbba48746ea0fd0d53`

Purpose: preserve a pre-repair execution point for the repository's existing CI and existing `sanctions-oracle/test/syncFailedReasons.test.ts` test.

No production/source code or test has been changed by this precommit. No repair is authorized before the First Red result is observed and preserved.

Expected observation from the existing repository state: the documented `SyncResult.failedWithReasons` field is referenced by the existing test but is absent from the `SyncResult` interface and omitted from the function return value. This expectation is not a PASS/FAIL claim until CI executes.

Claim boundary: internal repair-operation evidence only; no upstream merge, production readiness, external validation, or general correctness claim.
