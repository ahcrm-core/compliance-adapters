# ORE V0.2 Native Real 001 — Adversarial Contract Result

- Case: ORE-V0.2-NATIVE-REAL-001
- Upstream issue: stellar-compliance-kit/compliance-adapters#565
- Repair commit: e25bc0db6f2d2e34f9e265ef3dc0705593322145
- Adversarial workflow head: b75d3527994d6211e158f89a874e2f660f871f19
- GitHub Actions run: 35928601476
- Job: 107409559422
- Result: SUCCESS
- Scope: adversarial narrow source contract only.

The adversarial check verified the field type and uniqueness, typed accumulator, preservation of address and error reason in failure records, and inclusion of failedWithReasons in the SyncResult-like return.

Claim boundary:
- The unchanged behavioral test is still blocked by unrelated upstream TypeScript/dependency errors.
- This does not establish full repository health, production readiness, upstream acceptance, or general ORQELON superiority.
- The preserved First Red remains part of the permanent evidence chain.
