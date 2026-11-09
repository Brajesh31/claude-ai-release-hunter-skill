# Monitoring Schedule Runbook

## Configuration record

- Job name:
- Schedule:
- Time zone:
- Runtime environment:
- Working directory:
- State directory:
- Snapshot directory:
- Output directory:
- Delivery method:
- Operational owner:

## Before enabling the schedule

- [ ] Reporting window is explicit.
- [ ] State and snapshot directories persist between runs.
- [ ] Credentials are injected through a protected runtime mechanism.
- [ ] Logs redact tokens, addresses, and message credentials.
- [ ] The delivery recipient and command are validated.
- [ ] The first digest has been reviewed and approved.
- [ ] Retry and timeout behavior is bounded.
- [ ] An operator can pause or disable the job.

## Suggested daily execution sequence

1. Acquire a single-run lock to prevent overlapping jobs.
2. Read the previous successful state.
3. Calculate the reporting window.
4. Collect updates and classify failures.
5. Generate the message.
6. Save the message to durable storage.
7. Deliver through the approved mechanism.
8. Persist identifiers and snapshots only after successful delivery.
9. Append a run summary.
10. Release the job lock.

## Incident handling

| Condition | Action |
|---|---|
| Rate limit | Respect reset time and retry once when safe. |
| One platform unavailable | Continue other checks and mark the report incomplete. |
| State unreadable | Stop before delivery to avoid duplicate or lost updates. |
| Delivery failed | Preserve the message and do not advance state. |
| Overlapping job | Keep one active run and stop the duplicate. |
| Credential exposure | Disable delivery, rotate the credential, and inspect logs. |

## Run record

- Run ID:
- Window:
- Start time:
- End time:
- Platforms checked:
- Failures:
- Items included:
- Delivery result:
- State committed:
- Operator notes:

## Disable procedure

Stop future scheduled invocations, allow or terminate the active run safely, preserve state and logs, and record who disabled the job and why.