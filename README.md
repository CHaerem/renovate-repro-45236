# renovate-repro-45236

Minimal reproduction for [renovatebot/renovate#45236](https://github.com/renovatebot/renovate/issues/45236).

`.github/workflows/ci.yml` pins `actions/checkout` to an old commit with a `# v4` comment, so Renovate proposes a `digest` update to the commit `v4` points to now (`v4.4.0`, released 2026-07-20).
`renovate.json` sets `minimumReleaseAge: "3 days"` with the default `minimumReleaseAgeBehaviour: "timestamp-required"`.

The new commit is months old, so the update should pass `minimumReleaseAge`.
Instead, the branch stage logs `Marking 1 release(s) as pending, as they do not have a releaseTimestamp`, so `renovate/stability-days` stays pending.

Run Renovate with `--dry-run=full` against this repository to reach the branch-stage stability check.
