# Owner actions

Everything a routine noticed that needs a person. Routines append rows and always write
`status = open` and `closed = -`. **You own the last two columns.** When you have acted on a row,
set `status` to `closed` and `closed` to today's date.

Severity:
- **S1** — the routine cannot run: expired login, revoked connector, quota exhausted, required
  input missing. Target: act within 1 day.
- **S2** — degraded: partial data, stale source, a signal it could not evaluate. Target: 7 days.
- **S3** — advisory: something worth knowing, nothing broken. Target: 30 days.

O2 measures time-to-owner-action from `logged` to `closed`. If nothing is ever closed it reports
"no owner action has been closed in this log", which is the finding, not a bug.

| logged | routine | run-id | severity | observed | recommended | status | closed |
|---|---|---|---|---|---|---|---|
| <YYYY-MM-DDTHH:MM:SS+ZZ:ZZ> | <routine-id> | <run-id> | <S1 or S2 or S3> | <what the routine observed> | <what it recommends> | open | - |
