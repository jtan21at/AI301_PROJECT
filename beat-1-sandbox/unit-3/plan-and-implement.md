# Unit 3 — Plan and Build

## Posted upstream

**GitHub username**

jtan21at

**Plan comment**

https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-6011483709

My plan for #72 builds on [my reproduction](https://github.com/codepath/pathreview-ai301-fa26-s3/issues/72#issuecomment-5884640208) at `2f4e82f52efbcfcc57d65b3fa5348672163ca088` (Windows, Python 3.13.12, Passlib 1.7.4, bcrypt 4.3.0).

The real call `verify_password('password', 'not_a_valid_bcrypt_hash')` raised `passlib.exc.UnknownHashError: hash could not be identified` at the unguarded `pwd_context.verify()` call in `core/security.py`. The security module reported `24 passed, 1 xfailed`; the marked test expects `False`.

I plan to catch only `UnknownHashError` in `verify_password()` and return `False`, then remove the issue-specific strict xfail from `tests/unit/test_security.py`, as the issue and contribution guide request. Other exceptions will still propagate. No hashing, JWT, authentication-route, dependency, or unrelated-test changes are planned.

Validation: repeat the direct call (expect `False` without a traceback), run `test_verify_with_wrong_hash_format` (expect a normal pass, not xfail/XPASS), and run the full security module (expect 25 passing tests, preserving valid-password and wrong-password controls). I will save the commands and actual before/after output.

This addresses the reproduced unrecognized-hash case. Other structurally malformed hashes may raise different errors; I am not claiming they are covered by this narrow fix. The branch is `fix/72-invalid-password-hash` in my fork; I will review the diff and record any deviation before preparing the Unit 4 PR.

Update before posting: this comment is being posted after a local implementation, not before the build. The two-file change described above is implemented, committed as `a861730`, and pushed to `fix/72-invalid-password-hash` in my fork: the direct call now prints `False`, the targeted test reports `1 passed`, and the full security module reports `25 passed`. No implementation changes beyond the plan were needed.

AI assistance: I  review the reproduction, draft this plan, implement the narrow fix, and run validation. The resulting diff is available for review; this commit contains only the two source/test files, not the local plan drafts.


## Your branch

**Branch**

`fix/72-invalid-password-hash`

Committed as a8617308aff2fa7149a50fbd14f6c5c74e9fa80b and pushed to origin/fix/72-invalid-password-hash.

Branch: https://github.com/jtan21at/pathreview-ai301-fa26-s3/tree/fix/72-invalid-password-hash

The comment text above is copied exactly from the published GitHub comment.

**Evidence**

The same three commands were run in the existing Unit 2 environment,
first on the original implementation, then on the real two-file fix.

Before:

```text
$ "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Scripts\python.exe" -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -q -rxX
x                                                                        [100%]
============================== warnings summary ===============================
core\config.py:7
  D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\core\config.py:7: PydanticDeprecatedSince20: Support for class-based `config` is deprecated, use ConfigDict instead. Deprecated in Pydantic V2.0 to be removed in V3.0. See Pydantic V2 Migration Guide at https://errors.pydantic.dev/2.13/migration/
    class Settings(BaseSettings):

.venv\Lib\site-packages\_pytest\cacheprovider.py:469
  D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Lib\site-packages\_pytest\cacheprovider.py:469: PytestCacheWarning: could not create cache path D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.pytest_cache\v\cache\nodeids: [WinError 5] Access is denied: 'D:\\codepath ai301\\WK2\\pathreview-ai301-fa26-s3\\.pytest_cache\\v\\cache'
    config.cache.set("cache/nodeids", sorted(self.cached_nodeids))

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
=========================== short test summary info ===========================
XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
1 xfailed, 2 warnings in 4.35s

Exit code: 0

$ "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Scripts\python.exe" -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"
Traceback (most recent call last):
  File "<string>", line 1, in <module>
    from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))
                                                     ~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\core\security.py", line 37, in verify_password
    return bool(pwd_context.verify(plain_password, hashed_password))
                ~~~~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Lib\site-packages\passlib\context.py", line 2343, in verify
    record = self._get_or_identify_record(hash, scheme, category)
  File "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Lib\site-packages\passlib\context.py", line 2031, in _get_or_identify_record
    return self._identify_record(hash, category)
           ~~~~~~~~~~~~~~~~~~~~~^^^^^^^^^^^^^^^^
  File "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Lib\site-packages\passlib\context.py", line 1132, in identify_record
    raise exc.UnknownHashError("hash could not be identified")
passlib.exc.UnknownHashError: hash could not be identified

Exit code: 1

$ "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Scripts\python.exe" -m pytest tests/unit/test_security.py -q -rxX
.....................x...                                                [100%]
============================== warnings summary ===============================
core\config.py:7
  D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\core\config.py:7: PydanticDeprecatedSince20: Support for class-based `config` is deprecated, use ConfigDict instead. Deprecated in Pydantic V2.0 to be removed in V3.0. See Pydantic V2 Migration Guide at https://errors.pydantic.dev/2.13/migration/
    class Settings(BaseSettings):

.venv\Lib\site-packages\_pytest\cacheprovider.py:469
  D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Lib\site-packages\_pytest\cacheprovider.py:469: PytestCacheWarning: could not create cache path D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.pytest_cache\v\cache\nodeids: [WinError 5] Access is denied: 'D:\\codepath ai301\\WK2\\pathreview-ai301-fa26-s3\\.pytest_cache\\v\\cache'
    config.cache.set("cache/nodeids", sorted(self.cached_nodeids))

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
=========================== short test summary info ===========================
XFAIL tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format - issue #72 (manifest H-05): password verify raises UnknownHashError instead of returning False
24 passed, 1 xfailed, 2 warnings in 8.43s

Exit code: 0

```

