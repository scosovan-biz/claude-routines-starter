# Alerts

Every blocked tool call, quota error, login failure, timeout and permission block, written by the
routine that hit it. The `error` column holds the **exact** text, truncated at 300 characters —
never a paraphrase. O2 groups repeated error signatures from this column, and a paraphrased error
is an error that will never be recognised as a repeat.

Severity: S1 the routine cannot run · S2 degraded · S3 advisory.

| logged | routine | run-id | severity | step | error |
|---|---|---|---|---|---|
| <YYYY-MM-DDTHH:MM:SS+ZZ:ZZ> | <routine-id> | <run-id> | <S1 or S2 or S3> | <which step failed> | <exact error text, at most 300 characters> |
