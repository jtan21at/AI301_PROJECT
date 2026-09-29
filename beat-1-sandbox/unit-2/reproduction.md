# Unit 2 - Claim and Reproduce

Path: `beat-1-sandbox/unit-2/reproduction.md`

Record of the claim and reproduction on the issue selected for Unit 2, and
of the evaluation runs that produced `eval-run.txt`.

---

## Your identity upstream

**GitHub username**

jtan21at

---

## Posted upstream

**Claim comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5884560218

Hi, I'd like to investigate the malformed-password-hash behavior in
`verify_password` as a first contribution. I'll verify issue #72 on the
current `main` branch, record the exact environment, command, and exception,
and post the reproduction results here. After that, I plan to trace which
Passlib exception should be handled so verification fails closed without
changing valid-password behavior.

**Reproduction comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5884640208

I reproduced issue #72 on the current `main` branch.

Environment:

- PathReview commit `2f4e82f52efbcfcc57d65b3fa5348672163ca088`
- Windows 10.0.19045, x64
- Python 3.13.12
- pytest 9.1.1
- passlib 1.7.4
- bcrypt 4.3.0

Starting from a clean clone, I created a local virtual environment and
installed only the dependencies needed by the security test:

```powershell
python -m venv .venv
.\.venv\Scripts\python.exe -m pip install pytest "passlib[bcrypt]>=1.7.4" "bcrypt>=4.0.1,<5.0.0" "python-jose[cryptography]>=3.3.0" "pydantic-settings>=2.1.0"
.\.venv\Scripts\python.exe -m pytest tests\unit\test_security.py::TestSecurity::test_verify_with_wrong_hash_format -q -rxX
```

The targeted test reaches the expected strict xfail:

```text
XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
1 xfailed, 1 warning in 1.04s
```

I also called the function directly with the same values used by the test:

```powershell
.\.venv\Scripts\python.exe -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"
```

The call raises instead of returning a boolean:

```text
File "core\security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
passlib.exc.UnknownHashError: hash could not be identified
```

Control run:

```powershell
.\.venv\Scripts\python.exe -m pytest tests\unit\test_security.py -q -rxX
```

```text
24 passed, 1 xfailed, 1 warning in 6.73s
```

Expected: `verify_password("password", "not_a_valid_bcrypt_hash")` returns
`False`, so an unrecognized stored hash fails closed.

Actual: Passlib's `UnknownHashError` escapes from `pwd_context.verify()` at
`core/security.py:37`. The rest of `test_security.py` passes; only the
issue-specific test remains xfailed.

## Eval iterations

**Run history**

1. `18/20` scored packages agreed with the gold labels (`PASS`); every
   category matched at least one package. This was the first completed full
   run. An earlier launch was interrupted before producing a score because
   Windows used GBK for two package prompts; rerunning with Python UTF-8
   mode fixed the transport error without changing the rubric.

**Package analysis**

`pkg-20`: my rubric decides `reject`, matching the gold label `reject`.
The reproduction itself is strong, but the repo-facts block says Ghostty
requires disclosure of all AI use, including issue comments. Neither
candidate comment names the tool or extent of assistance, so the required
`repo-conventions` check fails even though the environment, steps,
artifacts, and conclusions pass.

**Check rationale**

> | behavior-matches-target | The repro report's raw artifacts (output, logs, measurements, screenshots, or control results), compared with the issue's described trigger, observed behavior, and expected behavior. | The artifacts visibly test the same trigger and distinguish the reported behavior from an adjacent error or normal operation. A reproduction shows the issue-specific symptom; a cannot-reproduce shows the attempted trigger and observable non-occurrence. Version or input deviations are not silently substituted for the target. | required |

I wrote this check around observable outcomes rather than report length or
format. That makes a short but faithful transcript sufficient, accepts an
honest cannot-reproduce when the attempt is shown, and rejects polished
reports whose command or output demonstrates a nearby error instead of the
issue's actual symptom.

**Trade-offs**

This check deliberately rejects a report when its prose sounds correct but
the available artifact cannot distinguish the target behavior from normal
operation. That can hold back a genuine reproduction whose key evidence is
difficult to capture, but posting an uncheckable confirmation would cost a
maintainer more time. In that case I would add a focused log, measurement,
screenshot, or control before posting rather than loosen the check.

---

Related paths: `eval-run.txt` in this directory; the skill files in
`tools/repro-check/`.
