---
name: superset-quarantine-to-green
description: Diagnose and restore a quarantined (skipped) Superset test, or complete a scoped test-hygiene migration, ending in a reviewable PR with root cause and validation evidence. Use when remediating a GitHub issue that references a skipped test or a scoped deprecated-API cleanup in this repository.
---

# superset-quarantine-to-green

Procedure for converting an approved test-debt issue in this repository into a
verified pull request. Follow the steps in order; do not skip the reproduction
step.

## Procedure

1. Read the GitHub issue named in your task, then read `CLAUDE.md` and any
   `AGENTS.md` files relevant to the paths you will touch. They define this
   repository's conventions, including pre-commit requirements.
2. Reproduce the smallest relevant failure before editing anything. For a
   skipped test: remove the skip locally and run the focused test to observe
   the actual failure. Record the exact command and output.
3. Investigate the root cause. Treat any hypothesis stated in the issue as a
   hypothesis to verify, not a prescribed fix.
4. Make the smallest safe correction. Prefer fixing test isolation, fixtures,
   or genuine product defects over restructuring.
5. Remove the skip (when the issue targets a skipped test) only after the
   behavior passes locally.
6. Run, in order: the focused test (repeat it several times if the failure was
   intermittent), the containing test module, and applicable pre-commit checks
   (stage files first — pre-commit only checks staged files).
7. Inspect your final diff for unrelated changes and remove them.
8. Open exactly one pull request against this repository's `master` branch. The
   description must include: the root cause, why the change preserves intended
   behavior, every validation command you ran with its result, and remaining
   risks.
9. Report your result through the session's structured output.

## Forbidden

- Weakening, deleting, or loosening test assertions to make a test pass.
- Replacing one skip with another skip, an xfail, retries, or sleeps.
- Introducing test-order dependence or hard-coded global IDs.
- Broad refactors, drive-by cleanups, or edits outside the issue's scope.
- Pushing to or opening PRs against `apache/superset` (read-only upstream).
- Merging any pull request; the PR is for human review.
- Editing CI workflow files or this skill file.
