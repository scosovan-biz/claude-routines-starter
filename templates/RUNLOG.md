# Run log

One line per run, appended by every routine on both surfaces. Never edit or tidy a line you did
not write; O2 counts lines that fail to parse and reports the count rather than repairing them.

Format, six fields separated by ` | `:

    {ISO timestamp} | {routine-id} | {run-id} | {OK|PARTIAL|FAILED} | {summary, 120 characters or fewer} | owner action: {none|S1/S2/S3 short text}

Example line (delete it before your first real run):

2026-09-04T07:04:11+10:00 | A1 | 20260904-0702-A1 | OK | 47 msgs, 9 follow-ups (3 P1), 7 drafts, 4 promises added | owner action: S3 no calendar source for item 6

Rotate this file monthly into `logs/archive/RUNLOG-YYYY-MM.md` once it passes a couple of thousand
lines. O2 raises an S2 at 2000 lines inside its seven-day window.
