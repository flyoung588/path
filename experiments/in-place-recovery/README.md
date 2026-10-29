# Round 6 Track D — interruption and rollback safety

Event check: prior Gambit-Checkmate/boltons PR1 is open and unchanged with no comments/reviews; upstream676 is unchanged and the native socket test is absent from its exact diff. No chase comment was posted. Root handles the prior settings contribution.

Discovery: 30 current PR rows. More-itertools1322 already absorbed other contributors' read-bound tests; path264 already fixed another contributor's self-copy loss report. D selected jaraco/path273, which had no discussion and changes in-place setup recovery.

New external collaboration PR: https://github.com/Apeksha9389/path/pull/1 targets the existing author's fix/inplace-setup-rollback branch, not upstream default.

Exact production+native-test commit: 422ace870c13d7b22e8f5a7926bd9721460cd773.

The candidate catches BaseException after stream teardown and cleans up the backup only on successful completion. This restores on KeyboardInterrupt/SystemExit during reader setup, writer setup and context body, and retains the backup if rollback rename itself raises. Eight tests all fail on author head bf1696f1e0b3f761a84510b400b042f7eae1537f; all pass with the patch. Existing news fragment updated; no license file was committed.

Validation:
- Author-head plus eight tests: 8 failed (candidate-before.txt).
- Patched TestInPlace: 15 passed (patched-inplace.txt).
- tests/test_path.py selection:127 passed/1skipped (full-tests.txt).
- Required skeleton workflow tox -e py:149 passed/1skipped, Ruff and mypy7files pass, overall coverage96% (tox-py.txt).
- Ruff direct lint/format and git diff check passed.

Repository AGENTS.md required reading https://blog.jaraco.com/skeleton/ in full. It was fetched/read before implementation; tox default was run with its default check extras. Build tooling generated an untracked LICENSE from the pre-existing package configuration; it is not part of the contribution. No new license choice was made.

This is a synthetic temporary-file failure-injection result, not a production incident, generic interruption atomicity claim or protection against failures before the initial backup rename. External author response/execution/acceptance, incorporation into upstream273 and merge are not observed at publication.
