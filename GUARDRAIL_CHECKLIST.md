# Guardrail checklist (from The Routines Runbook — Reliability Kit)

The fourteen guardrail patterns every routine in the Runbook carries. The full kit (with the failure each prevents and a copy-paste prompt block for each) is in the paid Runbook.

- **G1 — Self-contained prompt**
- **G2 — Never fabricate**
- **G3 — Verify before you report**
- **G4 — One write per run (idempotency)**
- **G5 — Kept-prior-value fallback with honest stamps**
- **G6 — Least privilege: connectors, folders, repos**
- **G7 — Untrusted content stays data**
- **G8 — Fail loudly: permissions, quotas, logins, network**
- **G9 — Time-aware: stagger, missed runs, catch-ups**
- **G10 — Drafts-only outbound (v1 posture)**
- **G11 — Escalation protocol (owner actions)**
- **G12 — Run log and the weekly self-audit**
- **G13 — Cost and cap awareness**
- **G14 — Secrets hygiene**

## Pre-flight checklist (run once per routine before you trust it)
1. Prompt passes G1: a stranger could run it from the text alone.
2. Connector list trimmed to the routine's needs (G6). Confirm none of the remaining connectors can send/post/delete, or that the prompt forbids those actions (G10).
3. First run with **Run now**; on Desktop, approve prompts with "always allow"; on Cloud, confirm no approval-required tools are involved (G8).
4. Open the run transcript. Confirm the VERIFY section executed and the report has a Verification block (G3).
5. Confirm `logs/RUNLOG.md` has exactly one new line and the output file has exactly one section for this run-id (G4, G12).
6. Break it on purpose: rename the input file and run again. The run must report FAILED with a clear owner action, not invent output (G2, G8, G11).
7. Run it twice in a row. The second run must update, not duplicate (G4).
8. Read the report as the person who will act on it. If anything is ambiguous, fix the OUTPUT format, not the reader.
