# CI Drill: On-Call Runbook Live-Fire Drill

This repository hosts a live-fire rehearsal of the CI incident runbook.

## Workflows

- **Drill CI** (`.github/workflows/drill-ci.yml`): triggered on push and manual dispatch; contains a job with a step that deliberately exits non-zero (`exit 1`) so the run goes red on purpose.
- **Drill Soak** (`.github/workflows/drill-soak.yml`): manual dispatch only; single job that sleeps ~20 minutes to simulate a stuck/long-running build.

## Drill Steps

1. Push triggers the Drill CI run; confirm it goes red.
2. Grab the failed job's log as evidence.
3. Open a tracking issue titled `CI drill: broken build on main` with the failed run id in the body.
4. Dispatch the Drill Soak workflow and cancel it while it is in flight.
5. Re-run only the failed jobs of the Drill CI run.
6. Post a summary comment ending with `DRILL COMPLETE`.
