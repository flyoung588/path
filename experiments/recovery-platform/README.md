# Round 8 Track D — actual free Linux and Windows recovery checks

Event check: Apeksha9389/path PR1 is open, no comments/reviews, head b60ed5467ba21d751c5b97541b58aab8f0ac8938. Upstream jaraco/path273 remains bf1696f1e0b3f761a84510b400b042f7eae1537f and does not include our added native tests. No developer request or adoption is claimed.

Actual CI run: https://github.com/flyoung588/path/actions/runs/40800878675
Exact CI commit: aed5f362447c9c7b24017355a1005d0f221f938a

Completed jobs, Python3.13.16:
- Linux standard ubuntu-latest:187 passed,1skipped; full default tox success.
  https://github.com/flyoung588/path/actions/runs/40800878675/job/123208428461
- Windows standard windows-latest:181 passed,7skipped; full default tox success.
  https://github.com/flyoung588/path/actions/runs/40800878675/job/123208428848

Both jobs used actual hosted runners. Raw logs, dependency output, run/job APIs and source SHA256 checks are retained. path/__init__.py, tests/test_path.py and the news fragment are byte-identical to collaboration safety commit b60ed5467ba21d751c5b97541b58aab8f0ac8938. No production/regression-test changes were made in Round8.

An isolated owned-public-fork branch ci/recovery-safety-linux-windows-20261029 replaces inherited workflows only on that branch with a push-filtered test-only workflow. It uses contents:read, checkout without persistent credentials, standard ubuntu-latest/windows-latest, Python3.13 and tox. No release/deploy/artifact-upload/secret references, default-branch writes, billing changes, larger/self-hosted runners or payments. The external PR contains no CI workflow changes.

Official eligibility reference: https://docs.github.com/en/actions/concepts/billing-and-usage (standard hosted runners in public repos are free). Trigger reference: https://docs.github.com/en/actions/how-tos/write-workflows/choose-when-workflows-run/trigger-a-workflow (push examines workflow at pushed ref; workflow_dispatch requires default registration). Repo public visibility and enabled Actions permissions were read back.

Prior 404/zero-workflow evidence did not prove universal lack of CI. An immediate post-push list also reported0, but the new workflow subsequently registered active and its push run completed. Why inherited main.yml was not registered earlier is not established. First branch commit f88d844 removed inherited workflows; creating the new file initially failed because the empty workflow directory had been removed. That commit did not configure a new workflow/run. Next commit aed5f36 created the directory and actual workflow; only its run is claimed.

These are bounded synthetic recovery tests and default project checks on the stated runner images/interpreter. They do not establish all-filesystem atomicity or protect failures before initial backup rename. Author execution, acceptance, branch merge and upstream absorption remain unobserved. Earlier macOS failures/receipts remain preserved under Round6/7 evidence.


Named safety coverage confirmation: https://github.com/flyoung588/path/actions/runs/40801416555 completed successfully on CI commit0e88679bf1893fb052660f37967d8728372d8cb2. Same two OS/interpreter configurations were repeated with only pytest verbosity/skip-reason flags added, because the original full-success dots did not identify recovery nodes or skip reasons. This was not an additional combination or production change. Both Linux and Windows logs show exactly26 named TestInPlace nodes PASSED and0 recovery skips. Linux full187pass/1skip; Windows full181pass/7skips.

Actual unrelated skips: Linux lacks Path.startfile. Windows lacks os.statvfs, os.pathconf, Path.chown, Path.group and Path.chroot; an existing Windows/Python>3.12 condition skips test_glob_win32 (see raw node/log); an invalid-path-encoding test skips because that encoding is disallowed. Exact raw reasons/locations and all52 recovery node outcomes are in native-coverage-confirmation.json; both raw verbose logs are retained. Source identity is verified independently for both completed CI commits.
