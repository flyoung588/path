# Round 7 Track D — recovery safety verification

Existing external PR https://github.com/Apeksha9389/path/pull/1 remains open. Initial actual checks found no author comments, inline comments or reviews; upstream jaraco/path273 head was unchanged. Root explicitly authorized deeper safety verification even without feedback.

Production behavior remains the prior fix 422ace870c13d7b22e8f5a7926bd9721460cd773. New safety-test commit b60ed5467ba21d751c5b97541b58aab8f0ac8938 adds 11 native cases to the SAME PR:

- reader and replacement descriptor closure on interrupted writer setup, plus exact KeyboardInterrupt/SystemExit object propagation;
- both streams and descriptors closed after success, RuntimeError, KeyboardInterrupt or SystemExit, in text/binary mode;
- custom backup suffix cleanup, original-content restoration, unchanged successful rewrite contents and permissions;
- failed rollback unlink preserves the original backup and partial replacement and propagates the exact rollback exception with the body error as context.

The new tests run against the author's production head bf1696f1e0b3f761a84510b400b042f7eae1537f fail 7 and pass 4 controls. Against current production fix all 11 pass, with TestInPlace totaling26 passes.

Actual platforms/interpreters:
- macOS/Python3.11.12: default tox160passed/1skipped; Ruff+mypy7files pass,96%coverage.
- macOS/Python3.10.17:26TestInPlace passed.
- macOS/Python3.13.3:26TestInPlace passed.
- Windows/Linux: NOT_RUN. No cross-platform pass is inferred from CI matrix configuration.

An initial full tox run failed due to an unused SIM115 noqa in a new test (159passed/1failure/1skipped). Original failure tox-py.txt is retained; unused suppression removed and identical default checks pass in tox-py-final.txt. Prior Round6 raw8failures are preserved in its existing evidence commit32c91fdc0084f823b94831120f18fc47d2a1fdfe.

CI availability checked without spending: own fork is public, Actions permissions report enabled, default main.yml/test-suite.yml files exist, and their platforms use standard GitHub-hosted runners. Official docs https://docs.github.com/en/actions/concepts/billing-and-usage state standard runners in public repos are free. However workflows API lists0 registered workflows; GET, enabling only main.yml and dispatching it each return404. Actual old/new head runs/checks count0. The attempted invocation is NOT a dispatch/completion result. No default branch, source workflow, billing or unrelated workflow was changed. No secrets were accessed. This API limitation is preserved in raw files.

Repo AGENTS.md and full required skeleton document https://blog.jaraco.com/skeleton/ were read before implementation; default tox checks were run. No generic filesystem atomicity or protection before initial backup rename is claimed. New tests establish bounded behaviors in this synthetic native failure injection, not author execution/adoption.