After:

```text
$ "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Scripts\python.exe" -m pytest tests/unit/test_security.py::TestSecurity::test_verify_with_wrong_hash_format -q -rxX
.                                                                        [100%]
============================== warnings summary ===============================
core\config.py:7
  D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\core\config.py:7: PydanticDeprecatedSince20: Support for class-based `config` is deprecated, use ConfigDict instead. Deprecated in Pydantic V2.0 to be removed in V3.0. See Pydantic V2 Migration Guide at https://errors.pydantic.dev/2.13/migration/
    class Settings(BaseSettings):

.venv\Lib\site-packages\_pytest\cacheprovider.py:469
  D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Lib\site-packages\_pytest\cacheprovider.py:469: PytestCacheWarning: could not create cache path D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.pytest_cache\v\cache\nodeids: [WinError 5] Access is denied: 'D:\\codepath ai301\\WK2\\pathreview-ai301-fa26-s3\\.pytest_cache\\v\\cache'
    config.cache.set("cache/nodeids", sorted(self.cached_nodeids))

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
1 passed, 2 warnings in 0.65s

Exit code: 0

$ "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Scripts\python.exe" -c "from core.security import verify_password; print(verify_password('password', 'not_a_valid_bcrypt_hash'))"
False

Exit code: 0

$ "D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Scripts\python.exe" -m pytest tests/unit/test_security.py -q -rxX
.........................                                                [100%]
============================== warnings summary ===============================
core\config.py:7
  D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\core\config.py:7: PydanticDeprecatedSince20: Support for class-based `config` is deprecated, use ConfigDict instead. Deprecated in Pydantic V2.0 to be removed in V3.0. See Pydantic V2 Migration Guide at https://errors.pydantic.dev/2.13/migration/
    class Settings(BaseSettings):

.venv\Lib\site-packages\_pytest\cacheprovider.py:469
  D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.venv\Lib\site-packages\_pytest\cacheprovider.py:469: PytestCacheWarning: could not create cache path D:\codepath ai301\WK2\pathreview-ai301-fa26-s3\.pytest_cache\v\cache\nodeids: [WinError 5] Access is denied: 'D:\\codepath ai301\\WK2\\pathreview-ai301-fa26-s3\\.pytest_cache\\v\\cache'
    config.cache.set("cache/nodeids", sorted(self.cached_nodeids))

-- Docs: https://docs.pytest.org/en/stable/how-to/capture-warnings.html
25 passed, 2 warnings in 7.11s

Exit code: 0

```

The module changed from 24 passed / 1 xfailed to 25 passed, and the direct
call changed from UnknownHashError to False. Both runs show existing
Pydantic deprecation and pytest cache-permission warnings. Targeted tests
and git diff --check passed; full application CI was not run.

## Eval iterations

**Run history**

No official Claude harness run occurred: Claude quota was exhausted.
One informal Zed assistant review covered all 20 scored Markdown packages,
using the authored skill before reading gold labels. It produced 5 accept
and 15 reject verdicts. An answer-key comparison performed afterward found
18/20 agreement: clear-accept 5/7, scope-creep 4/4, wrong-cause 4/4,
unbuildable 3/3, thread-convention 2/2. The original judgments were retained;
no model regrading or official PASS is claimed. This is the same unofficial
18/20 comparison appended to eval-run.txt. Staff acceptance of the
alternative is unconfirmed.

**Package analysis**

`pkg-01`: the informal rubric verdict was `reject`; the gold label is
`reject`. The plan claims “The Python-version difference is a red herring;
the tokenizer has always been too strict,” but the reproduction says
“the request items are never handed to HTTPie's item parser.” The same
items parse without the verbose flag, so blaming the item tokenizer
contradicts the control and observed failure layer. The grounded-diagnosis
check therefore holds the plan even though its wording sounds confident.

**Check rationale**

> | grounded-diagnosis | Candidate plan's cause and quoted repro evidence, compared with the issue trigger, observed result, and expected result. | The diagnosis explains the reproduced behavior without contradicting its artifacts or replacing the trigger. An unproven cause is identified as a hypothesis with a concrete verification step, not asserted as established fact. | required |

I chose an evidence-and-hypothesis rule rather than requiring a particular
heading or an exhaustive code trace. A terse plan can pass if its cause
explains the reproduced trigger; a polished plan must fail when its cause
contradicts the control. A specific investigation gate allows honest
uncertainty without treating every tentative diagnosis as unbuildable.
No claim is made that this rule was revised through official eval runs.

**Trade-offs**

This rule can be too strict about a plausible mechanism inferred from
observed behavior. The frozen informal review rejected pkg-03 and pkg-14,
while gold accepts both: the key treats tool-by-tool support checks in
pkg-03 and the scoped reattach fix in pkg-14 as sufficient handling of
unknowns. I retained those disagreements rather than changing judgments
after seeing the key. No --only canary or official rerun was performed.
Future calibration should distinguish unsupported certainty from a
reasonable working explanation paired with a bounded verification plan.

## Outstanding submission actions and process deviations

- Review every implementation diff before keeping or committing it.
- Completed: the plan comment is posted; its verified permalink and exact text appear above.
- Completed: the fork commit contains only core/security.py and tests/unit/test_security.py; plan.md and comment.md were excluded.
- Completed: the fix branch and course-repo artifacts are pushed; this comment-link update is committed separately.
- Ask staff whether this transparently labeled, non-harness evaluation is acceptable.
- Public posting will follow the local build, unlike the assignment's post-before-build order.
- Submit the whole course repository URL in the portal and enter actual hours spent.
