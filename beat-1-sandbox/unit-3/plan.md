# Fix issue #72: unrecognized password hashes fail closed

Issue: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72
Fork: https://github.com/jtan21at/pathreview-ai301-fa26-s3
Reproduction: https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5884640208

This plan was reviewed by the current Zed assistant using the installed plan-check rubric, not Claude CLI. The issue body, relevant maintainer/student thread comments, and docs/CONTRIBUTING.md were checked. The comment is prepared but not yet publicly posted.

## Diagnosis and quoted reproduction evidence

The Unit 2 report used commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`, Windows 10.0.19045 x64, Python 3.13.12, pytest 9.1.1, Passlib 1.7.4, and bcrypt 4.3.0. It called the real function, not a stand-in:

```powershell
.\.venv\Scripts\python.exe -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"
```

Quoted result:

```text
File "core\security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
passlib.exc.UnknownHashError: hash could not be identified
```

The targeted regression currently has strict xfail:

```text
XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
1 xfailed, 1 warning in 1.04s
```

The control report was:

```text
24 passed, 1 xfailed, 1 warning in 6.73s
```

Inspection of `core/security.py` shows `verify_password` returns the result of `pwd_context.verify` without handling this exception. The reproduced unrecognized hash therefore escapes rather than producing the documented boolean rejection. This supports a narrow exception-boundary fix, not a change to hash creation or authentication routes.

## Scope and files to touch

- `core/security.py`: import Passlib's `UnknownHashError`, catch that exception around verification, and return `False` for an unrecognized stored hash.
- `tests/unit/test_security.py`: remove only issue #72's strict xfail marker so the existing assertion becomes a mandatory regression. Add a focused propagation test for unrelated operational exceptions if needed to prove the catch remains narrow.
- Out of scope: hashing algorithms, dependency upgrades, password policy, JWT handling, route changes, broad exception suppression, database cleanup, and unrelated xfails.
- `plan.md` and `comment.md` remain local drafts, never part of the fix commit. The completed plan is separately submitted in the course repo.

## Approach

1. Read the current issue and contribution rules, then re-run the direct repro and targeted test in the existing Unit 2 environment; save raw outputs before modifying code. This baseline has been saved in tests-before.txt.
2. Verify that the failing exception is `passlib.exc.UnknownHashError` in that installed Passlib version.
3. Wrap only `pwd_context.verify` in a try/except for `UnknownHashError`, preserving valid-hash success and wrong-password rejection. Do not catch `Exception`, `TypeError`, or general `ValueError`.
4. Remove the specific xfail marker and run the targeted test, direct call, and full security test module. Review the complete diff before retaining it.
5. Record deviations honestly, re-grade the completed plan if the approach changes, and retain commands and outputs for the course submission.

## Test plan

Run in the Path Review fork root using the existing `.venv`:

```powershell
.\.venv\Scripts\python.exe -m pytest tests\unit\test_security.py::TestSecurity::test_verify_with_wrong_hash_format -q -rxX
.\.venv\Scripts\python.exe -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"
.\.venv\Scripts\python.exe -m pytest tests\unit\test_security.py -q -rxX
```

Expected after the fix: the targeted test passes normally (not xfail or strict XPASS); the direct call prints `False` without a traceback; the security module's valid-password, incorrect-password, case, salt, whitespace, and token tests continue to pass. If no extra test is added, the existing module should report 25 passed; any added regression changes that count and will be documented with actual output.

If a propagation test is added, monkeypatch `pwd_context.verify` to raise `RuntimeError` and assert it still escapes, proving backend faults are not silently converted to bad credentials. Run that new check on the old implementation as a control and the fix as a regression.

## Risks and unknowns

- The demonstrated input is an unrecognized hash. A recognized but structurally corrupt bcrypt hash may raise a different exception; this plan makes no claim that all corruption is covered. Broaden the boundary only if the issue and new evidence require it, then record the change.
- Swallowing broad exceptions could hide backend faults; catch only the observed Passlib exception.
- Keep the Unit 2 dependency versions for comparable evidence; bcrypt compatibility warnings are not automatically part of this issue.
- Removing strict xfail is required: leaving it in place would turn a correct fix into a failing XPASS.
- The issue explicitly requires removing its xfail marker. docs/CONTRIBUTING.md requires an issue-number branch, relevant tests, and green checks for a future PR; do not claim full CI is green from a targeted module run. Relevant thread review found the student's claim and reproduction and no additional maintainer constraints. The plan comment discloses Zed AI assistance and is not yet posted.

## Deviations

The implementation followed the proposed two-file change: catch only UnknownHashError and remove the issue-specific xfail marker. No extra propagation test was added; existing valid-password and wrong-password controls remained passing. The direct call now prints False, the targeted test reports 1 passed, and the complete security module reports 25 passed. Raw commands and output are saved in tests-before.txt and tests-after.txt.

Process deviations: Claude quota was exhausted, so both skill evaluation and live plan review were performed by the   Claude CLI. The 20-package review was frozen before reading gold labels, then independently compared with the answer key (18/20 agreement);   Public plan posting remains pending student approval, so the build occurred before the public plan comment rather than after it as the assignment requests. These alternatives require staff acceptance and are not claimed to fulfill the official eval or post-before-build requirements.
